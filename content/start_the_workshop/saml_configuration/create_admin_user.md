+++
title = "Create the Amazon Connect Admin user"
weight = 25
+++

Now that the Admin User application has been created, let's configure the admin users for this workshop. Access your Amazon Connect instance using the link available in the [Amazon Connect console](https://console.aws.amazon.com/connect/home).

After logging in, choose **User management** menu on the left side and then select **Add new users**. Proceed to create a new user and use **Admin** for the first name, **User** for the last name and **admin-user@amazon-connect-workshop.com** as the login name.

Make sure you select **Basic Routing Profile** as the Routing Profile and **Admin** as the Security Profile:

![CreateAdminUser](/images/enable-aws-sso/create_connect_admin_user.png)

Select **Save** then choose **Create users**.

After creating the admin user in Amazon Connect, return to the [AWS SSO](https://console.aws.amazon.com/singlesignon/home) page and can provision the user there. 

Start by creating a group named **ConnectAdmins**. On the SSO page, select **Groups** and choose **Create group**:

![CreateAdminGroup](/images/enable-aws-sso/create_admin_group.png)

In the next screen, name your group **ConnectAdmins**, add a description and select **Create**:

![AdminGroupDetails](/images/enable-aws-sso/admin_group_details.png)

Now, return to the SSO Users screen and create a new user. Make sure you are using the same email address that you have used when creating your user in Amazon Connect and to select the **Generate a one-time password that you can share with the user** option.

![AdminUserDetails](/images/enable-aws-sso/admin_user_details.png)

You can then assign the admin user to the Admin group and then select **Add user**:

![AdminUserGroup](/images/enable-aws-sso/admin_user_group.png)

Make sure you store the user password for the admin user.

After creating the user and group, it is time to assign the group to the Amazon Connect admin application. Select **Applications** and then choose the **Amazon Connect - Admin application**. Select the **Assigned users** tab and choose **Assign users**:

![AssignAdminGroup](/images/enable-aws-sso/assign_admin_group.png)

On the next screen, select the **Groups** tab and then select the **ConnectAdmins** group. Once selected, choose **Assign users**. When logged in as an admin user,  the Amazon Connect admin application should be available:

![ConnectAdminApp](/images/enable-aws-sso/connect_admin_app.png)

