+++
title = "Configure Agent Events Stream"
weight = 53
+++

Now that we have the web application properly deployed, it is time to configure the Agent Event streams so the Lambda Function can start pulling out this information and updating the database that is accessed by the web application.

To do so, the first thing to do is creating an Amazon Kinesis stream. Go to the [Amazon Kinesis console](https://console.aws.amazon.com/kinesis/home) and on this screen, make sure that the **Kinesis Data Streams** is selected and click in **Create data stream**:

![CreateDataStream](/images/deploy-reports-interface/create_data_stream.png)

Name your Data Stream as **ConnectAgentsData** and put the number of open shards 1. After this, click in **Create data stream**:

![DataStreamConfig](/images/deploy-reports-interface/data_stream_config.png)

After creating the Data Stream, we have to enable the data streaming capabilities in the Amazon Connect instance. To do so, on the [Amazon Connect console](https://console.aws.amazon.com/connect/home), click in you connect instance alias and under **Data streaming** select **Enable data streaming** and under **Agent Events** pick the kinesis stream that you just created and click in **Save**:

![ConfigureAgentEventsStream](/images/deploy-reports-interface/configure_agent_event_stream.png)

Now, we have to update the Lambda Function that will grab the information from the Kinesis stream and populate the database. To do so, access the [AWS Lambda console](https://console.aws.amazon.com/lambda/home) and look for a Lambda function that starts with **AmazonConnectReporting-AgentEventStreamToDDB**. Click on the function and on the **Function overview** section, select the **+ Add trigger** buttom:

![AddTrigger](/images/deploy-reports-interface/add_trigger.png)

In the next screen, select **Kinesis**, pick the Kinesis stream that we just created, named **ConnectAgentsData** and click in **Add**:

![AddTrigger](/images/deploy-reports-interface/configure_trigger.png)

Note that it might take a couple of minutes to get your trigger properly created. You will be able to see the streams status on the Lambda configuration page. When the streams changes to **Enabled** it means that the configuration is finished:

![LambdaTriggerStatus](/images/deploy-reports-interface/trigger_status.png)
