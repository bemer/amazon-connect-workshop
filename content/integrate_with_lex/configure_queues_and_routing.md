+++
title = "Configure Queues and Routing Profiles"
weight = 20
+++


The next step after adding the Lex bot to the Amazon Connect instance is to configure the *Queues* and the *Routing Profile* so the agent previously created will be able to receive calls and chat messages.

Let's start by creating two different queues: **CheckSchedule** and **TvSignalProblem**. To do so, on the left menu click on **Queues** under the **Routing** menu:

![AddLexBot](/images/configure-queues-and-routing/queues_menu.png)

On the queues screen, click in **Add new queue** button on the top right corner of the screen. For the name, type **CheckSchedule**, add a description, select **Basic Hours** under *Hours of operation* and pick the *Outbound caller ID number*. When finishing, click in **Add new queue** button:

![AddCheckScheduleQueue](/images/configure-queues-and-routing/add_checkschedule_queue.png)

After adding the **CheckSchedule** queue, click in the **Add new queue button** and execute the same steps to create the **TvSignalProblem** queue.

When both queues are created, it is time to create the **Routing Profile**. Click in the **Routing profiles** menu under *Routing* and then on the button **Add new profile**. On the *Add new routing profile* screen, name it **CableTvSupport**, add a description and make sure you add both the *TvSignalProblem* and the *CheckSchedule* queue. Also, pick the *TvSignalProblem* as the *Default outbound queue*. When finishing, click in the **Add new profile** buttom on the top right corner:

![AddRoutingProfile](/images/configure-queues-and-routing/add_routing_profile.png)

Now that the queues and the routing profile are created, let's get back and assign it to the *agent1* user so it will be able to receive calls and chat interactions. To do so, go back to the *User management* screen, select the *agent1* user and click in **Edit** on the top right corner. Replace the *Basic Routing Profile* with the **CableTvSupport** that you just created and click in **Save**:

![ReplaceRoutingProfile](/images/configure-queues-and-routing/replace_routing_profile.png)

{{% notice info %}}
If you have created more agents in the [Create Connect Agents](/start_the_workshop/saml_configuration/create_connect_agents/) chapter, make sure you replace the routing profile in all of them, otherwise they won't be receiving any calls or chat interactions.
{{% /notice %}}


Now that your routing configurations are in place, you can go ahead and create the proper call flows that will send calls to the Lex bot and to the agent.