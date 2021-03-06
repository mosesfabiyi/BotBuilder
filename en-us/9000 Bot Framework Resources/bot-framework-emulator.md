---
layout: 'redirect'
permalink: /en-us/tools/bot-framework-emulator/
redir_to: 'https://docs.microsoft.com/en-us/bot-framework/debug-bots-emulator'
sitemap: false
---

We have released a new Bot Framework Emulator! Get it [here](https://emulator.botframework.com/) and for documentation, [here](https://github.com/microsoft/botframework-emulator/wiki/Getting-Started). 

![Bot Framework Emulator running on Ubuntu](/en-us/images/emulator/newemulator-ubuntu.png)

The Emulator is one of your most powerful tools in building your bot, and the new one is a great upgrade over our v1 emulator.

* **New** Support for Mac, Linux and Windows
* **New** All the Bot Framework card types are supported
* **New** Save multiple profiles for when you're working online and off
* **New** Simplifies configuration when you're working with ngrok
* **New** Uses the webchat control for higher fidelity layout and consistency with the webchat experience
* Send requests and receive responses to/from your bot endpoint on localhost
* Inspect the Json response
* Emulate a specific user and/or conversation

<div>And - a much requested feature, the new Emulator is open source, please check it out on <a href="https://github.com/Microsoft/BotFramework-Emulator" target="_blank">GitHub</a></div>

{% comment %}
* TOC
{:toc}

## What is the Bot Framework Emulator?
The Bot Framework provides an emulator that lets you test calls to your Bot as if it were being called by the Bot Framework cloud service. 

Using the Emulator, you can:

* Send requests and receive responses to/from your bot endpoint on localhost
* Inspect the Json response
* Emulate a specific user and/or conversation

## Installation and configuration

[Install the Windows Emulator](https://aka.ms/bf-bc-emulator)
 
See an example of use in the [Getting started page](/en-us/csharp/builder/sdkreference/gettingstarted.html#emulator).

## Using the Emulator with Ngrok to interact with your bot in the cloud
You can also use the emulator to talk with your bot deployed in the cloud.  Doing this allows you to see JSON back and forth, and also the RAW
error messages that are hidden from the end user in normal chat.

In the V3 version of the Bot Framework API, the authentication model has changed from Basic Auth to Open Id with JWT tokens and Microsoft Account. 
Doing auth in this way introduces the additional requirement of being able to get auth callbacks to the Emulator from the Internet.  Conveniently
[ngrok](https://ngrok.com/)\* provides an easy way to do this for debugging/diagnosis purposes. *\*ngrok is not a Microsoft product.*

Download ngrok from the site; and run it from a command prompt:

{% highlight csharp %}
    ngrok http -host-header=rewrite 9000
{% endhighlight %}

![Getting ngrok running](/en-us/images/emulator/emulator-ngrok-config.png)

This will set up a temporary open port 9000 that will be redirected from an ngrok location out on the web. The forwarding https URL is the 
piece we have to care about for now.

Now open up the Bot Framework Channel Emulator and fill in the fields at the top:

| field | value |
|-------|-------|
| Local port | 9000, or whatever was specified in the ngrok command |
| Emulator URL | the ngrok forwarding URL (with https) |
| Bot URL | the bot endpoint URL (with https) |
| Microsoft App ID | Your Microsoft App ID |
| Microsoft App Password | Your Microsoft App Password |

Once populated, the emulator will look a little like this:

![Emulator configured for cloud debugging](/en-us/images/emulator/emulator-testbot-cloud-config.png)

In this configuration, ngrok also offers some lovely communication monitoring by opening a browser to the port http://127.0.0.1:4040.

## Mac and Linux support using command line emulator
For folks who are developing on Mac and Linux we have created a console only version which works using mono. 

To install

1. Download [Console Emulator Zip](https://aka.ms/bfemulator)
2. Unzip it
3. Install [Mono](http://www.mono-project.com/download/#download-mac)
4. mono BFEmulator.exe

{% comment %}adding tabs for codeblocks after a list, embeds them in the last list item. adding &nbsp; to break it.{% endcomment %}
&nbsp;

    Microsoft Framework Emulator
    
    /exit or /quit to exit
    /settings to change endpoint, appId and appSecret settings
    /dump [#] to show contents of last # messages (default: 1)
    /attachment [path] <- to add a file to your message
    Current settings:
    Endpoint: http://localhost:8002/api/messages
    AppId: TestBot
    AppSecret: 12345678901234567890123456789012
              

    > hello
    Cookie:1 User:1 Conversation:1 PerUser:1 You said:hello


    > /dump

    TestBot said:
    Cookie:1 User:1 Conversation:1 PerUser:1 You said:hello
    ==== raw BOT Content ====
    {
      "type": "Message",
      "conversationId": "8a684db8",
      "language": "en",
      "text": "Cookie:1 User:1 Conversation:1 PerUser:1 You said:hello",
      "from": {
        "name": "TestBot",
        "channelId": "emulator",
        "address": "TestBot",
        "isBot": true
      },
      "to": {
        "name": "User1",
        "channelId": "emulator",
        "address": "User1",
        "isBot": false
      },
      "replyToMessageId": "8c0aa5205b374a6d8f58145e4dec041b",
      "participants": [
        {
          "name": "User1",
          "channelId": "emulator",
          "address": "User1"
        },
        {
          "name": "TestBot",
          "channelId": "emulator",
          "address": "TestBot"
        }
      ],
      "totalParticipants": 2,
      "channelMessageId": "cc693595f3e046ecb9c02bda9de603c0",
      "channelConversationId": "Conv1",
      "botUserData": {
        "counter": 1
      },
      "botConversationData": {
        "counter": 1
      },
      "botPerUserInConversationData": {
        "counter": 1
      }
    }

{% endcomment %}
