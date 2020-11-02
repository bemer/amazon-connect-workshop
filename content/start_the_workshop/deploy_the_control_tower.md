+++
title = "Deploy the AWS Control Tower"
weight = 21
+++


AWS Control Tower is a managed service, that provides the easiest way to set up and govern a new, secure, multi-account AWS environment based on best practices established through AWS’ experience working with thousands of enterprises as they move to the cloud. You could initiate the AWS Control tower deployment from the AWS Management Console with few clicks and a form to fill.

{{% notice tip %}}
Even though the AWS Control Tower is not a requirement to have the Amazon Connect succesfully implemented, we understand that many of the customers that uses this service have multi-tenancy needs. If this is not your case and you want to just start playing with the Amazon Connect without creating this additional infrastructure pieces you can proceed to the chapter [Creating an Amazon Connect instance](ADD.LINK.HERE).
{{% /notice %}}


{{% notice info %}}
It takes 60-90 minutes to launch an AWS Control Tower on a new AWS account. Hence we recommend to deploy the AWS Control Tower Section upfront before attending the class if possible.
{{% /notice %}}

In this section, we will deploy the AWS Control Tower service. Following tasks are performed on the successful launch of the service:

* Creates 1 additional organizational units for your Connect instance.
* Provisions 2 additional accounts on top of master account. These are used for log archive, and security audit.
* 24 preventive guardrails to enforce policies and 16 detective guardrails to detect violations.
* A native cloud directory with preconfigured groups and single sign-on access.

In order to launch the **AWS Control Tower** you should access the [AWS Control Tower](https://console.aws.amazon.com/controltower/home) console in your AWS account. Note that this account will be referred to as **Master account** henceforth. 

The AWS Control Tower is currently supported in the following regions: N. Virginia, Ohio, Oregon, Ireland and Sydney. Please make sure you are in one of these five supported regions. 

On the AWS Control Tower home page, select Set up your landing zone button:

![SetupLandingZone](/images/deploy-the-control-tower/setup_landing_zone.png)

You will be taken to the *Landing Zone setup screen*. In this page you will need to provide two email addresses that will be used to provision the shared accounts: Log archive account and the Audit account.

![AccountEmails](/images/deploy-the-control-tower/account_emails.png)

>The **Log archive account** works as a repository for logs of API activities and resource configurations from all accounts in the landing zone and the **Audit account** is a restricted account that's designed to give your security and compliance teams read and write access to all accounts in your landing zone. From the audit account, you have programmatic access to review accounts, by means of a role that is granted to Lambda functions only. You can find more information about the accounts provisioned by the Control Tower in the [official documentation](https://docs.aws.amazon.com/controltower/latest/userguide/how-control-tower-works.html).

After adding the email addresses, make sure you click in the *"I understand the permissions AWS Control Tower will use to administer AWS resources and enforce rules on my behalf."* checkbox before clicking in **Set up landing zone**:

![AgreementCheckbox](/images/deploy-the-control-tower/agreement_checkbox.png)

After clicking in the *Set up landing zone* button you will be redirected to AWS Control Tower Dashboard. The launch progress will be shown in the blue bar on top of the Dashboard. At this point you will need to wait until the Landing Zone creation is completed. Since there will be new accounts being created, you will need to check your emails for account creation confirmation from AWS Single Sign-On.

After some minutes, you will receive an email with the subject **Invitation to join AWS Single Sign-On** on the master account email address. You will have toopen this email and click on **Accept invitation**. This email will also contain the *User portal* URL. We recommend you to bookmark this since you will be using this same URL to access the AWS environment in the following labs.

When clicking in *Accept Invitation*, you will be redirected to the AWS Single Sign-On page where you will be asked to set a new password to your master account.

Another email will be sent to your master account email address with the subject ** receive one more email with subject **AWS Organizations email verification request**. Make sure you click on **Verify your email address** to continue with inviting newly created accounts into AWS Organization.

Wait for the blue progress bar with % complete to disappear on top of the AWS Control Tower dashboard.

{{% notice tip %}}
The email address you provided for the audit account will receive AWS Notification - Subscription Confirmation emails from every AWS Region supported by AWS Control Tower. To receive compliance emails in your audit account, you must choose the Confirm subscription link within each email from each AWS Region supported by AWS Control Tower.
{{% /notice %}}

After deploying the Control Tower, you should be able to move to the next step.