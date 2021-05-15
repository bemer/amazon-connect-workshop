+++
title = "Deploy the CloudFormation templates"
weight = 10
+++


In order to get the Lex Chatbot working properly, we have to deploy the appropriate Lambda Functions and DynamoDB tables. In this workshop we will simulate a Cable TV company that allows customers to call and talk about technical problems. After the customer start talking to the bot, there are a few different options available:

- If the customer has a problem with a single or a just a few channels, the call is transferred to an agent;
- If the customer has a problem with all the TV channels, the chatbot will schedule a technical visit;
- If the customer ask for information about the visit, the chatbot provides it;
- If the customer wants to cancel or reschedule the technical visit, the bot will do it.


Start downloading the zip file that contains the Lambda function code and the CloudFormation templates. You will find it in [this link](/files/cloudformation_template.zip).

After extracting the file locally, you will see two folder: one is named *code-s3* and another one named *Stack*. We will be using both of them. 


Now, access the [CloudFormation console](https://console.aws.amazon.com/cloudformation/home) and in this screen click in the **Create Stack** button on the right top corner, and select the option **With new resources**:

![DeployCfnStack](/images/deploy-cloudformation/create-cfn-stack.png)


You will have to deploy the stack named **CreateBucket.yaml**. To do so, select the option **Upload a template file** and select the file *CreateBucket.yaml* that is available on the *Stack* folder and click in **Next**:

![CreateBucketStack](/images/deploy-cloudformation/create_bucket_stack.png)

For the **Stack Name** enter **CableTv-Demo-Bucket-Stack** and click in **Next** again:

![S3BucketStackName](/images/deploy-cloudformation/s3_bucket_stack_name.png)

In the next screen, click in **Next** and then in **Create Stack**. You will see a stack being created. When the stack creation finishes, you will be able to see a bucket name in the **Outputs** session. Note that this is a ramdonly generated number. Take note of this name: 

![BucketNameOutput](/images/deploy-cloudformation/cfn_bucket_name_output.png)

After obtaining the bucket name, you should upload the Python scripts present on the **code-S3** folder to it. You can do it by using your terminal and the *awscli* or via the Amazon S3 console:

![CodeInS3](/images/deploy-cloudformation/code_in_s3.png)

Now, it is time for us to deploy the next CloudFormation template, that will deploy the Lambda Functions, DynamoDB Tables and IAM Roles needed for the environment. On the [CloudFormation console](https://console.aws.amazon.com/cloudformation/home), click again on **Create Stack**, select the option **With new resources**, pick the **Upload a template file** option again and this time, make sure you select the file named **CableTV-Infra.yaml** and click in **Next**:

![CableTvInfraStackCreation](/images/deploy-cloudformation/cable_tv_infra_stack.png)

For **Stack Name** type **CableTv-Demo-Infra-Stack** and for the **BucketName** add the name of the bucket that was created by the previous stack. In my case it was **cabletv-demo-bucket-stack-lambdazipsbucket-1gede3t0yoxvh*:

![InfraStackParameters](/images/deploy-cloudformation/infra_stack_parameters.png)

After filling these fields, click in **Next**, **Next** again and select the field under **Capabilities** that says *I acknowledge that AWS CloudFormation might create IAM resources with custom names.* before clicking in **Create stack**:

![IamAcknowledge](/images/deploy-cloudformation/iam_acknowledge.png)

It will take a couple of minutes for your stack to be created and when it is finished, you will be able to see all the resources that were created under the **Resources** tab on the CloudFormation console:

![CableTvStackResources](/images/deploy-cloudformation/cable_tv_stack_resources.png)


Now that you have the infrastructure created, you can go ahead and provision your Lex chatbot.