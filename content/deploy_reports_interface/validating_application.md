+++
title = "Validating the application"
weight = 55
+++

Now that we have completed all the pre-requisites to get the reporting platform working, it is time to valide it's functionality.

To do so, access the reporting platform web interface, using the CloudFront URL (don't forget to add the */metrics/metrics.html* in the end). You will be prompted with a username an password screen. On that, use the following data:

    usernamme: sjobs
    password: password

After logging in the application, you will be able to see data about your queue and your agents. Try changing the agent status and placing a few calls that will be directed to the queue and you should see everything on this screen:


![QueueReport](/images/deploy-reports-interface/queue_report.png)

![AgentReport](/images/deploy-reports-interface/agent_report.png)
