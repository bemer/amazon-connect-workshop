+++
title = "Create an Amazon Connect Instance"
weight = 23
+++


In this module we are going to create an Amazon Connect Instance that we will use through out the remainder of the workshop. Open the AWS management console, select the appropriate region, and navigate to the Amazon Connect console. If this is the first time launching a Connect Instance you will see a Get Started page. Click on the button Get Started.

When selecting a region review the [Amazon Connect Pricing Page](https://aws.amazon.com/connect/pricing/) to determine which region will have telephone numbers available for the countries you are supporting with your Contact Center.

![CreateConnectInstance](/images/create-a-connect-instance/getting_started_with_connect.png)

When configuring an Amazon Connect Instance you will need to configure 4 key elements.

- Identity
- Administrator Account
- Telephony Options
- Data and Storage

In this workshop we are going to select SAML 2.0 based authentication for our Amazon Connect Instance. This feature enables you to use your organiztions existing Identity Provider for authentication. 

{{% notice tip %}}
Once you choose your Identity management system and create the Instance this configuration cannot be changed. Carefully plan your identity managment design before creating your Instance. As a best practice we recommend using SAML integration for identity management.
{{% /notice %}}

Select the radio button for SAML 2.0-based authentication and the fill in the Access URL box with a name for your Instance. The name must be unique and cannot be changed after configuration of the Instance is complete. In this example we are using aws-connect-workshop-123, and you can use the same convention just append a random 4 digit number to the end of the name.

![CreateConnectInstance](/images/create-a-connect-instance/identity_management.png)


Next we will configure an Administrator Account that can be used for accessing the Amazon Connect Console. Provide the firstname, lastname, and username for the admin user. The login is case sensitive.
Click **Next Step**

![CreateConnectInstance](/images/create-a-connect-instance/administrator.png)

Now we will configure Telephony Options for your Connect Instance. Amazon Connect offers the ability to accept inbound calls, make outbound calls, or both. We will leave the default here to allow both incoming and outbound calls. Click **Next Step**

![CreateConnectInstance](/images/create-a-connect-instance/telephony_options.png)


Now we will configure Data Storage Options for Amazon Connect. Amazon Connect uses **S3** to store data such as Call Recordings, Chat Transcripts, and Reports. Amazon Connect uses **CloudWatch** to store log data.

![CreateConnectInstance](/images/create-a-connect-instance/data_storage.png)

Click **Customize Settings**: on the Data storage condfiguration page. This will bring up the default storage configuration for the Instance and allow you customize the settings. It is important to understand the configuration. You can customize if needed for your deployment, but for the workshop we will use the default. Click **Next Step**

![CreateConnectInstance](/images/create-a-connect-instance/data_storage_customization.png)

{{% notice tip %}}
Customers can bring their own KMS key for encrypting data in S3. 
{{% /notice %}}

Now we will review the configuration setting for our Instance. Click **Create Instance**

![CreateConnectInstance](/images/create-a-connect-instance/review_create_instance.png)

Once the Instance is created your will see the following page. Click **Get Started**

![CreateConnectInstance](/images/create-a-connect-instance/get_started.png)

You will be brought the Amazon Connect console. Click **Lets Go** to begin configuring your Connect Instance.

![CreateConnectInstance](/images/create-a-connect-instance/getting_started_with_connect.png)

{{% notice tip %}}
Make sure to click Allow on the browser window requesting access to your microphone.
{{% /notice %}}

After clicking the Lets Go button you will be brought to the Connect **Claim a Phone Number** page. On this page you can select a phone number for your Instance. You have 3 options when choosing a number

- Country
- Type Direct Dial or Toll Free
- Phone Number

Select a number for the appropriate country, use a direct dial number, and pick a phone number from the list.

![CreateConnectInstance](/images/create-a-connect-instance/claim_phone_number.png)

{{% notice tip %}}
If you do not see a number you require for your production Instance open a Support Request with AWS support to check on the availability of numbers you are looking for. This could be for example a certain area code where you do business.
{{% /notice %}}

Click **Next**

Wait a couple of minutes for the new number to be configured in your Instance. The next screen is going to show you the number to call and show the **Contact Control Panel** embedded in the page. The **Contact Control Panel** is the Agents interface to handle incoming Contacts. 

![CreateConnectInstance](/images/create-a-connect-instance/make_a_call.png)

Call the number you requested from your mobile phone. You will be sent to the default sample **Contact Flow**. Press 1 to be placed in queue for an agent. Press 1 again to move to the front of the queue and press 1 to go in Queue. You will get a notification within the **Contact Control Panel** that you have an incoming call. Press the **Green Check** button to accept the contact.

![CreateConnectInstance](/images/create-a-connect-instance/incoming_contact.png)

You are now connected to your customer and have made your first call through your Amazon Connect Instance. This is the first step in delivering on your Customer Experience goals. Now we will head to configuring your Connect Contact Center.

![CreateConnectInstance](/images/create-a-connect-instance/connected_call.png)

Press the **Continue** button. This will bring you to the Amazon Connect Dashboard.

{{% notice tip %}}
The Connect Admin guide is a useful resource that can help you through out the workshop. [official documentation](https://docs.aws.amazon.com/connect/latest/adminguide/amazon-connect-get-started.html).
{{% /notice %}}
