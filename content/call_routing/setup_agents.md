+++
title = "Setup Agents"
weight = 32
+++


In this module we are going to setup Amazon Connect Agents. We are going to create 3 agents, one to work in each department.

- Sales
- Service
- Parts

Open the AWS Console and type Connect in the Find Services search box. Select the Amazon Connect Service.

![SteupAgents](/images/setup-contact-routing/open-console.png)

Select the Instance Access URL to bring up the Amazon Connect Login URL.

![SteupAgents](/images/setup-contact-routing/instance-login-url.png)

Enter your username and password for the Instance.

![SteupAgents](/images/setup-contact-routing/connect-login.png)

Once you are logged into the Connect Console navigate to the **Users** menu on the left hand side of the console. Select **User Management** in the Users Menu

![SetupAgents](/images/setup-agents/users-user-management-menu.png)

This will bring you to the User Management Page. From here select the **Add New Users** button to being setting up your agents.

![SetupAgents](/images/setup-agents/add-new-users.png)

This will open the Add New Users screen and you will have two options for adding users. The default option is to Create and Setup users manually. You can also select the Upload users from a csv. For this part of the workshop we are going to add users manually. 

{{% notice tip %}}
Along with adding users manually and uploading CSV files for creating users there is an API avaialble for adding users. The API allows customer to integrate user management in Amazon Connect with other Identity Management Systems and Automate the creation and deletion of users.  [API Reference](https://docs.aws.amazon.com/connect/latest/APIReference/API_CreateUser.html)
{{% /notice %}}

Select the **Next** Button to being creating your **Agents**

![SetupAgents](/images/setup-agents/users-user-management-next.png)

Enter **Sales** for the First Name and **User** for the last name. Enter **sales@aws-connect-workshop-123.com** for the Login Name. 

Select **Sales** for the Routing Profile.

Select **Agents** for the Security Profile.

Leave the rest of the options default. Your **Sales** user configuration should look like this.

![SetupAgents](/images/setup-agents/sales-user.png)

Click the **Save** Button to go to the **Verify User Details** Screen and then click the **Create Users** button. 

Now click the **Create More Users** button to create the next user.

Follow the steps above to create a **Service Agent** and a **Parts Agent**. Makw sure to assign the appropriate **Routing Profile** to each agent.

Once you complete the other 2 agents you user list should look like this.

![SetupAgents](/images/setup-agents/user-list.png)

Now that we have our **Routing Profiles** and **Agents** setup we can create a **Contact Flow** to route contacts to our agents. Continue with the next module to setup a basic Contact Flow.

{{% notice tip %}}
The Connect Admin guide is a useful resource that can help you through out the workshop. [Official Documentation](https://docs.aws.amazon.com/connect/latest/adminguide/amazon-connect-get-started.html).
{{% /notice %}}


