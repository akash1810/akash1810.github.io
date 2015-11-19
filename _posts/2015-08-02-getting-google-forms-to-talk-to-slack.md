---
layout: post
title: Getting Google Forms to talk to Slack
---

When you want to get feedback from a site you're developing, a [Google Form](https://www.google.co.uk/forms/about/) is a quick and cheap solution. In the simplest case, all you need is a form with a single free text field to allow people to write freely.

Once you've got your form, add a link to it on your site and you're done. But wait, how do you know when someone has completed the form? Well, you could set up an email trigger, so that you'll get an email once a new response has been made. The trouble with that though is you can't create a trigger to email a group - the recipient will be the email address of the account creating the trigger.

So if you're developing the site in a group, you'll either need to get everyone to create their own trigger, or setup an email forwarding rule.

This is all going on the assumption that you read and respond to your email in real time - I know I certainly don't! If only there were other ways to be informed...

Well, how about posting to a Slack channel?

Turns out this is actually really simple and is a one off process. You'll need to add a [Google Apps Script](https://developers.google.com/apps-script/quickstart/forms-add-on) to your form, then configure a trigger. Then, using an [Incoming Webhook](https://api.slack.com/incoming-webhooks) to post to Slack, we'll format the Form response as an attachment to make the message a bit richer, resulting in a message that looks like:

![Slack message](/img/2015-08-02/slack-message.png)

Much better! We now post to Slack, with an `@channel` mention so that everyone on the channel is alerted to the message. We also show all the information in the message: who completed the form, when and what they said.

There are also two links in the message too - one to view the Google Sheets that holds all the Form's responses and another to email the sender using a simple `mailto` link.

#Open `mailto` in GMail Compose

I'm not sure about you, but I'm not the biggest fan of `mailto` links as it requires you to have set up something to handle that protocol - on a mac, its the Mail App, which I don't actually use. I'd much prefer to just use the GMail web client to compose the message. Well, you can!

Just replace `responseAttachment` in the below snippet with:

{% highlight js %}
var responseAttachment = {
    "fallback": FormApp.getActiveForm().getTitle(),
    "title": "Respond via email?",
    "title_link": "https://mail.google.com/mail/u/0/?view=cm&fs=1&tf=1&source=mailto&to=" + e.response.getRespondentEmail()
};
{% endhighlight %}


All this does is replace `mailto` with `https://mail.google.com/mail/u/0/?view=cm&fs=1&tf=1&source=mailto&to=` which will open a new tab to compose an email to the address of the `to` query value.

[Test it yourself](https://mail.google.com/mail/u/0/?view=cm&fs=1&tf=1&source=mailto&to=person@email.com).

#The Code

Grab the full code below.

{% gist 640a45d5997de1d95f4a %}

#Screencast
[![screencast](http://img.youtube.com/vi/bBkXdagMGaw/0.jpg)](http://www.youtube.com/watch?v=bBkXdagMGaw)
