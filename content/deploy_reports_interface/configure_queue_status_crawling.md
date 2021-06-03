+++
title = "Configure Queue Stats"
weight = 54
+++

The final step for us to have all the information being populated in the new interface is to configure the application so it can start obtaining information from the Amazon Connect queues. To do so, the first thing we need to do is to get the Queue ARN from the Amazon Connect instance.

Access you Amazon Connect instance and navigate to the **Queues** on the left side menu:

![AccessQueueMenu](/images/deploy-reports-interface/queue_menu.png)

There, click in the Queue that you want to get metrics. In this case, we are going to proceed with the **Basic Queue**. Expand the **Show additional queue information** and copy the ARN from there:

![GetAdditionalQueueInformation](/images/deploy-reports-interface/get_queue_arn.png)

Now, with this information, go to the [DynamoDB console](https://console.aws.amazon.com/dynamodbv2/home). On the left hand menu, click in **Tables** and select the table **RealTimeQueueStats**. On the table page, click in the **View items** button:

![DDBQueueStatsTable](/images/deploy-reports-interface/queue_stats_table.png)

On the **Items** page, click in the **Create item** button and on the following screen, you should add the following JSON object, replacing the **<QUEUE_ARN>** with the ARN that we just got from your queue. After adding the JSON file, you can go ahead and click in the **Create item** button:

    {
        "queue": "<QUEUE_ARN>",
        "queueName": "Basic Queue"
    }

![CreateItem](/images/deploy-reports-interface/create_item.png)
