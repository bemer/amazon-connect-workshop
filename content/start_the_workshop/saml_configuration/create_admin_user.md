+++
title = "Create the Connect Admin"
weight = 25
+++

No that you already have the SSO Application for the admin user, let's go ahead and create the first admin user that we will be using during the workshop. Access your Amazon Connect instance using the link available in the [Amazon Connect console](https://console.aws.amazon.com/connect/home).

{{% notice info %}}
In case you're not able to login with the first user, because you have enabled the SSO, you can click in your connect instance name and use the **Emergency access** link. This will provide you admin access to your Amazon Connect instance with an Admin profile. Please note that we don't recommend you to use this link in your day-to-day operations.
{{% /notice %}}

After logging in, click in the **User management** menu on the left side and then click in the **Add new users** button. Proceed to create a new user and use **Admin** for the first name, **User** for the last name and **admin-user@amazon-connect-workshop.com** as the login name.

Make sure you select **Basic Routing Profile** as the Routing Profile and **Admin** as the Security Profile:

![CreateAdminUser](/images/enable-aws-sso/create_connect_admin_user.png)

Click in **Save** and then in the **Create users** button.

After creating the admin user in Connect, get back to the [AWS SSO](https://console.aws.amazon.com/singlesignon/home) page so we can provision the user there as well. 

Start by creating a group named **ConnectAdmins**. To do so, in the SSO page, click in **Groups** in the left menu and then click in **Create group**:

![CreateAdminGroup](/images/enable-aws-sso/create_admin_group.png)

In the next screen, name your group **ConnectAdmins**, add a description and click in **Create**:

![AdminGroupDetails](/images/enable-aws-sso/admin_group_details.png)

Now, get back to the SSO Users screen and create a new user. Make sure you are using the same email address that you have used when creating your user in Amazon Connect and to select the **Generate a one-time password that you can share with the user** option.

![AdminUserDetails](/images/enable-aws-sso/admin_user_details.png)

You can then assign the admin user to the Admin group and then click in **Add user**:

![AdminUserGroup](/images/enable-aws-sso/admin_user_group.png)

Make sure you store the user password for the admin user.

After creating the user and group, it is time to assign the group to the Amazon Connect admin application. To do so, click in the **Applications** menu on the left page of the SSO screen and then click in the **Amazon Connect - Admin** application. There, click in the tab **Assigned users** and then in the button **Assign users**:

![AssignAdminGroup](/images/enable-aws-sso/assign_admin_group.png)

In the next screen, click in the tab **Groups** and then select the **ConnectAdmins** group. After selecting it, click in the **Assign users** button. When logging with the admin user in the SSO URL, you should be able to see the Amazon Connect admin application:

![ConnectAdminApp](/images/enable-aws-sso/connect_admin_app.png)

