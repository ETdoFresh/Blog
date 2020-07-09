---
title: Discord Notification of Unity Cloud Build via Webhooks
author: ETdoFresh
type: post
date: 2017-03-13T02:14:04+00:00
url: /discord-notification-of-unity-cloud-build-via-webhooks/
featured_image: /wp-content/uploads/2017/03/path4597.png
hide_featured_image: true
tags:
  - Utility
  - Discord
  - Programming
  - Unity

---
**EDIT**: Looks like Unity Cloud Build now has this built in! Yay! Thanks for those that did donated! Hope it helped you out in the interim!<figure class="wp-block-image">

![](/wp-content/uploads/2019/03/image.png)

------------------------------------------------

![](/wp-content/uploads/2017/03/webhook01.png)

I wanted to write a small blog post about how to show notifications on your Discord channel when a cloud build is ready. Here are the steps:

  1. (Optional) Add a channel where build notifications will appear
  2. Setup webhook URL in Discord
  3. Setup translation webhook
  4. Connect webhook URL to Unity Cloud Build
  5. Done!

### Add #builds Channel (optional)

![](/wp-content/uploads/2017/03/path4529-2-4.png)

If you like to keep the build information in a separate channel, create a new channel such as #builds in Discord

### Setup Webhook in Discord

The goal here is to get Discord's webhook URL. Follow these steps:

{{< figure src="/wp-content/uploads/2017/03/SetupWebhook00.png" caption="Edit Channel" >}}

{{< figure src="/wp-content/uploads/2017/03/path4597.png" caption="Create Webook | Fill out Name and Channel | Save | Copy Webhook URL" >}}

### Setup Translation Webhook

Until Unity Cloud Build or Discord comes up with a way to produce/consume each other's webhook, I came up with a solution that translates Unity Cloud Build's webhook into a Discord webhook. Here's how to set it up:

Create a new Translation Webhook: <https://www.etdofresh.com/webhook/translate.php?from=unity&to=discord>

{{< figure src="/wp-content/uploads/2017/03/webhook02-1.png" caption="Paste Discord's Webhook URL, Click Update, and Copy Webhook at bottom of page" >}}

Feel free to change Username and Avatar URL if you like.

### Connect Webhook to Unity Cloud Build

Now we have to connect the webhook to Unity Cloud Build. Navigate to your project's Cloud Build under <https://developer.cloud.unity3d.com/projects/>. Then go to the Notifications Tab and click "Add New Webhook"

![](/wp-content/uploads/2017/03/path4612.png)

Then paste your Webhook URL, setup the webhook as you like, and Save!

![](/wp-content/uploads/2017/03/webhook03.png)

Give it a ping to make sure it works!

![](/wp-content/uploads/2017/03/webhook04.png)