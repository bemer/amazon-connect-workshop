+++
title = "Configure the Amazon Connect instance"
weight = 10
+++


In order to be able to connect the Amazon Connect instance with the Amazon Lex chatbot, the first step is for you to  add the Lex bot in the Contact Flows configuration of your Connect Instance. This step basically provides the right permissions so the Connect instance can interact with the Lex bot.

To do so, click in you Amazon Connect instance on the [Amazon Connect console](https://console.aws.amazon.com/connect) and there, navigate to the **Contact flows** on the left menu:

![ContactFlows](/images/integrate-with-lex/contact_flows.png)

In this screen, under **Amazon Lex**, select the bot named **CableTvSupport** that we just created and click in **+ Add Lex Bot**:

![AddLexBot](/images/integrate-with-lex/add_lex_bot.png)

You will see a message saying that the Lex Bot was succesfully added and it will be listed under the **Lex bots** list:

![LexBotAdded](/images/integrate-with-lex/added_lex_bot.png)

After doing this, you can go back to your Amazon Connect instance dashboard to configure the Call Flow that will redirect calls to the Lex bot.