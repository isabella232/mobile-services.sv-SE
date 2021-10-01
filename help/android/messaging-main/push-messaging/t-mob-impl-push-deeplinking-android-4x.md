---
description: När du har konfigurerat URL:en för djuplänkning i användargränssnittet för Adobe Mobile Services, kommer den här URL:en att finnas i push-nyttolasten med nyckeln adb_deplink.
title: Implementera push-meddelanden med djup länkning
uuid: e24f9248-8d48-4e57-84af-3a05b72e2a09
exl-id: ab97db32-d9d2-41ec-aae8-a951c7745df8
source-git-commit: f18d65c738ba16d9f1459ca485d87be708cf23d2
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---

# Implementera push-meddelanden med djuplänkning {#implement-push-messaging-with-deep-linking}

När du har konfigurerat URL:en för djuplänkning i användargränssnittet för Adobe Mobile Services, kommer den här URL:en att finnas i push-nyttolasten med nyckeln adb_deplink.

Du kan hämta URL:en genom att anropa `remoteMessage.getData().get("adb_deeplink")` i `FirebaseMessagingService`.

>[!TIP]
>
>Du kan definiera olika återgivningar beroende på om nyttolasten har en URL med djup länkning.

1. Gör något av följande:

   * Om URL:en för djuplänkning **är** i push-nyttolasten skapar du en `ACTION_VIEW`-metod med URL:en.

      När användaren klickar på push-meddelandet utlöses en djup länk.

   * Om URL:en för djuplänkning **inte är** i push-nyttolasten skapar du en metod som öppnar en av dina aktiviteter.

## Exempel

Här följer ett exempel på implementering för klassen som sträcker sig från `FirebaseMessagingService`:

```java
public void onMessageReceived(RemoteMessage message) { 
 
       Map<String, String> data = message.getData(); 
       String messageStr = data.get("message"); 
       String deepLink = data.get("adb_deeplink"); 
 
       sendNotification(deepLink, messageStr, data); 
    } 
 
private void sendNotification(String deeplink, String message, Map<String, String> data) { 
       Intent intent; 
 
       if (deeplink!=null) { 
           intent = new Intent(Intent.ACTION_VIEW, Uri.parse(deeplink)); 
       } else { 
           intent = new Intent(this, MainActivity.class); 
       } 
 
       intent.addFlags(Intent.FLAG_ACTIVITY_CLEAR_TOP); 
 
       //put the data map into the intent to track clickthroughs 
       Bundle pushData = new Bundle(); 
       Set<String> keySet = data.keySet(); 
       for (String key : keySet) { 
           pushData.putString(key, data.get(key)); 
       } 
 
       intent.putExtras(pushData); 
 
       PendingIntent pendingIntent = PendingIntent.getActivity(this, 0, intent, 
               PendingIntent.FLAG_ONE_SHOT); 
 
       Uri defaultSoundUri= RingtoneManager.getDefaultUri(RingtoneManager.TYPE_NOTIFICATION); 
 
       NotificationCompat.Builder notificationBuilder = new NotificationCompat.Builder(this) 
                .setSmallIcon(R.drawable.icon) 
                .setContentTitle("FCM Deep Link Push") 
                .setContentText(message) 
                .setAutoCancel(true) 
                .setSound(defaultSoundUri) 
                .setContentIntent(pendingIntent); 
 
       NotificationManager notificationManager =  
       (NotificationManager)getApplicationContext().getSystemService(Context.NOTIFICATION_SERVICE); 
           notificationManager.notify(0, notificationBuilder.build()); 
       } 
```
