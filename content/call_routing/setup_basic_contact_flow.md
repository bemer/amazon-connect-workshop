+++
title = "Setup Basic Contact Flow"
weight = 33
+++


In this module we are going to setup an Amazon Connect Contact Flow to greet our customers and route them to the appropriate department.

- Sales
- Service
- Parts

Open the AWS Console and type Connect in the Find Services search box. Select the Amazon Connect Service.

![SetupBasicContactFlow](/images/setup-contact-routing/open-console.png)

Select the Instance Access URL to bring up the Amazon Connect Login URL.

![SetupBasicContactFlow](/images/setup-contact-routing/instance-login-url.png)

Enter your username and password for the Instance.

![SetupBasicContactFlow](/images/setup-contact-routing/connect-login.png)

Once you are logged into the Connect Console navigate to the **Routing** menu on the left hand side of the console. Select **Contact Flows** in the Routing Menu

![SetupBasicContactFlow](/images/setup-basic-contact-flow/contact-flow-menu.png)

This will bring you to the **Contact Flow** page and show a list of **Default** and **Sample** flows. These flows are used for the default experience when calling into your Amazon Connect Instance. The Sample call flows provide customers with examples of how to build certain contact flows.

![SetupBasicContactFlow](/images/setup-basic-contact-flow/default-sample-contact-flows.png)

Take some time to review the **Default** and **Sample** flows to understand how **Contact Flows** are constructed. Search for **Sample Inbound Flow** to filter the list of Contact Flows.

![SetupBasicContactFlow](/images/setup-basic-contact-flow/sample-inbound-flow.png)

Select the **Name** of the Contact Flow to open the Contact Flow in the Contact Flow Editor.

The following screen shows the **Contact Flow Editor**

![SetupBasicContactFlow](/images/setup-basic-contact-flow/sample-inbound-flow.png)

Key elements in the **Contact Flow Editor** include:

- Menu For Contact Flow Blocks
- Publish and Save Buttons
- Zoom Controls

Menu for Contact Flow Blocks

![SetupBasicContactFlow](/images/setup-basic-contact-flow/contact-flow-block-menu.png)

Use the **Drop Down** arrows to open the different menu sections and drag and drop the **Contact Blocks** onto the canvas.

Publish and Save Buttons

The **Publish** button allows you to publish a Contact Flow

Zoom Controls

![SetupBasicContactFlow](/images/setup-basic-contact-flow/contact-flow-block-zoom.png)

Use the **Zoom** Controls to zoom in and out on the canvas. This allows you to navigate large contact flows.



{{% notice tip %}}
The Connect Admin guide is a useful resource that can help you through out the workshop. [Official Documentation](https://docs.aws.amazon.com/connect/latest/adminguide/amazon-connect-get-started.html).
{{% /notice %}}


