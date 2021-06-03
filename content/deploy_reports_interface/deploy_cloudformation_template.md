+++
title = "Deploy the CloudFormation Template"
weight = 51
+++

The first thing we are going to do is to deploy a CloudFormation template that will create all the basic resources that you will need to have the reporting platform. It will create a static website hosted in a S3 bucket, a Cognito UserPool that will be used for authentication, the DynamoDB tables, Lambda functions and API Gateways used to access the data and some additional resources needed.

The CloudFormation template is available in [this link](/files/metricswebsiteCFN.yaml). Make sure that you download it to your computer and then access the [CloudFormation console](https://console.aws.amazon.com/cloudformation/home). In this screen, on the right top corner, click in **Create Stack** and make sure you select the option **With new resources (standard)**:


![CreateNewStack](/images/deploy-reports-interface/deploy_cfn.png)

{{% notice info %}}
If don't see the **Create stack** button on the top right corner of the screen, you can extend the menu on the left side and click in **Stacks**. It will present all of your stacks and the option **create stack** will be on this screen.
{{% /notice %}}

In this screen, makw sure you keep all the sections as default, pick the option **Upload a template file** and select the *metricswebsiteCFN.yaml* file that you just downloaded. After this, click in **Next**:

![SelectTemplate](/images/deploy-reports-interface/select_template.png)

Now, name you Stack as **AmazonConnectReporting** and make sure that you enter a valid S3 Bucket name. Please note that S3 bucket names should be unique within the entire AWS ecosystem, so you can use something like **<your-company-name>-connect-reporting-website**. In this screen you will also need the Amazon Connect instance ID. You can get the Amazon Connect instance ID from the [Amazon Connect console](https://console.aws.amazon.com/connect) by clicking in your Instance Alias. In the instance Alias screen you will se the **Instance ARN** field. The last part of if represents the Amazon Connect instance ARN:

![ConnectInstanceId](/images/deploy-reports-interface/connect_instance_id.png)

In my case, the instance ID is *a59181b1-0371-4928-b6c3-50b2ef9b125a*. Make sure you are getting the right instance ID and adding it to the CloudFormation Parameters screen. Once you have all information, click in **Next**:

![CloudFormationParametersScreen](/images/deploy-reports-interface/cfn_parameters_screen.png)


In the following screen, just click **Next** and on the **Review** page, make sure that you are selecting the **I acknowledge that AWS CloudFormation might create IAM resources.** checkbox before clicking in **Create stack**:

![AckIamRoles](/images/deploy-reports-interface/ack_iam_roles.png)

You will see a notice saying that the stack was succesfully create when the CloudFormation deployment finishes:

![CreateComplete](/images/deploy-reports-interface/create_complete.png)
