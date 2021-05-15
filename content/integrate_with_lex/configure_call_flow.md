+++
title = "Configure the Amazon Connect contact flow"
weight = 30
+++


After adding the bot to the Amazon Connect instance, it is time to configure the Contact Flow, so your calls can be handled by the Lex bot. To do so, access your Amazon Connect dashboard - you can do this by using your SSO administration login.

To make your life easier, insted of creating a contact flow from the scratch, you can just go ahead and download the provided [Cable TV Contact flow](/files/CableTVContactFlow.json).

On the Amazon Connect dashboard, on the left menu, click in **Contact Flows**:

![ContactFlowsMenu](/images/configure-contact-flow/contact_flow_menu.png)

Now, click in the **Create contact flow** option on the top right corner of the screen:

![CreateFlowButton](/images/configure-contact-flow/create_flow_button.png)

On the *New contact flow* page, click on the menu located on the right top of the pace and select the option **Import flow (beta)**. Than, select the **CableTvContactFlow.json** file that you just downloaded:

![ImportContactFlow](/images/configure-contact-flow/import_contact_flow.png)

Since the contact flow was generated in another account and possibly in a different region, make sure that you double click in the **Get customer input** block and select the proper Lex bot before moving forward:

![ClickGetCustomerInput](/images/configure-contact-flow/click_get_customer_input.png)

![SelectRightBot](/images/configure-contact-flow/select_right_bot.png)

After selecting the right Lex bot, click on the **Save** button and after in the **Publish**, both on the top right corner of the *Edit contact flow* screen:

![SaveAndPublish](/images/configure-contact-flow/save_and_publish.png)

Now that your Contact Flow is properly created, it is time to associate it with the Phone Number that was previously obtained. To do so, under the *Routing* menu, click in **Phone Numbers**:

![PhoneNumbersMenu](/images/configure-contact-flow/phone_numbers_menu.png)

You phone number will be exhibted in this screen. Click in it, and under the **Contact flow/IVR** option, select the **Cable TV Contact Flow**. After picking the right one, you can go ahead and click in **Save**:

![ChooseContactFlow](/images/configure-contact-flow/choose_contact_flow.png)


