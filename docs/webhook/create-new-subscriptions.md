---
title: Create New Subscriptions
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: noindex
next:
  description: ''
---
After completing the develop of your webhook endpoint, please follow these steps to add a webhook subscription in the Omnichat Admin Panel.

Here is the steps of the configuration:

1. In the Omnichat Admin Panel, navigate to **Settings** on the left menu, then find **Webhook Settings** and click to enter the page.

<Image align="center" className="border" width="200px" border={true} src="https://files.readme.io/f1bc5a5-image.png" />

2. In the **Webhook Settings** page, click the **Create Webhook** button.

<Image align="center" className="border" border={true} src="https://files.readme.io/9fd80a8-image.png" />

3. Fulfill the form and click **Save**:

   i. In the **Name** field, enter a name to identify this subscription.

   ii. In the **Endpoint URL** field, enter the endpoint URL you developed to receive event notifications.

   iii. In the **Verification Token** field, enter a specified string. Omnichat will pass this to you for verification during **Endpoint Verification**.

   iv. If you want to enable the subscription immediately, move the **Status** toggle to the right (Enabled). Omnichat will verify the endpoint's validity when you click **Save**.

   v. Finally, choose the topics you want to subscribe to.

<Image align="center" className="border" border={true} src="https://files.readme.io/baaf407-image.png" />

4. After saving, a success message will be displayed.

<Image align="center" className="border" width="500px" border={true} src="https://files.readme.io/714c6a6-image.png" />

5. You can obtain the **Signature Secret** in your subscription data.

<Image align="center" className="border" border={true} src="https://files.readme.io/20f39fe-image.png" />
