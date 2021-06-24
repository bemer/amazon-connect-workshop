+++
title = "Configure the AWS SSO for Admins"
weight = 24
+++

After creating an SSO application that will be used by your agents, it is time to create another application that will provide access to the Amazon Connect admin console. We will be repeating the previous steps with a couple of changes.

Start by acessing the [AWS SSO applications page](https://console.aws.amazon.com/singlesignon/home#/applications) and adding a new application. select **Add application** , *Amazon Connect* and then choose **Add application**.

Name this application **Amazon Connect - Admin**. Download the metadata file available in the *AWS SSO Metadata* section and in the **Relay state** field you should add the following URL:

    https://<region-id>.console.aws.amazon.com/connect/federate/<instance-id>

Note that this URL is different from the previous one, where it provides access to the Amazon Connect administrator dashboard instead of redirecting the users to the softphone interface. Make sure you are replacing the *\<region-id\>* and the *\<intance-id\>* with your information.

After downloading the metadata file and changing the **Relay state** URL field, choose **Save changes**.

Now, access the [AWS IAM console](https://console.aws.amazon.com/iam/home), select **Identity providers** from the navigation menu and select **Create provider** .

For the provider type, select **SAML**, name it **AmazonConnectAdminAccess**, upload the most recent metadata file and choose **Next step**:

![CreateIdp](/images/enable-aws-sso/iam_create_admin_provider.png)

After validating the information, select **Create**.

Now, access the [AWS IAM Roles](https://console.aws.amazon.com/iam/home#/roles) page and select **Create role** to create the role that will be used by the new AWS SSO application. In this screen, select **SAML 2.0 federation** as the Role type and make sure you select the **AmazonConnectAdminAccess** SAML provider. Select **Allow programmatic and AWS Management Console access** and choose **Next Permissions** :

![CreateIAMAdminRole](/images/enable-aws-sso/create_iam_admin_role.png)

In the following screen, select the **AmazonConnectSSOPolicy** policy and choose **Next tags**. On the tags screen, select **Next review**. 

Name your role **AmazonConnectAdminAccessRole** and choose **Create role**.

After creating the IAM Role, access the [AWS SSO applications page](https://console.aws.amazon.com/singlesignon/home#/applications) and choose the **Amazon Connect - Admin** application. In the application page, select the **Attribute mappings** tab and create a new attribute with the following content:

    Attribute: https://aws.amazon.com/SAML/Attributes/Role
    Value: <IAM role ARN>,<IAM identity provider ARN>

The Value field will be similar to:

    arn:aws:iam::123456789012:role/AmazonConnectAdminAccessRole,arn:aws:iam::123456789012:saml-provider/AmazonConnectAdminAccess

After changing this information, choose **Save changes** .