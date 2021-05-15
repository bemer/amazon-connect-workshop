+++
title = "Testing the Lex Chatbot"
weight = 30
+++


Now that you have deployed the chatbot, it is time to test it. The first thing we will need is to add some customer data in the **CableTvCustomers** DynamoDB table. To do so, go to the [DynamoDB console](https://console.aws.amazon.com/dynamodbv2) and click in the **CableTvCustomers** table. On the table page, click in the **Create Item** button:

![CreateItem](/images/test-chatbot/create_ddb_item.png)

On the *Create Item* page, insert the following JSON document (remember to replace the data with your name and your phone number):

    {
    "customerId": "1235",
    "CustomerPhone": "+551196540004",
    "CustomerSince": "2019-02-01",
    "TvPlan": "Gold",
    "CustomerName": "Bruno Emer"
    }

And click in **Create Item**:

![DdbItem](/images/test-chatbot/ddb_item.png)

After creating the Item on the DDB table, get back to the [Amazon Lex console](https://console.aws.amazon.com/lex) amd click in the **Test Chatbot** option, located on the right side of the screen:

![TestChatbot](/images/test-chatbot/test_button.png)

After scheduling a new technical visit, take a look in your cellphone. If everything went well, you should have received an SMS text telling you about the technical visit.

In the test window, you can start a conversation with your chatbot. You can use the following script to test it out:

![ChatbotDialog1](/images/test-chatbot/chatbot_dialog_1.png)

Now, you can check if your technical visit was properly schedule, so follow the next script:

![ValidateSchedule](/images/test-chatbot/validate_schedule.png)

And if you want, feel free to reschedule or cancel it:

![ValidateSchedule](/images/test-chatbot/reschedule_visit.png)

Now that we have the chatbot properly deployed, it is time to move forward and configure the Amazon Connect instance, so your clients will be able to interact with the Chatbot using voice.

