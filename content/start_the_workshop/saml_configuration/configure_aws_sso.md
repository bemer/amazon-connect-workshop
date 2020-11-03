+++
title = "Configure AWS SSO"
weight = 21
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

