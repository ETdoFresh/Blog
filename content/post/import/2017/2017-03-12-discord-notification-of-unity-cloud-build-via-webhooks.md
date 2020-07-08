---
title: Discord Notification of Unity Cloud Build via Webhooks
author: ETdoFresh
type: post
date: 2017-03-13T02:14:04+00:00
url: /discord-notification-of-unity-cloud-build-via-webhooks/
categories:
  - Programming
tags:
  - Unity

---
**EDIT**: Looks like Unity Cloud Build now has this built in! Yay! Thanks for those that did donated! Hope it helped you out in the interim!<figure class="wp-block-image">

[<img src="https://www.etdofresh.com/wp-content/uploads/2019/03/image.png" alt="" class="wp-image-1549" srcset="http://localhost/wp-content/uploads/2019/03/image.png 960w, http://localhost/wp-content/uploads/2019/03/image-300x179.png 300w, http://localhost/wp-content/uploads/2019/03/image-768x459.png 768w" sizes="(max-width: 960px) 100vw, 960px" />][1]</figure> 

<hr class="wp-block-separator" />

[<img class="aligncenter wp-image-851" src="https://www.etdofresh.com/wp-content/uploads/2017/03/webhook01-300x58.png" alt="" width="500" height="97" srcset="http://localhost/wp-content/uploads/2017/03/webhook01-300x58.png 300w, http://localhost/wp-content/uploads/2017/03/webhook01-768x148.png 768w, http://localhost/wp-content/uploads/2017/03/webhook01.png 942w" sizes="(max-width: 500px) 100vw, 500px" />][2]

I wanted to write a small blog post about how to show notifications on your Discord channel when a cloud build is ready. Here are the steps:

  1. (Optional) Add a channel where build notifications will appear
  2. Setup webhook URL in Discord
  3. Setup translation webhook
  4. Connect webhook URL to Unity Cloud Build
  5. Done!

### Add #builds Channel (optional)

[<img class="aligncenter size-medium wp-image-843" src="https://www.etdofresh.com/wp-content/uploads/2017/03/path4529-2-4-300x131.png" alt="" width="300" height="131" srcset="http://localhost/wp-content/uploads/2017/03/path4529-2-4-300x131.png 300w, http://localhost/wp-content/uploads/2017/03/path4529-2-4-768x335.png 768w, http://localhost/wp-content/uploads/2017/03/path4529-2-4-1024x447.png 1024w, http://localhost/wp-content/uploads/2017/03/path4529-2-4-1200x524.png 1200w" sizes="(max-width: 300px) 100vw, 300px" />][3]

If you like to keep the build information in a separate channel, create a new channel such as #builds in Discord

### Setup Webhook in Discord

The goal here is to get Discord&#8217;s webhook URL. Follow these steps:

<div id="attachment_844" style="width: 261px" class="wp-caption aligncenter">
  <a href="https://www.etdofresh.com/wp-content/uploads/2017/03/SetupWebhook00.png"><img aria-describedby="caption-attachment-844" class="wp-image-844 size-full" src="https://www.etdofresh.com/wp-content/uploads/2017/03/SetupWebhook00.png" alt="" width="251" height="62" /></a>
  
  <p id="caption-attachment-844" class="wp-caption-text">
    Edit Channel
  </p>
</div>

<div id="attachment_846" style="width: 310px" class="wp-caption aligncenter">
  <a href="https://www.etdofresh.com/wp-content/uploads/2017/03/path4597.png"><img aria-describedby="caption-attachment-846" class="wp-image-846 size-medium" src="https://www.etdofresh.com/wp-content/uploads/2017/03/path4597-300x144.png" alt="" width="300" height="144" srcset="http://localhost/wp-content/uploads/2017/03/path4597-300x144.png 300w, http://localhost/wp-content/uploads/2017/03/path4597-768x369.png 768w, http://localhost/wp-content/uploads/2017/03/path4597-1024x492.png 1024w, http://localhost/wp-content/uploads/2017/03/path4597-1200x576.png 1200w" sizes="(max-width: 300px) 100vw, 300px" /></a>
  
  <p id="caption-attachment-846" class="wp-caption-text">
    Create Webook | Fill out Name and Channel | Save | Copy Webhook URL
  </p>
</div>

### Setup Translation Webhook

Until Unity Cloud Build or Discord comes up with a way to produce/consume each other&#8217;s webhook, I came up with a solution that translates Unity Cloud Build&#8217;s webhook into a Discord webhook. Here&#8217;s how to set it up:

Create a new Translation Webhook: <https://www.etdofresh.com/webhook/translate.php?from=unity&to=discord>

<div id="attachment_855" style="width: 310px" class="wp-caption aligncenter">
  <a href="https://www.etdofresh.com/wp-content/uploads/2017/03/webhook02-1.png"><img aria-describedby="caption-attachment-855" class="wp-image-855 size-medium" src="https://www.etdofresh.com/wp-content/uploads/2017/03/webhook02-1-300x110.png" alt="" width="300" height="110" srcset="http://localhost/wp-content/uploads/2017/03/webhook02-1-300x110.png 300w, http://localhost/wp-content/uploads/2017/03/webhook02-1.png 709w" sizes="(max-width: 300px) 100vw, 300px" /></a>
  
  <p id="caption-attachment-855" class="wp-caption-text">
    Paste Discord&#8217;s Webhook URL, Click Update, and Copy Webhook at bottom of page.
  </p>
</div>

Feel free to change Username and Avatar URL if you like.

### Connect Webhook to Unity Cloud Build

Now we have to connect the webhook to Unity Cloud Build. Navigate to your project&#8217;s Cloud Build under <https://developer.cloud.unity3d.com/projects/>. Then go to the Notifications Tab and click &#8220;Add New Webhook&#8221;

[<img class="aligncenter size-medium wp-image-847" src="https://www.etdofresh.com/wp-content/uploads/2017/03/path4612-300x104.png" alt="" width="300" height="104" srcset="http://localhost/wp-content/uploads/2017/03/path4612-300x104.png 300w, http://localhost/wp-content/uploads/2017/03/path4612-768x266.png 768w, http://localhost/wp-content/uploads/2017/03/path4612-1024x354.png 1024w, http://localhost/wp-content/uploads/2017/03/path4612-1200x415.png 1200w" sizes="(max-width: 300px) 100vw, 300px" />][4]

Then paste your Webhook URL, setup the webhook as you like, and Save!

[<img class="aligncenter wp-image-857 size-medium" src="https://www.etdofresh.com/wp-content/uploads/2017/03/webhook03-300x196.png" alt="" width="300" height="196" srcset="http://localhost/wp-content/uploads/2017/03/webhook03-300x196.png 300w, http://localhost/wp-content/uploads/2017/03/webhook03-768x500.png 768w, http://localhost/wp-content/uploads/2017/03/webhook03.png 890w" sizes="(max-width: 300px) 100vw, 300px" />][5]

Give it a ping to make sure it works!

[<img class="aligncenter wp-image-858 size-medium" src="https://www.etdofresh.com/wp-content/uploads/2017/03/webhook04-300x95.png" alt="" width="300" height="95" srcset="http://localhost/wp-content/uploads/2017/03/webhook04-300x95.png 300w, http://localhost/wp-content/uploads/2017/03/webhook04.png 404w" sizes="(max-width: 300px) 100vw, 300px" />][6]

 

 [1]: https://www.etdofresh.com/wp-content/uploads/2019/03/image.png
 [2]: https://www.etdofresh.com/wp-content/uploads/2017/03/webhook01.png
 [3]: https://www.etdofresh.com/wp-content/uploads/2017/03/path4529-2-4.png
 [4]: https://www.etdofresh.com/wp-content/uploads/2017/03/path4612.png
 [5]: https://www.etdofresh.com/wp-content/uploads/2017/03/webhook03.png
 [6]: https://www.etdofresh.com/wp-content/uploads/2017/03/webhook04.png