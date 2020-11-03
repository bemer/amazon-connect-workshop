+++
title = "Setup Contact Routing in Amazon Connect"
weight = 31
+++


In this module we are going to setup Contact Routing in Amazon Connect. Amazon Connect uses Queues, Routing Profiles, and, Contact Flows to route contacts to Agents. We are going to build 3 Queues and 3 Routing Profiles to simulate a companies Contact Center.

- Sales
- Service
- Parts

Open the AWS Console and type Connect in the Find Services search box. Select the Amazon Connect Service.

![SetupRouting](/images/setup-contact-routing/open-console.png)

Select the Instance Access URL to bring up the Amazon Connect Login URL.

![SetupRouting](/images/setup-contact-routing/instance-login-url.png)

Enter your username and password for the Instance.

![SetupRouting](/images/setup-contact-routing/connect-login.png)

Once you are logged into the Connect Console navigate to the **Routing Menu** on the left hand side of the console. Select **Queues** in the Routing Menu

![SetupRouting](/images/setup-contact-routing/connect-routing-menu.png)

This will bring you to the Queues List and you will see that there is a Basic Queue in the list. This is a default queue that is created when the Instance is created. We will create 3 additional Queues for Sales, Service, and Parts. When creating a queue you will need to define some basic parameters for the queue. Select the **Add new Queue** button to begin adding the queues.

![SetupRouting](/images/setup-contact-routing/create-new-queue.png)

In the new Queue creation screen we will define the parameters for the Queue

- Name
- Description
- Hours of Operation
- Outbound Caller ID Name
- Outbound Caller ID Number
- Outbound Whisper Flow

Type in **Sales** for the name of the queue and **Sales Department** for the description. For Hours of Operations select **Basic Hours** from the drop down. **Basic Hours** is a default Hours of Operations table that is built when the Instance is deployed. 

Type in **Sales** for the **Outbound Caller ID Name** and select the **Phone Number** claimed in the Instance setup portion of the workshop.

Select **Default Outbound** for the **Outbound Whisper Flow** this flow is the default Outbound Whisper flow that is created when the Instance is built.

![SetupRouting](/images/setup-contact-routing/sales-queue-setup.png)

Repeat the above steps for the **Service** and **Parts** queues.

{{% notice tip %}}
**Avoid Blank, Spam, or Telemarketer Labels.**
Amazon Connect has contracted with a leading provider of CNAM services for US numbers to provide Calling Name to the extent possible. This enables outbound calls that show the enrolled Calling Line Identity (CLI) to generally avoid reputation-sensitive labels like "spam" or "telemarketer."
To enroll your numbers with this CNAM services provider, open a Support ticket. Our Support team will gather the required information to enroll your numbers.
Only numbers in the 50 US states, Puerto Rico, and Virgin Islands are eligible.
{{% /notice %}}

Now you should have 3 queues created and the list of queues should look like this.

![SetupRouting](/images/setup-contact-routing/queue-list.png)

With the appropriate queues created we now need to create **Routing Profiles** that will be assigned to agents to staff the configured queues. While queues are a 'waiting area' for contacts, a routing profile links queues to agents. When you create a routing profile, you specify which queues will be in it. You can also specify whether one queue should be prioritized over another.

{{% notice tip %}}
Each agent is assigned to one routing profile.
{{% /notice %}}  
Select the **Users** menu on the left of the Connect Console and then select **Routing Profiles**

![SetupRouting](/images/setup-contact-routing/select-routing-profiles.png)

You will see the list of **Routing Profiles** in the Instance. Notice there is a Basic Routing Profile. This is the default Routing Profile that is created when the Connect Instance is created. 

We are going to create 3 Routing Profiles for our different agent types. We will create a **Sales** Routing Profile that will include all 3 queues we created, but we will set **Priority** on the **Sales Queue**. This is because we want Sales agents to focus primarily on Sales Calls. We will give the **Parts** queue the second priority and the **Service Queue** the third priority. 

Click **Add New Profile** to add a new Routing Profile.

![SetupRouting](/images/setup-contact-routing/add-new-routing-profile.png)

Enter the name **Sales** for the name of the Routing Profile and enter the description **Sales Department**. For Channels enable Voice and Chat. Set the maximum number of Chats per agent to 3.




![SetupRouting](/images/setup-contact-routing/sales-routing-profile-1.png)

{{% notice tip %}}
The maximum number of Chats allowed per agent is **5**. This limit cannot be increased.
{{% /notice %}}

Now add the **Sales** Queue to the Routing Profile by selecting the queue from the drop down menu. Select **Voice** and **Chat** for channels and leave the **Priority** as 1. Then click the **Add Queue** Button. 

Next add the **Parts** Queue to the Routing Profile by selecting the queue from the drop down menu. Select **Voice** and **Chat** for channels and change the **Priority** to 2.

Next add the **Service** Queue to the Routing Profile by selecting the queue from the drop down menu. Select **Voice** and **Chat** for channels and change the **Priority** to 3.

For the **Outbound Queue** select the **Sales Queue**. When an outbound call is placed by an agent, it must be associated with a queue.

You have configured the **Routing Profile** with **Queues** and the queues have a **Priority** that will allow **Sales** calls to take top priority over **Parts**  and **Service** calls.

**Sales** and **Parts** to take **Priority** over **Service Calls**

Setting the **Priority** allows the **Sales** team to focus on sales calls, but still take parts or service calls if no agents are available and calls are in queue.

Your **Routing Profile** should looke like this.

![SetupRouting](/images/setup-contact-routing/sales-routing-profile-2.png)

Click the **Add New Profile** Button at the top of the add routing profile page.

![SetupRouting](/images/setup-contact-routing/sales-routing-profile-3.png)

Now we need to add the 2 other **Routing Profiles** to complete the routing profiles for our Contact Center.

For **Service** create a new Routing Profile following the same steps as above, but change the **Queue** order and **Priority**.

- Queue         Priority
- Service        1
- Parts          2
- Sales          3

This is how your queues and priorities should be set.

![SetupRouting](/images/setup-contact-routing/service-routing-profile-1.png)

For **Parts** create a new Routing Profile following the same steps as above, but change the **Queue** order and **Priority**.

- Queue         Priority
- Parts          1
- Service        2
- Sales          3

This is how your queues and priorities should be set.

![SetupRouting](/images/setup-contact-routing/parts-routing-profile-1.png)

This completes the **Routing Profile** setup. Next we will configure **Agents** and assign the **Routing Profiles** to agents.



![SetupRouting](/images/setup-contact-routing/complete-routing-profile.png)

{{% notice tip %}}
The Connect Admin guide is a useful resource that can help you through out the workshop. [Official Documentation](https://docs.aws.amazon.com/connect/latest/adminguide/amazon-connect-get-started.html).
{{% /notice %}}

