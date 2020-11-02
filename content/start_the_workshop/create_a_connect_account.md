+++
title = "Create an Account for Amazon Connect"
weight = 22
+++


Since we have already created a landing zone by leveraging the Control Tower, let's now create an AWS Account where we will deploy the Amazon Connect instance.

{{% notice tip %}}
Note that the goal of this workshop is to show you how to have a multi-tenant environment where you can spin up multiple AWS Accounts to host different Amazon Connect instances, so in a real world scenario, you can replicate exactly these steps when building your environment.
{{% /notice %}}

To do so, let's start by creating a new *Organization Unit* into our organizations. You can use organizational units (OUs) to group accounts together to administer as a single unit. This greatly simplifies the management of your accounts. For example, you can attach a policy-based control to an OU, and all accounts within the OU automatically inherit the policy. You can create multiple OUs within a single organization, and you can create OUs within other OUs. Each OU can contain multiple accounts, and you can move accounts from one OU to another. However, OU names must be unique within a parent OU or root.

When running a large deployment of Amazon Connect with multiple different customers or AWS Accounts, the first step is to create a new *OU* for each one of these customers. To do so, the first step is to access the Organizational units under the [Control Tower console](https://console.aws.amazon.com/controltower/home/organizationunits). Now, click in the **Add an OU** button on the top right corner of the screen:

![CreateAnOu](/images/create-an-account/add_an_ou.png)

Name the OU *CustomerOne* and click in **Add**:

![NameOu](/images/create-an-account/ou_naming.png)

After creating the OU, we should be able to provision a new AWS Account that will be used to run the Amazon Connect instance. 

{{% notice tip %}}
When dealing with Amazon Connect, the recommendation is that you create different accounts for different environments, such as *Dev*, *QA* and *Prod*.
{{% /notice %}}

Let's now leverage the Control Tower [Account factory](https://docs.aws.amazon.com/controltower/latest/userguide/account-factory.html) to provision the Dev account for our environment. Start by acessing the [Account factory](https://console.aws.amazon.com/controltower/home/accountfactory) menu on the left side of the screen. Now, click in **Enroll account**. After this, you will need to fill informations about this brand new account:

- For *Account email*: use a new email address that will be associated to that account
- For *Display name*: Use *CustomerOneDevAccount*
- AWS SSO email: use the email address that will be used to access this account with the SSO
- AWS SSO user name: the user name of the SSO email address (can be your name)

Make sure that you are also selecting the **CustomerOne** Organizational unit from the drop down list:

![CreateDevAccount](/images/create-an-account/create_dev_account.png)

After filling all the fields, click in **Enrol account**. It will take some time until the account is created, but after that you should be able to access it using the AWS SSO.

{{% notice tip %}}
If you want to learn more about the Control Tower setup, you can reffer to the Control Tower [official documentation](https://docs.aws.amazon.com/controltower/latest/userguide).
{{% /notice %}}
