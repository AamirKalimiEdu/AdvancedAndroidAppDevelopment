# Advanced Android App Development [13-10-2017]

## Stage 1 [13-10-2017]

## Stage 2 [14-10-2017]
**Fragments**  
*Fragments are Android app components that represent a self-contained portion of user interface in an activity. You can think of them as mini-activities. They are essentially reusable pieces of UI, similar to a layout similat to a layout or ViewGroup*

>It's important to note that a Fragment must always be embedded in an activity and the fragment's lifecycle is directly affected by the host activity's lifecycle. For example, when the activity is paused, so are all fragments in it, and when the activity is destroyed, so are all fragments.

*Fragments are reusable, modular (because they have their own lifecycle), and can be dynamically changed at runtime!*

**onCreateView()**  
*onCreateView() is where a fragment inflates its UI, hooksup any data source it needs, and then returns the created view to the host activity.*  

**onDestroyView()**  
And there's a corresponding on destroy view callback that can be called before a host activity is destroyed.*  

>Yes! When the host activity is created, both it, and the fragments it contains, call their onCreate methods. Then, right after this creation, fragments call their onCreateView method to inflate their view dynamically!

*Any class who want to be a fragment, "from chomu to fragment hahaha okay that enough go back to study pussy cat" must extends from Fragment and it's up to you use support.v4 Fragment or app.Fragment but this extension is important, because it's how Android knows to treat this class, and its lifecycle events and creation, as a fragment. Now every fragment will implement a couple of methods. The first is an empty constructor that's necessary for instantiating the fragment. The second is a method onCreateView, which is called when the fragment that we just created is inflates for display, similar to onCreate for an activity. So, make sure to implement for any fragment you create.*

>Every fragment needs to to be embedded in a host activity. 

**FragmentManager**  
*FragmentManager let's you add, remove, or replace fragments in an activity at runtime!*  
*FragmentManager facilitates these transactions:*
1. ADD
2. REMOVE
3. REPLACE


>Transactions let you create a dynamic user experience and help efficiently add and remove fragments wihtout you having to worry about the finer details of memory management. 

>To dynamically change fragments, you'll need a container view to reference their location and hold each fragment. This is often a empty FrameLayout 

**Containers are needed to use transactions:**  
1. ADD
2. REMOVE
3. REPLACE

>Static framents (that don't change during runtime) don not need a container

*Static fragments don't need transactions*  

*Make each fragment self-contained* -> *This just means that a single fragment will also contain code that define its layout and behavior, when it comes to user interaction. And it also means that generally, fragments can never directly communicate with one another. But then, how can you communicate between two self-contained fragments? Well all fragment to fragment communication can be done through a shared activity. To give a fragment the ability to communicate up to its host activity, it's good prectice to define an interface in the fragment class, and implement it within the activity. *

**Why interfaces?**  
*To keep fragments modular and reusable, you cannot have them communicate directly with one another or directly tied to a host activity. An interface gives you a way to communicate but also stay modular because it can be implemented by any host activity -- this way the fragment is not tied directly to an activity.*

## Stage 3 [15-10-2017]

*The Support Library includes methods for checking for existing permissions, and requesting new permissions in a backwards compatible way: It will only affect devices running API level 23 or higher, so you don't have to do any API level checks yourself.*

**64K Method Limit**  
*Another consideration in deciding whether or not to use a library is to be aware of how it will affect the size of your app. When your app, including the libraries it uses, reaches a certain size, you encounter build errors that indicate your app has reached a limit of the Android app build architecture (64K Method Limit). Libraries are commonly used and without a doubt efficient, but do be aware of theses considerations. *



**What two methods should you use with the FaceDetector.Builder to turn on Classifications and improve performance by disabling tracking (which maintains an ID between consecutive frames if the same face exists in both of them?)**  
*Great! setClassificationType(FaceDetector.ALL_CLASSIFICATIONS) and setTrackingEnabled(false) are the correct methods.*

>By default bitmaps are immutable meaning we can't change them

## Stage 4 [16-10-2017]

**Polling**  
*Polling, when we're talking about client-server communication, is the act of continually pinging the server every so often to see if there are any updates. If you've seen apps using JobSchedulers or sync adapters to connect to a server, more likely than not, the app is using the polling strategy.*  

**Pushing**  
*The idea behind a pushing strategy is that instead of having your client phone constantly asking the server if there are updates, instead, the server is responsible for telling the phone when it has new information.*  

**FCM Features**  
1. Automatic Retries  
2. Mass messages  
3. Cross-platform  
4. Scale  

**Add FCM to your project**  
1. Connect your app to Firebase  
2. Add FCM to your apps (Setup dependencies correctly)  
3. Acess the device registration token  

*Download the google-service.json config file and save it in Squawker's app directory. This configuration file is what tells Squawker what Firebase server instance to connect to online. It is specific to the Firebase "app" you just created. If you ever accidentally delete the google-service.json file, you can redownload it, by going to the app Settings.*

**FCM Registration Token**  
*An FCM registration token is a string of numbers and characters that is used to uniquely identify a device. It's generated when the app first starts and changes, say, if you uninstall and reinstall the app. The FCM server can use these unique tokens to send messages to specific devices. So let's see how you actually find out what the FCM registration token is for your device. There's actually pretty clear online documentation about how to do this. If i scroll down the first step is to create a service that extends from FirebaseInstanceIdService. Like all android components, the service needs to be registered to the manifest. Now to able to catch the event when a token is generated for your device, it's important that you intent filter here It has the action instance ID event. And after extending this service and adding it to the manifest, the only other real thing that you need to do is implement this onTokenRefresh() method And this menthod is part of the FirebaseInstanceIdService class. Functionally, you could od a couple of different things when this method is called.  But for you, you just want to know what the token is, so you can actually print it out in a log.*

>When the firebase console sends a message to the FCM server, it sends what's known as a notification message which looks like a notification with default look and feel by firebase you can change the look and feel if you want. This is the added benefit that on the client phone, it makes the notification appear. FCM has another type of message whic you seee here, known as a data message. The data message looks like this. But the key difference being that instead of saying notification here, it says data. Your app will react differently, depending on whether it will send a notification message or a data message. Notification messages display a message, as long as the app is in the background. They have predefined key value pairs such as the body key with some value. This controls what the body of your notification says. You can also have optional key value pairs that go into the intent extras bundle which is accessible when you launch the app for that notification. Also notification messages can be sent from the Firebase console. Now in comparison, data messages do nothing automatically. And what this means is that you're responsible for adding the code to process the data that comes in. It won't display a notification or anything like that automatically. Because data messages can do almost anything, they have whatever custom key value pairs you'd lie to pass along. Note that as of now, data messages cannot be sent from the firebase console which means that you have to go to the hard work of coding up your own server to send data messages.

Notificaction Message | Data Message
---|---
Display notification automatically | Requires you to do all the data processing 
Predefined key values | All custom key value pairs 
Extra values in intent extra | -
Can be sent from firebase console | cannot be sent from firebase console  
App in Background: shows notification | App in Foreground or Background: Triggers onMessageReceived
App in Foreground: triggers onMessageReceived(only if you setup the FirebaseMessagingService) | -  

**Notification + Data Messages**  
1. Cannot be sent fromm the Firebase console
2. App in the Background: 
    1. Shows notification, does not trigger onMessageReceived
    2. The notification has extra in the intent
3. App in the Foreground
    1. Trigger onMessageReceived 


*To receive and process a data message, you need to implement another service called FirebaseMessagingService. This involves three things. First, you need to create a service that extends FirebaseMessagingService. Then, you need to add that serrvice to the manifest with the MESSAGIN_EVENT intent filter. Finally, you should override the onMessageReceived method, which is inside of FirebaseMessagingService. This will create a service on your client phone that is triggered by incoming FCM data messages, as well as notification messages when the app is in the foreground. This is useful because it means the app can be in the background and get pinged by an FCM data message. And then you can execute whatever code you need in onMessageReceived.*


**Choosing Notification vs Data Messages**  
**Notificaction**  
1. You want the system to show notification on your behalf
2. You only need to run code in the foreground
3. Example: Advertisement or notification for a mobile gmae without the need to change code  

**Data** 
1. You need to run code, whether the app is in the background or the foreground, choose this option!
2. Example: Email app that should sync whenever a new message is received  


>Luckily, there are a few ways to send data to multiple phones using FCM. Two ways to send data to groups are using DeviceGroups and Topics  

**Device Groups**  
*Device groups are typically sets of devices that all belong to the same user. For example, if jessica owns two phones and a tablet that all use Squawker, we could store all of these devices together is a device group. The creation of management of these device groups is done on the server side on the app server. Now the squawker server doesn't actually do anything with device groups, and so, it's outside of the scope of this lesson. But i did link some additional information in the notes*  

**Topics**  
*Topics are a bit like mailing list. some client devices will choose to subscribe to a topic, and then only those devices which subscribed will be sent the messages when the topic sends a message. So what does this actually look like in code? On the server side, instead of sending a message to a specific ID, you could send the message to a topic. A topic is represented by a single string key. For example could use the key currentEvents. Note that the topic key will always come after the word topics surrounded by forward slashes /topics/currentEvents client devices can subscribe and unsubscribe to topics using that key. A device subscribed to a topic will get all the messages sent to that topic.*  
```java
// Subscribing to topics
FirebaseMessaging.getInstance().subscribeToTopic(“japan”);
FirebaseMessaging.getInstance().subscribeToTopic(”usa”);

// Unsubscribing from a topic
FirebaseMessaging.getInstance().unsubscribeFromTopic(“usa”);
```

>OK, so it's uper important to note that the key that you subcribe to, and the key that the server sends the message to, needs to match exactly. 

**There's more to explore in FCM**  
1. How to write FCM server code 
2. Managing registration id tokens and groups on an app server
3. Upstream messages are when to send meaages from your phone to FCM to be sent out to other devices but you know what is downstream messages getting messages from FCm server to your phone
4. Other message attributes
    1. Message Lifespan (how long FCM will keep trying to re-ping your device if its offline 
    2. Message Priority (determine  weather to wake your phone up if it's in doze mode)
    3. Collapsible/Non-collapsible Messages (Collapse messages are replaced when a new message is sent. For exmaple, let's say that your phone is off, and every time you get a new email, an FCM message tells your phone to sync withe the email server. If your phone is off for a week, you don't need to be told to sync your phone 100 times when you power your phone back on. You just need to be told to sync once.


