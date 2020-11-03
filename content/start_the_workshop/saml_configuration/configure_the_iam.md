+++
title = "Configure the IAM IdP"
weight = 22
+++


After configuring the AWS SSO, it is time to get back to the IAM and create an *Identity provider* and proper IAM Policy and IAM Role. The IAM identity provider is used to configure AWS SSO as an IdP for SAML 2.0 federation while the IAM policy and role are used for the directory users to assume an IAM role and access an Amazon Connect instance.

In the IAM console, in the [Identity providers](https://console.aws.amazon.com/iam/home#/providers) menu, click in the button **Create Provider**:

![CreateIdp](/images/enable-aws-sso/create_idp.png)

As the **Provider Type**, select **SAML**, give it the name of **AmazonConnectAgentAccess** and upload the AWS SSO metadata file that you downloaded before from the AWS SSO page:

![CreateIdp](/images/enable-aws-sso/iam_create_provider.png)

Click in **Next Step** and than in **Create**.

After creating the Identity Provider, it is time to create a new IAM Policy. To do so, access the [IAM Policies](https://console.aws.amazon.com/iam/home#/policies) console and click in **Create Policy**. In this page, switch to the JSON tab and past the following code, replacing the **connect instance ARN** with your current instance ARN:

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

After updating the JSON content, click in **Review policy**. Name your policy **AmazonConnectSSOPolicy** and click in **Create policy**.

Now, let's create an IAM Role that will be used by the federated users so they can access the Amazon Connect instance. You can click in [this link](https://console.aws.amazon.com/iam/home#/roles) to access the IAM Roles menu. Once in the Roles screen, click in the button **Create role**. For the Role type, in the top menu, you should select **SAML 2.0 federation** and use the following configurations:

* For *SAML provider* select **AmazonConnectAgentAccess**
* Choose **Allow programmatic and AWS Management Console access**

After picking the right configuration, click in **Permissions**:

![CreateIamRole](/images/enable-aws-sso/create_iam_role.png)

In the *Attach permissions policies* menu, you should select **AmazonConnectSSOPolicy**. You can use the search to filter for this policy. After selecting the policy, click in **Next: Tags**:

![SelectIamPolicy](/images/enable-aws-sso/select_iam_policy.png)

In the *Add tags (optional)* scree, just click in **Next: Review**. Name your role **AmazonConnectAgentAccessRole** and click in **Create role**.

After creating your role, take note of the IAM role ARN. You use it later while configuring the AWS SSO application. For example:

    arn:aws:iam::<account id without hyphen>:role/AmazonConnectAgentAccessRole

After creating the Identity Provider, IAM policy and IAM Role, it is time to get back to the AWS SSO an nao the attribute values.

{{% notice tip %}}
Some service providers require custom SAML assertions to pass additional data about your user sign-ins. In that case, use the following procedure to specify how your applications user attributes should map to corresponding attributes in AWS SSO. You can find more information about it in the [official documentation](https://docs.aws.amazon.com/singlesignon/latest/userguide/mapawsssoattributestoapp.html).
{{% /notice %}}

Get back to the [AWS SSO console](https://console.aws.amazon.com/singlesignon/home) and, under the *Applications* menu, select the application called **Amazon Connect** that we created previously. There, you should select the tab **Attribute mappings** and add a new attribute mapping with the following information:

    Attribute: https://aws.amazon.com/SAML/Attributes/Role
    Value: <IAM role ARN>,<IAM identity provider ARN>

The *Value* field will be similar to:

    arn:aws:iam::123456789012:role/AmazonConnectAgentAccessRole,arn:aws:iam::123456789012:saml-provider/AmazonConnectAgentAccess

After adding the new attribute, click in **Save changes**:

![SsoAttributeMapping](/images/enable-aws-sso/sso_attribute_mapping.png)