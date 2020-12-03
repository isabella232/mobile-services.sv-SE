---
description: Du kan bifoga bildfiler till dina Android-meddelanden. Genom att lägga till visuella komponenter kan du öka användarnas engagemang avsevärt med push-meddelanden.
seo-description: Du kan bifoga bildfiler till dina Android-meddelanden. Genom att lägga till visuella komponenter kan du öka användarnas engagemang avsevärt med push-meddelanden.
seo-title: Ta emot omfattande push-meddelanden
title: Ta emot omfattande push-meddelanden
uuid: 4a0340a6-666b-49b6-907a-9afc966dfdba
translation-type: tm+mt
source-git-commit: dca3663986b3ecc6e9fb736cc99513279715225c
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---


# Få omfattande push-meddelanden {#receive-rich-push-notifications}

Du kan bifoga bildfiler till dina Android-meddelanden. Genom att lägga till visuella komponenter kan du öka användarnas engagemang avsevärt med push-meddelanden.

## Hantera inkommande RTF-meddelande (Rich push Message) {#section_AF1A3BC2312C4E1DA517CC90296C11E2}

Om appen finns i förgrunden hanteras push-meddelandet av appen som utökar `FirebaseMessagingService` klassen och deklareras i manifestfilen på följande sätt:

```java
<service
    android:name=".MyFirebaseMessagingService"
    android:exported="false">
    <intent-filter>
        <action android:name="com.google.firebase.MESSAGING_EVENT" />
    </intent-filter>
</service>
```

>[!IMPORTANT]
>
>Klassen som innehåller implementeringen hanterar de data som tas emot. `onMessageReceived()`

Om push-meddelandet innehåller en medie-URL är URL:en tillgänglig i den parameter `RemoteMessage` som skickas till `onMessageReceived()` funktionen. Nyckeln som ska användas visas `attachment-url` i följande kodexempel:

```java
public class MyFirebaseMessagingService extends FirebaseMessagingService {
        @Override
        public void onMessageReceived(RemoteMessage remoteMessage) {
      Log.d("Remote Message", "RemoteMessage: " + remoteMessage.toString());
            // Check if message contains a data payload.
            if (remoteMessage.getData().size() > 0) {
                Log.d("Remote Message", "RemoteMessage: " + remoteMessage.getData());
                sendNotification(remoteMessage);
            }
    }
 
private void sendNotification(RemoteMessage message) {
        Intent intent = new Intent(this, MainActivity.class);
    intent.addFlags(Intent.FLAG_ACTIVITY_CLEAR_TOP);
    PendingIntent pendingIntent = PendingIntent.getActivity(this, 0 /* Request code */, intent, PendingIntent.FLAG_ONE_SHOT);

     String channelId = getString(R.string.default_notification_channel_id);
     Uri defaultSoundUri = RingtoneManager.getDefaultUri(RingtoneManager.TYPE_NOTIFICATION);
     NotificationCompat.Builder notificationBuilder =
                new NotificationCompat.Builder(this, channelId)
                        .setSmallIcon(R.drawable.ic_stat_ic_notification)
                        .setContentTitle(getString(R.string.fcm_message))
                        .setContentText(message.getData().get("body"))
                        .setAutoCancel(true)
                        .setSound(defaultSoundUri)
                        .setContentIntent(pendingIntent);
  
    //Handle image url if present in the push message 
        String attachmentUrl = message.getData().get("attachment-url");
  
    if (attachmentUrl != null) { 
    Bitmap image = getBitmapFromURL(attachmentUrl); 
    if (image != null) { 
      notificationBuilder.setStyle(new        NotificationCompat.BigPictureStyle().bigPicture(image)); 
        } 
        } 

     NotificationManager notificationManager =
              (NotificationManager) getSystemService(Context.NOTIFICATION_SERVICE);

     // Since android Oreo notification channel is needed.
     if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.O) {
        NotificationChannel channel = new NotificationChannel(channelId,
                    "Channel human readable title",
                    NotificationManager.IMPORTANCE_DEFAULT);
            notificationManager.createNotificationChannel(channel);
     }

     notificationManager.notify(0 /* ID of notification */, notificationBuilder.build());
    }
}
```

>[!IMPORTANT]
>
>När du anger `NotificationCompat.BigPictureStyle`det kanske inte stora bilder visas. Om du vill vara säker på att stora bilder alltid visas anger du det ursprungliga `Notification.BigPictureStyle`fotot.

## Exempel på omfattande push-meddelanden {#section_6819316BEDDE45108413B541CA2BB2DC}

Här följer ett exempel på ett omfattande push-meddelande med en bild:

![](assets/rich-push-notification_example.png)

Mer information om avancerade push-meddelanden med Android finns i [Engagera med multimediemeddelanden](https://developer.android.com/distribute/best-practices/engage/rich-notifications.html).
