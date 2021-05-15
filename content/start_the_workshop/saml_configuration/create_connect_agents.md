+++
title = "Create Connect agents"
weight = 23
+++

After configuring the SSO, it is time to go ahead and create the firt Amazon Connect agents. With the SSO setup, users are created and defined in the Connect instance but all the password management will happen through the SSO. Let's then create a few Connect users and see how this integration looks like.

The first step here is to access your Amazon Connect instance with your administrator account (that we created in the previous lab) and create a new user. To do so, visit the [Amazon Connect console](https://console.aws.amazon.com/connect/home) and click in the *Access URL*. You will be taken to the Amazon Connect management portal. In this dashboard, click in the *User management* menu in the left side:

![ConnectUserManagement](/images/enable-aws-sso/_user_management.png)

In the new screen, click in **Add new users** buton in the top right corner:

![AddNewUsers](/images/enable-aws-sso/_add_new_users.png)

There are mainly two options to create users in the Amazon Connect instance: manually and upload a template with multiple users. For our workshop purposes, we are going to create two different agents, named **agent1** and **agent2**, so go ahead in click in the  In the **Add new users** button on the top right corner of the **User management** screen, make sure that the option **Create and set up a new user.** is selected and click in **Next**:

![CreateSetupUser](/images/enable-aws-sso/_create_setup_user.png)


Enter **Agent** for the First Name and **1** for the last name. Enter **agent1@connect-workshop.com** for the Login Name. After adding this information, select the **Basic Routing Profile** as the *Routing Profile* and **Agent** as the *Security Profiles*. When finishing it, click in the **Save** button on the bottom of the page:

![CreateAgent1](/images/enable-aws-sso/_agent1_creation_connect.png)

On the following scree, just click in the **Create users** button:

![FinishConnectCreateUsers](/images/enable-aws-sso/_finish_connect_create_users.png)

Now that we have the *agent1* already created in the Amazon Connect instance, it is time to provision it in the SSO. To do so, access the [AWS SSO console](https://console.aws.amazon.com/singlesignon/home#/users) and under the *Users* menu click in the **Add User** button. Then, add information about the new user. Make sure that you are using the **same email address that you used when creating the user in the Connect instance**. 

{{% notice info %}}
By default, when creating a new user in SSO, the Amazon SSO Service will send an email to the user's email address with login information and asking for a new password. Given that in this workshop we are not using a valid domain name, make sure you are selecting the option **Generate a one-time password that you can share with the user** before creating the user. 
{{% /notice %}}

![AddSsoAgent1](/images/enable-aws-sso/_add_sso_agent1.png)

After filling all the fields, click in the button **Next: Groups** on the bottom of the page. To make our life easier, let's go ahead and create a new group that will allow us to assign the users with the proper permissions on our Amazon Connect instance. To do so, click in the **Create group** button and type **ConnectAgents** as the **Group name**. Add a description about it, and click in **Create**:

![SsoCreateAgentsGroup](/images/enable-aws-sso/_sso_create_agent_group.png)

The user will be created and you will be able to obtain the generated password by clicking in the **Show password** option. Make sure you copy this field, because it will be used when trying to login via the SSO configuration:

![AgentUserCreated](/images/enable-aws-sso/_agent_user_created.png)


After creating the user and the group, you should get back to the Connect application created in the SSO and allow access to it. To do so, click in the [Applications menu](https://console.aws.amazon.com/singlesignon/home#/applications) on the SSO page and click in the *Amazon Connect* application. There, navigate to the **Assigned users** tab and click in the button **Assign users**:

![AssignSsoUsers](/images/enable-aws-sso/assign_sso_users.png)

Now, select the *Groups* tab, select the *ConnectAgents* group and click in the button **Assign users**:

![AssignUsers](/images/enable-aws-sso/_assign_users.png)

By selecting the group there, it will be easier for you to add more agents in your Connect instance in the future, so you don't need to assign every individual user to the Connect application created on the AWS SSO.


Repeat the steps to as many users you want in both the Amazon Connect instance and the SSO.

After creating the users, you should be able to access the SSO interface with them. To get the login URL, please go to the [AWS SSO](https://console.aws.amazon.com/singlesignon/home) console. You will find the SSO portal URL under *User portal*.

Note that during the first login, a password change will be asked. After changing the password and logging in the system, the agents will be able to see the **Amazon Connect** application:

![ConnectSsoApplication](/images/enable-aws-sso/connect_sso_application.png)

When clicking in the Connect application, you will be redirected to the Connect agent interface and will be able to start receiving and answering calls.