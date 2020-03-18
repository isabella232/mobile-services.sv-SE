---
description: Du kan bifoga bildfiler till dina Apple-meddelanden. Genom att lägga till visuella komponenter kan du öka användarnas engagemang avsevärt med push-meddelanden.
seo-description: Du kan bifoga bildfiler till dina Apple-meddelanden. Genom att lägga till visuella komponenter kan du öka användarnas engagemang avsevärt med push-meddelanden.
seo-title: Ta emot omfattande push-meddelanden
title: Ta emot omfattande push-meddelanden
uuid: 0dbda409-cf49-4eb8-90ee-baf27911dc07
translation-type: tm+mt
source-git-commit: d028fe0f9477bc011aa8fda21a0a389808df0fce

---


# Få omfattande push-meddelanden {#receive-rich-push-notifications}

Du kan bifoga bildfiler till dina Apple-meddelanden. Genom att lägga till visuella komponenter kan du öka användarnas engagemang avsevärt med push-meddelanden.

Så här får du omfattande push-meddelanden i din iOS-app:

1. Implementera push-meddelanden för appen genom att slutföra stegen i [Push Messaging](/help/ios/messaging-main/push-messaging/push-messaging.md).
1. Verifiera att du kan skicka ett SMS-push-meddelande till din app.
1. Lägg till ett meddelandetjänsttillägg genom att utföra följande steg:

   1. Välj **[!UICONTROL File]** > **[!UICONTROL New]** > **[!UICONTROL Target]** i Xcode-projektet.
   1. Välj **[!UICONTROL Notification Service Extension]**.
   1. Kontrollera att `NotificationService.m` filen finns.

1. Öppna `NotificationService.m` filen och kontrollera att följande delegatmetoder finns:

   * En metod för att ta emot en meddelandebegäran.
   * En metod för att hantera tjänsttilläggets förfallodatum.

      Den första metoden används för att ta emot omfattande push-meddelanden:

      ```objective-c
      (void)didReceiveNotificationRequest:(UNNotificationRequest *)request withContentHandler:(void (^)(UNNotificationContent *contentToDeliver))contentHandler;
      ```

      I den här metoden kan du hämta medie-URL:en från `userInfo` med hjälp av `attachment-url` -tangenten. När du har hämtat filen till en lokal katalog lägger du till den lokala sökvägen i `bestAttemptContent.attachments`.

      Här är ett exempel på koden i den här metoden:

      ```objective-c
      - (void)didReceiveNotificationRequest:(UNNotificationRequest *)request withContentHandler:(void (^)(UNNotificationContent * _Nonnull))contentHandler {
      self.contentHandler = contentHandler;
      self.bestAttemptContent = [request.content mutableCopy];
         NSDictionary* userInfo = request.content.userInfo;
      if(userInfo[@"attachment-url"]){
         NSURL* url = [[NSURL alloc] initWithString:userInfo[@"attachment-url"]];
         NSURLSessionDownloadTask* task = [[NSURLSession sharedSession] downloadTaskWithURL:url completionHandler:^(NSURL * _Nullable location, NSURLResponse * _Nullable response, NSError * _Nullable error) {
             if(!location){
                 return;
             }
             NSString* tmpDirectory = NSTemporaryDirectory();
             NSString* tmpFilePath = [NSString stringWithFormat:@"file://%@%d%d%@", tmpDirectory, arc4random_uniform(100000),
                                    arc4random_uniform(100000), [url lastPathComponent]];
             NSURL* tmpUrl = [[NSURL alloc] initWithString:tmpFilePath];
             NSError * fileError = nil;
             [[NSFileManager defaultManager] moveItemAtURL:location toURL:tmpUrl error:&amp;fileError];
             if(fileError){
                 return;
             }
             UNNotificationAttachment* attachment = [UNNotificationAttachment attachmentWithIdentifier:@"video" URL:tmpUrl options:nil error:&amp;fileError];
             if(fileError){
                 return;
             }
             self.bestAttemptContent.attachments = @[attachment];
             self.contentHandler(self.bestAttemptContent);
         }];
         [task resume];
       }
      }
      ```


Mer information om avancerade push-meddelanden med iOS finns i [UNNotificationAttachment](https://developer.apple.com/documentation/usernotifications/unnotificationattachment).