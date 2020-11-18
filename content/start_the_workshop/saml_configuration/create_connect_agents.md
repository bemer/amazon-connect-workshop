+++
title = "Create Connect agents"
weight = 23
+++

After configuring the SSO, it is time to go ahead and create the firt Amazon Connect agents. With the SSO setup, users are created and defined in the Connect instance but all the password management will happen through the SSO. Let's then create a few Connect users and see how this integration looks like.

The first step here is to access your Amazon Connect instance with your administrator account (that we created in the previous lab) and create a new user. To do so, visit the [Amazon Connect console](https://console.aws.amazon.com/connect/home) and click in the *Access URL*. You will be taken to the Amazon Connect management portal. In this dashboard, click in the *User management* menu in the left side:

![ConnectUserManagement](/images/enable-aws-sso/user_management.png)

In the new screen, click in **Add new users** buton in the top right corner:

![AddNewUsers](/images/enable-aws-sso/add_new_users.png)

There are mainly two options to create users in the Amazon Connect instance: manually and upload a template with multiple users. In our case, let's just create a single users that we will use for testing. In the *Add new users* screen, make sure that the option **Create and set up a new user.** is selected and click in **Next**.

Enter **Sales** for the First Name and **User** for the last name. Enter **sales@aws-connect-workshop.com** for the Login Name.

After filling the user information, select the **Routing profile** and for the security profile select **Agent**. After filling the user information, click in **Save**:

![AddUserInfo](/images/enable-aws-sso/add_user_information.png)


In the confirmation screen, click in the **Create users** button.

![CreateUser](/images/enable-aws-sso/create_user.png)

After creating the *Sales* user, click in the button **Create more users** and create two more users: one for the **Service**  and another one for the **Parts** departments.

Once you complete the other 2 agents you user list should look like this.

![UsersList](/images/enable-aws-sso/connect_users_list.png)


After creating the users in the Connect instance, it is time to provision them in the SSO. To do so, access the [AWS SSO console](https://console.aws.amazon.com/singlesignon/home#/users) and under the *Users* menu click in the **Add User** button. Then, add information about the new user. Make sure that you are using the **same email address that you used when creating the user in the Connect instance**. 

{{% notice info %}}
By default, when creating a new user in SSO, the Amazon SSO Service will send an email to the user's email address with login information and asking for a new password. Given that in this workshop we are not using a valid domain name, make sure you are selecting the option **Generate a one-time password that you can share with the user** before creating the user. 
{{% /notice %}}

After, click in the **Next: Groups** button:

![CreateSsoUser](/images/enable-aws-sso/create_sso_user.png)

To make our life easier, let's now create a group that will be used by all the Connect Agents. To do so, click in the **Create group** button in the top of the screen. Name your group *ConnectAgents* and click in the **Create button**. After creating the group, make sure you have it selected in the Groups screen before clicing in the **Add user** button.

When finishing the user creation, you will be able to get the user password from the screen. Please make sure you copy this information, so you can access the system with this user later:

![GetUserPassword](/images/enable-aws-sso/get_user_password.png)

After creating the user and the group, you should get back to the Connect application created in the SSO and allow access to it. To do so, click in the [Applications menu](https://console.aws.amazon.com/singlesignon/home#/applications) on the SSO page and click in the *Amazon Connect* application. There, navigate to the **Assigned users** tab and click in the button **Assign users**:

![AssignSsoUsers](/images/enable-aws-sso/assign_sso_users.png)

Now, select the *Groups* tab, select the *ConnectAgents* group and click in the button **Assign users**:

![AssignUsers](/images/enable-aws-sso/assign_users.png)

By selecting the group there, it will be easier for you to add more agents in your Connect instance in the future, so you don't need to assign every individual user to the Connect application created on the AWS SSO.


Repeat the steps to create both the **Parts** and the **Service** users in the SSO.

After creating the users, you should be able to access the SSO interface with them. To get the login URL, please go to the [AWS SSO](https://console.aws.amazon.com/singlesignon/home) console. You will find the SSO portal URL under *User portal*.

Note that during the first login, a password change will be asked. After changing the password and logging in the system, the agents will be able to see the **Amazon Connect** application:

![ConnectSsoApplication](/images/enable-aws-sso/connect_sso_application.png)

When clicking in the Connect application, you will be redirected to the Connect agent interface and will be able to start receiving and answering calls.