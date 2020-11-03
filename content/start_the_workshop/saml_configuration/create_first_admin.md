+++
title = "Create the first Connect Admin"
weight = 25
+++

Now that you already have the SSO Application for the admin user, let's go ahead and create the first admin user that we will be using during the workshop. Access your Amazon Connect instance using the link available in the [Amazon Connect console](https://console.aws.amazon.com/connect/home).

{{% notice info %}}
In case you're not able to login with the first user, because you have enabled the SSO, you can click in your connect instance name and use the **Emergency access** link. This will provide you admin access to your Amazon Connect instance with an Admin profile. Please note that we don't recommend you to use this link in your day-to-day operations.
{{% /notice %}}

After logging in 

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