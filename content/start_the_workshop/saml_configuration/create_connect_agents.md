+++
title = "Create Amazon Connect agents"
weight = 23
+++

After configuring AWS SSO, it is time to go ahead and create the first Amazon Connect agents. With AWS SSO setup, users are created and defined in the Connect instance but all  password management will happen through the AWS SSO. Let's then create a few Connect users and see how this integration looks like.

The first step here is to access your Amazon Connect instance with your administrator account (that we created in the previous lab) and create a new user. To do so, visit the [Amazon Connect console](https://console.aws.amazon.com/connect/home) and choose *Access URL*. The Amazon Connect administration interface will open in a new tab or window. From the home page, select *User management* from the main navigation menu:

![ConnectUserManagement](/images/enable-aws-sso/_user_management.png)

On the User management page, select **Add new users**:

![AddNewUsers](/images/enable-aws-sso/_add_new_users.png)

There are two ways to create users in the Amazon Connect administration interface: manually and bulk upload using a template. For our workshop purposes, we are going to create two different agents, named **agent1** and **agent2**, so in the **Add new users** button on the top right corner of the **User management** screen, make sure that the option **Create and set up a new user** is selected and choose **Next**:

![CreateSetupUser](/images/enable-aws-sso/_create_setup_user.png)


Enter **Agent** for the First Name and **1** for the last name. Enter **agent1@connect-workshop.com** for the Login Name. After adding this information, select the **Basic Routing Profile** as the *Routing Profile* and **Agent** as the *Security Profiles*. When finished, save the user by selecting **Save**:

![CreateAgent1](/images/enable-aws-sso/_agent1_creation_connect.png)

On the following screen, just select **Create users**:

![FinishConnectCreateUsers](/images/enable-aws-sso/_finish_connect_create_users.png)

Now that we have the *agent1* already created in the Amazon Connect instance, it is time to provision them in AWS SSO. To do so, access the [AWS SSO console](https://console.aws.amazon.com/singlesignon/home#/users) and from the *Users* menu select **Add User**. Then, add information about the new user. Make sure that you are using the **same email address that you used when creating the user in the Amazon Connect instance**. 

{{% notice info %}}
By default, when creating a new user in SSO, the Amazon SSO Service will send an email to the user's email address with login information and asking for a new password. Given that in this workshop we are not using a valid domain name, make sure you are selecting the option **Generate a one-time password that you can share with the user** before creating the user. 
{{% /notice %}}

![AddSsoAgent1](/images/enable-aws-sso/_add_sso_agent1.png)

After filling all the fields, select **Next: Groups** on the bottom of the page. To make our life easier, let's go ahead and create a new group that will allow us to assign the users with the proper permissions on our Amazon Connect instance. To do so, choose **Create group** and type **ConnectAgents** as the **Group name**. Add a description, and select **Create**:

![SsoCreateAgentsGroup](/images/enable-aws-sso/_sso_create_agent_group.png)

The user will be created and you will be able to obtain the generated password by selecting the **Show password** option. Make sure you copy this field, because it will be used when trying to login via the SSO configuration:

![AgentUserCreated](/images/enable-aws-sso/_agent_user_created.png)


After creating the user and the group, you should return to the Amazon Connect application created in the SSO and allow access to it. To do so, choose the [Applications menu](https://console.aws.amazon.com/singlesignon/home#/applications) on the SSO page and select the *Amazon Connect* application. There, navigate to the **Assigned users** tab and choose **Assign users**.

Now, select the *Groups* tab, select the *ConnectAgents* group and choose **Assign users**:

![AssignUsers](/images/enable-aws-sso/assign_users.png)

By selecting the group there, it will be easier for you to add more agents in your Connect instance in the future, so you don't need to assign every individual user to the Amazon Connect application created in AWS SSO.


Repeat this process in both Amazon Connect instance and AWS SSO for each user.

All configured users should be able to authenticate via the AWS SSO portal. To get the login URL, please go to the [AWS SSO](https://console.aws.amazon.com/singlesignon/home) console. You will find the SSO portal URL under *User portal*.

Note that during the first login, a password change will be asked. After changing the password and logging in the system, the agents will be able to see the **Amazon Connect** application.

Once you select the Amazon Connect application, you will be redirected to the Amazon Connect agent interface and will be able to start accepting calls.