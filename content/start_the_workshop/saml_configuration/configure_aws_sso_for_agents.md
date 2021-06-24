+++
title = "Configure AWS SSO for Agents"
weight = 21
+++


In this module we are going to enable [AWS Single Sign-On (SSO)](https://aws.amazon.com/single-sign-on/) and configure it as the identity provider for our Amazon Connect Instance. 

{{% notice info %}}
Note that for the purpose of this workshop we will be leveraging AWS SSO as the identity provider to authenticate our users in the Amazon Connect instance, but you can use different tools as stated in the [documentation](https://docs.aws.amazon.com/connect/latest/adminguide/configure-saml.html).
{{% /notice %}}

The first step is to enable AWS SSO. To do so, access the [AWS SSO console](https://console.aws.amazon.com/singlesignon/home). In this page, you can choose **Enable AWS SSO**:

![EnableAwsSso](/images/enable-aws-sso/enable_sso.png)

AWS SSO requires the [AWS Organizations](https://aws.amazon.com/organizations/) service. To get everything up and running, you should now choose **Create AWS organization**. This will create an AWS Organization and setup AWS SSO for you:

![CreateOrganization](/images/enable-aws-sso/create_organization.png)

After creating your Organization and setting up AWS SSO, you will be redirected to the AWS SSO main page:

![SsoDashboard](/images/enable-aws-sso/sso_dashboard.png)

Let's now add the Amazon Connect integration. To do so, you should choose **Applications** in the left side menu, and then select **Add a new application**:

![AddNewApplication](/images/enable-aws-sso/add_new_application.png)

{{% notice info %}}
Note that you can leverage AWS SSO to handle the authentication for multiple applications. When implementing Amazon Connect, it is a best practice that you create two different applications: one for your Connect agents and another one for the Amazon Connect instance administrators. During this workshop, we will demonstrate how to provision the application that will be used by the Amazon Connect agents.
{{% /notice %}}

In the search box, type **Amazon Connect**. It will find the *Amazon Connect* app. You can then choose the application logo and then select the **Add application** to move to the application configuration page:

![AmazonConnectApp](/images/enable-aws-sso/amazon_connect_app.png)

In this page, name your application **Amazon Connect - Agent** and make sure that you download the **AWS SSO SAML metadata file**. You will find a download link just in the **AWS SSO Metadata** section. After downloading the metadata file, go ahead and change the **Relay state** field under **Application Properties**. In this box, please insert the following, making sure that you replace the data with the right AWS region and your Amazon Connect instance ID:

    https://\<region-id>.console.aws.amazon.com/connect/federate/\<instance-id>?destination=%2Fconnect%2Fccp

You can find information about the Amazon Connect instance ID in the [Amazon Connect console](https://console.aws.amazon.com/connect/home) by viewing the instance details. It is the last part of the *Instance ARN*. In my case, the ARN is: 

    arn:aws:connect:us-east-1:257804509653:instance/9690dd9b-3de7-4097-b4d9-67829f7c8fur

Which means that the Amazon Connect instance ID will be:

    9690dd9b-3de7-4097-b4d9-67829f7c8fur

Since my instance is in the *us-east-1* region, my **Relay state** URL will be:

      https://us-east-1.console.aws.amazon.com/connect/federate/9690dd9b-3de7-4097-b4d9-67829f7c8fur?destination=%2Fconnect%2Fccp


After downloading the metadata file and changing the **Relay state** URL field, keep all the rest as default and choose **Save changes**:

![RelayStateUrl](/images/enable-aws-sso/relay_state_url.png)

