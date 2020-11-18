+++
title = "Setup Agents"
weight = 32
+++


Now that our agents are already created and we also have the Queues and Routing Proflies in place, it is time to assign these Routing Profiles to the agents. To do so, in your Amazon Connect admin interface, click in the **User management** menu to see all the agents. In this screen, start selecting the **sales-user** and then click in the **Edit** button:

![SelectUser](/images/setup-agents/select_user.png)

In the next screen, change the Routing Profile from *Basic Routing Profile* to *Sales* and click in **Save**:

![ChangeRoutingProfile](/images/setup-agents/change_routing_profile.png)

Repeat this step for the Parts and Service users, making sure to assign the right user profile to each of them. Once you complete this step for the three users, your list will look like this:

![UsersList](/images/setup-agents/users_list.png)

Now that we have our **Routing Profiles** and **Agents** setup we can create a **Contact Flow** to route contacts to our agents. Continue with the next module to setup a basic Contact Flow.

