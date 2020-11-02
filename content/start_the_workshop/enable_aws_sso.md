+++
title = "Enable AWS SSO"
weight = 22
+++


In this module we are going to enable the [AWS Single Sign-On (SSO)](https://aws.amazon.com/single-sign-on/) and configure it as the identity provider for our Amazon Connect Instance. 

{{% notice info %}}
Note that for the purpose of this workshop we will be leveraging the AWS SSO as the identity provider to authenticate our users in the Amazon Connect instance, but you can use different tools as stated in the [documentation](https://docs.aws.amazon.com/connect/latest/adminguide/configure-saml.html).
{{% /notice %}}

The first step is to enable the AWS SSO. To do so, access the [AWS SSO console](https://console.aws.amazon.com/singlesignon/home). In this page, you can click in the **Enable AWS SSO** button:

![EnableAwsSso](/images/enable-aws-sso/enable_sso.png)

AWS SSO requires the [AWS Organizations](https://aws.amazon.com/organizations/) service. To get everything up and running, you should now click in **Create AWS organization**. It will create an AWS Organization and setup the AWS SSO for you:

![CreateOrganization](/images/enable-aws-sso/create_organization.png)

After creating your Organization and setting up the AWS SSO, you will be redirected to the AWS SSO main page:

![SsoDashboard](/images/enable-aws-sso/sso_dashboard.png)

Let's now add the Amazon Connect integration. To do so, you should click in **Applications** in the left side menu, and then click in the **Add a new application** button:

![AddNewApplication](/images/enable-aws-sso/add_new_application.png)

In the search box, type **Amazon Connect**. It will find the *Amazon Connect* app. You can then click in the application logo and then in the **Add application** button to move to the application configuration page:

![AmazonConnectApp](/images/enable-aws-sso/amazon_connect_app.png)

In this page, make sure that you download the **AWS SSO SAML metadata file**. You will find a download link just in the **AWS SSO Metadata** section. After downloading the metadata file, go ahead and change the **Relay state** field under **Application Properties**. In this box, please insert the following, making sure that you replace the data with the right AWS region and your Amazon Connect instance ID:

    https://\<region-id>.console.aws.amazon.com/connect/federate/\<instance-id>?destination=%2Fconnect%2Fccp

You can find information about the Connect instance ID in the [Amazon Connect console](https://console.aws.amazon.com/connect/home) when clicking in your connect instance. It is the last part of the *Instance ARN*. In my case, the ARN is: 

    arn:aws:connect:us-east-1:257804509653:instance/9690dd9b-3de7-4097-b4d9-67829f7c8fur

It means that the Connect instance ID will be:

    9690dd9b-3de7-4097-b4d9-67829f7c8fur

That being said, since I am running the worshop in *us-east-1*, the URL I'll add to the **Relay state** field will be:

      https://us-east-1.console.aws.amazon.com/connect/federate/9690dd9b-3de7-4097-b4d9-67829f7c8fur?destination=%2Fconnect%2Fccp


After downloading the certificate and changing the **Relay state** URL fiel, keep all the rest as default and click in **Save changes**:

![AmazonConnectApp](/images/enable-aws-sso/amazon_connect_app.png)

After configuring the AWS SSO, it is time to get back to the IAM and create an *Identity provider* and proper IAM Policy and IAM Role. The IAM identity provider is used to configure AWS SSO as an IdP for SAML 2.0 federation while the IAM policy and role are used for the directory users to assume an IAM role and access an Amazon Connect instance.

In the IAM console, in the [Identity providers](https://console.aws.amazon.com/iam/home#/providers) menu, click in the button **Create Provider**:

![CreateIdp](/images/enable-aws-sso/create_idp.png)

As the **Provider Type**, select **SAML**, give it the name of **Connect-SSO** and upload the AWS SSO metadata file that you downloaded before from the AWS SSO page:

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

After updating the JSON content, click in **Review policy**. Name your policy **Connect-SSO-Policy** and click in **Create policy**.

Now, let's create an IAM Role that will be used by the federated users so they can access the Amazon Connect instance. You can click in [this link](https://console.aws.amazon.com/iam/home#/roles) to access the IAM Roles menu. Once in the Roles screen, click in the button **Create role**. For the Role type, in the top menu, you should select **SAML 2.0 federation** and use the following configurations:

* For *SAML provider* select **Connect-SSO**
* Choose **Allow programmatic and AWS Management Console access**

After picking the right configuration, click in **Permissions**:

![CreateIamRole](/images/enable-aws-sso/create_iam_role.png)

In the *Attach permissions policies* menu, you should select **Connect-SSO-Policy**. You can use the search to filter for this policy. After selecting the policy, click in **Next: Tags**:

![SelectIamPolicy](/images/enable-aws-sso/select_iam_policy.png)

In the *Add tags (optional)* scree, just click in **Next: Review**. Name your role **Connect-SSO** and click in **Create role**.

After creating your role, take note of the IAM role ARN. You use it later while configuring the AWS SSO application. For example:

    arn:aws:iam::<account id without hyphen>:role/Connect-SSO

After creating the Identity Provider, IAM policy and IAM Role, it is time to get back to the AWS SSO an nao the attribute values.

{{% notice tip %}}
Some service providers require custom SAML assertions to pass additional data about your user sign-ins. In that case, use the following procedure to specify how your applications user attributes should map to corresponding attributes in AWS SSO. You can find more information about it in the [official documentation](https://docs.aws.amazon.com/singlesignon/latest/userguide/mapawsssoattributestoapp.html).
{{% /notice %}}

Get back to the [AWS SSO console](https://console.aws.amazon.com/singlesignon/home) and, under the *Applications* menu, select the application called **Amazon Connect** that we created previously. There, you should select the tab **Attribute mappings** and add a new attribute mapping with the following information:

    Attribute: https://aws.amazon.com/SAML/Attributes/Role
    Value: <IAM role ARN>,<IAM identity provider ARN>

The *Value* field will be similar to:

    arn:aws:iam::123456789012:role/Connect-SSO,arn:aws:iam::123456789012:saml-provider/Connect-SSO

After adding the new attribute, click in **Save changes**:

![SsoAttributeMapping](/images/enable-aws-sso/sso_attribute_mapping.png)

After configuring the SSO, it is time to go ahead and create some users. With the SSO setup, users are created and defined in the Connect instance but all the password management will happen through the SSO. Let's then create a new user and see how this integration looks like.

The first step here is to access your Amazon Connect instance with your administrator account (that we created in the previous lab) and create a new user. To do so, visit the [Amazon Connect console](https://console.aws.amazon.com/connect/home) and click in the *Access URL*. You will be taken to the Amazon Connect management portal. In this dashboard, click in the *User management* menu in the left side:

![ConnectUserManagement](/images/enable-aws-sso/user_management.png)

In the new screen, click in **Add new users** buton in the top right corner:

![AddNewUsers](/images/enable-aws-sso/add_new_users.png)

There are mainly two options to create users in the Amazon Connect instance: manually and upload a template with multiple users. In our case, let's just create a single users that we will use for testing. In the *Add new users* screen, make sure that the option **Create and set up a new user.** is selected and click in **Next**.

Fill the user information making sure that you are using a valid email address. Please note that the email used in this step will have to match with the email for the user provisioned in the SSO instance. 

After filling the user information, select the **Routing profile** and for the security profile select **Agent**. After filling the user information, click in **Save**:

![AddUserInfo](/images/enable-aws-sso/add_user_information.png)


In the confirmation screen, click in the **Create users** button.

![CreateUser](/images/enable-aws-sso/create_user.png)

After creating the user in the Connect instance, it is time to provision the user in the SSO. To do so, access the [AWS SSO console](https://console.aws.amazon.com/singlesignon/home#/users) and under the *Users* menu click in the **Add User** button. Then, add information about the new user. Make sure that you are using the **same email address that you used when creating the user in the Connect instance**. After, click in the **Next: Groups** button:

![CreateSsoUser](/images/enable-aws-sso/create_sso_user.png)

To make our life easier, let's now create a group that will be used by all the Connect Agents. To do so, click in the **Create group** button in the top of the screen. Name your group *ConnectAgents* and click in the **Create button**. After creating the group, make sure you have it selected in the Groups screen before clicing in the **Add user** button.

After creating the user and the group, you should get back to the Connect application created in the SSO and allow access to it. To do so, click in the [Applications menu](https://console.aws.amazon.com/singlesignon/home#/applications) on the SSO page and click in the *Amazon Connect* application. There, navigate to the **Assigned users** tab and click in the button **Assign users**:

![AssignSsoUsers](/images/enable-aws-sso/assign_sso_users.png)

Now, select the *Groups* tab, select the *ConnectAgents* group and click in the button **Assign users**:

![AssignUsers](/images/enable-aws-sso/assign_users.png)

By selecting the group there, it will be easier for you to add more agents in your Connect instance in the future, so you don't need to assign every individual user to the Connect application created on the AWS SSO.

When creating the new user, an email will be sent to the email address used with information about the Single Sign-On instance. You will have to click in the **Accept invitation** link, to be redirected to the SSO portal. A password change will be requested and after changing the password, you will be able to login to the SSO and see the Amazon Connect application:

![ConnectSsoApplication](/images/enable-aws-sso/connect_sso_application.png)

When clicking in the Connect application, you will be redirected to the Connect agent interface and will be able to start receiving and answering calls.