---
date: "2018-01-23T11:21:11+06:00"
title: "Send notifications using Firebase"
---

---

## What is Firebase?
  
Firebase is a very popular platform for developing mobile and web application. Firebase provides many services of different categories such as : analytics, authentication, app performance reports, cloud hosting etc. To view the list of all products with details, please check this [page](https://firebase.google.com/products/).

---

## Firebase Cloud Messaging (FCM)

Firebase Cloud Messaging([FCM]((https://firebase.google.com/products/cloud-messaging/))) (Formerly known as Google Cloud Messaging or GCM) is a cross-platform messaging solution that lets us reliably deliver and receive messages and notifications on Android, iOS and the Web at no cost.

### Key Capabilities
  
* We can send message to single devices, to groups of devices, or to devices subscribed to topics. 
* Client apps can also send messages to our server over FCM.
* We can send notification messages immediately, or at a future time in the user's local time zone.
* Messages are fully integrated with Firebase Analytics in order to track user engagement and conversion.

---

## How does it work?

An FCM implementation includes two main components for sending and receiving messages or notifications

 1) A trusted environment such as [Cloud Functions](https://firebase.google.com/products/functions/) for Firebase or an app server

 2) An iOS, Android, or web (JavaScript) client app that receives messages.

The app server (or trusted server environment) sends message requests to the FCM servers(provided by Google), which then sends messages to client apps.

---

## FCM Messages

FCM messages are divided into two types : Notification messages and Data messages.

#### 1) Notification messages :
Notification messages are handled by the FCM SDK automatically. They are also known as "display messages" as these messages are displayed on the user’s device by FCM on behalf of the application.

e.g.,
 
```
{
  "message":{
    "token":"YOUR-TOKEN-GOES-HERE...",
    "notification":{
      "title":"New Message",
      "body":"You've got a message"
    }
  }
}
```

#### 2) Data messages :
Client app is responsible for processing [data messages]. These messages have only custom key-value pairs and maximum payload is 4KB.

e.g.,

```
    {
      "message":{
        "token":"YOUR-TOKEN-GOES-HERE...",
        "data":{
          "id" : 101,
          "category" : "tech",
        }
      }
    }
```

#### Notification messages with an optional data payload

We can also send notification messages with an optional data payload. In such cases, FCM will handle displaying the notification payload, and the client app will handle the data payload.

i.e., Message with optional data payload :

```
{
  "message":{
    "token":"YOUR-TOKEN-GOES-HERE...",
    "notification":{
      "title":"New Message",
      "body":"You've got a message"
    },
    "data" : {
      "id" : 101,
      "category" : "tech",
    }
  }
}
```

> When apps receive messages that include both notification and data payloads, the behavior of the app depends on whether the app is in the background or the foreground. For more details, please visit this [page](https://firebase.google.com/docs/cloud-messaging/concept-options#notification-messages-with-optional-data-payload).

### Customizing a message across platforms :
      
It is possible to customize FCM messages for different platforms (ios, android etc) using platform-specific key blocks. So, when creating a message, we can target that message for android or iphone apps only. We may also send a common message to all platforms but with some platform-specific values so that different platforms can handle that message correctly.

For example, this request sends a common notification title and content to all platforms, but also sends some platform-specific overrides.

```
{
  "message":{
    "token":"YOUR-TOKEN-GOES-HERE...",
    "notification":{
      "title":"New Message",
      "body":"You've got a message"
    },
    "android":{
      "ttl":"86400s",
      "notification":{
        "click_action":"OPEN_ACTIVITY_1"
      }
    },
    "apns":{
      "headers":{
        "apns-priority":5
      },
      "payload":{
        "aps":{
          "category":"NEW_MESSAGE_CATEGORY"
        }
      }
    },
    "webpush":{
      "headers":{
        "TTL":"86400"
      }
    }
  }
}
```

for more details, please read the [offical doc](https://firebase.google.com/docs/cloud-messaging/concept-options#customizing_a_message_across_platforms).