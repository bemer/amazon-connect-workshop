+++
title = "Configure the IAM IdP"
weight = 22
+++


After configuring AWS SSO, it is time to get back to the IAM and create an *Identity provider*, *IAM Policy*, and *IAM Role*. The IAM identity provider is used to configure AWS SSO as an IdP for SAML 2.0 federation. The IAM policy and role are provide the role and permissions that allow users to access the Amazon Connect instance.

In the IAM console, in the [Identity providers](https://console.aws.amazon.com/iam/home#/providers) menu, select **Create Provider**:

![CreateIdp](/images/enable-aws-sso/create_idp.png)

As the **Provider Type**, select **SAML**, give it the name of **AmazonConnectAgentAccess** and upload the AWS SSO metadata file that you downloaded before from the AWS SSO page:

![CreateIdp](/images/enable-aws-sso/iam_create_provider.png)

choose **Next Step** and than in **Create**.

Once the identity provider is created, you can create the IAM policy. To do so, access the [IAM Policies](https://console.aws.amazon.com/iam/home#/policies) console and choose **Create Policy**. In this page, switch to the JSON tab and past the following code, replacing the **connect instance ARN** with your Amazon Connect instance ARN:

    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Sid": "Statement1",
                "Effect": "Allow",
                "Action": "connect:GetFederationToken",
                "Resource": [
                    "<connect instance ARN>/user/${aws:userid}"
                ]
            }
        ]
    }

After updating the JSON content, choose **Review policy**. Name your policy **AmazonConnectSSOPolicy** and choose **Create policy**.

Now, let's create an IAM Role that will be used by the federated users so they can access the Amazon Connect instance. Access the [IAM Roles menu](https://console.aws.amazon.com/iam/home#/roles). Once in the Roles screen, select **Create role**. For the Role type, select **SAML 2.0 federation** and use the following configurations:

* For *SAML provider* select **AmazonConnectAgentAccess**
* Choose **Allow programmatic and AWS Management Console access**

After completing the configuration, select **Permissions**:

![CreateIamRole](/images/enable-aws-sso/create_iam_role.png)

In the *Attach permissions policies* menu, you should select **AmazonConnectSSOPolicy**. You can use the search to filter for this policy. After selecting the policy, choose **Next: Tags**:

![SelectIamPolicy](/images/enable-aws-sso/select_iam_policy.png)

In the *Add tags (optional)* screen, leave everything to default and select **Next: Review**. Name your role **AmazonConnectAgentAccessRole** and choose **Create role**.

After creating your role, take note of the IAM role ARN. You use it later while configuring the AWS SSO application. For example:

    arn:aws:iam::<account id without hyphen>:role/AmazonConnectAgentAccessRole

After creating the Identity Provider, IAM policy and IAM Role, return to the AWS SSO console an add the attribute values to the application.

{{% notice tip %}}
Some service providers require custom SAML assertions to pass additional data about your user sign-ins. In that case, use the following procedure to specify how your application's user attributes should map to corresponding attributes in AWS SSO. You can find more information about it in the [official documentation](https://docs.aws.amazon.com/singlesignon/latest/userguide/mapawsssoattributestoapp.html).
{{% /notice %}}

Get back to the [AWS SSO console](https://console.aws.amazon.com/singlesignon/home) and, under the *Applications* menu, select the application called **Amazon Connect** that we created previously. There, you should select the tab **Attribute mappings** and add a new attribute mapping with the following information:

    Attribute: https://aws.amazon.com/SAML/Attributes/Role
    Value: <IAM role ARN>,<IAM identity provider ARN>

The *Value* field will be similar to:

    arn:aws:iam::123456789012:role/AmazonConnectAgentAccessRole,arn:aws:iam::123456789012:saml-provider/AmazonConnectAgentAccess

After adding the new attribute, choose **Save changes**:

![SsoAttributeMapping](/images/enable-aws-sso/sso_attribute_mapping.png)