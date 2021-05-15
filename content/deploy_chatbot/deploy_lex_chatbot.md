+++
title = "Deploy the Lex Chatbot"
weight = 20
+++


After deploying the infrastructure with Lambda Functions and DynamoDB tables that will be used by the chatbot, it is time to deploy the chatbot itself. Start by downloading the zip file from [this link](/files/CableTvLexChatbot.zip).

After downlinad the file, navigate to the [Amazon Lex console](https://console.aws.amazon.com/lex/home) and on this screen, click in **Actions** and than in **Import**:

![ImportChatbot](/images/deploy-lex-chatbot/actions_import.png)

Here, select the *CableTvLexChatbot.zip* file and click in **Import**:

![ImportBot](/images/deploy-lex-chatbot/import_bot.png)

After importing the Lex chatbot, we will need to change a few configurations and point it to use the Lambda functions that we just deployed. To do so, click in the chatbot *CableTvSupport*: 

![ClickChatbot](/images/deploy-lex-chatbot/click_chatbot.png)

On the **Editor** tab, click in the **ManageSchedule** intent and under **Fullfilment** select **AWS Lambda function** and finally pick the function named **CableTv-ManageTechVisitSchedule**. When selecting the function, there will be a new window saying that you are about to provide permissions so the chatbot will be able to call the function on your behalf. Just click **OK**. After picking the right function, go ahead, and click in **Save intent**:

![CableTvSchedule](/images/deploy-lex-chatbot/manage_schedule_function.png)

After picking the Lambda Function for the **ManageSchedule** intent, let's do the same for the **SignalLost** and the **VisitSchedule** intents. Make sure you're picking the following:

- **SignalLost** intent: select the **CableTv-ValidateCustomerId** function
- **VisitSchedule** intent: select the **CableTv-ScheduleTechVisit** function

{{% notice info %}}
Make sure you click on the **Save Intent** button after picking the Lambda function for each intent.
{{% /notice %}}



After picking the three functions, it is time for us to build and publish our chatbot. Start by clicking in the button **Build** on the top right corner of the screen. A message will be presented saying that you can continue editing your bot while the build process is in progress. You can just click on **Build**.

After finishing your build process, it is time for you to click in the **Publish** button. When doing it, you will be asked to create an alias. Typo **demo_environment** and click in the **Publish** button. When the publish process is finished, you can just click in **Close** and start testing your environment:

![PublishedBot](/images/deploy-lex-chatbot/published_bot.png)
