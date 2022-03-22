---
description: In Adobe Analytics, you can manage roles on the Admin Tools Home page.
title: Roles and Permissions
uuid: ad350f8d-ef51-4519-98aa-3025bc0f5588
exl-id: 70f0b427-60d5-4a79-a8d3-e03274edd917
source-git-commit: 7b26c852dd9dba67a8b5e3228c1fecadfb465dca
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 1%

---

# Roles and permissions{#roles-and-permissions}

In Adobe Analytics, you can manage roles on the Admin Tools Home page.

## Översikt {#section_91B8192891E14E5285718C8118912500}

The following roles manage permissions in the Mobile Services UI:

### Analytics Admin

An Analytics Admin manages user groups and assigns permissions, one of which is the Mobile App Admin. The Experience Cloud Admin links your Adobe ID to your Adobe Analytics account, which allows you to log in to the Mobile Services UI by using your Adobe ID. [](https://experienceleague.adobe.com/docs/core-services/interface/administration/admin-getting-started.html)

>[!TIP]
>
>An existing Analytics Admin has the ability to assign the Analytics Admin role to any user.

### Mobile App Admin

This role is the Admin for the Mobile Services UI.

>[!IMPORTANT]
>
>**[!UICONTROL Segment Creation]**

## Managing access {#section_E6939C2695AA4A0DBF432D50B2670920}

Here is some additional information about accessing options in the Mobile Services UI:

### Apps and report suites

All Mobile Service apps are tied to report suites. If users do not have access to a report suite, they will not have access to that report suite&#39;s associated app.

### Mobile Services and Analytics features

If your company does not have an Analytics contract to access a feature in the UI, such as Push Messaging, no user in your company will have access to that feature, regardless of permission level.

## Roles and permissions {#section_20AA029D5B8C413C8659777E79B11620}

Here are the roles in the Mobile Services UI, with their relevant permissions:

### Analytics Admin permissions

* All User and Mobile App Admin Permissions
* Create App with new report suite
* Delete App from Mobile Services

   >[!IMPORTANT]
   >
   >Although the app has been deleted in the Mobile Services UI, the report suite still exists in Analytics.

* Manage App Settings

   * Enable Lifecycle Reporting
   * Enable Location Reporting
   * Create/Update/Delete Variables and Metrics

### Mobile App Admin permissions

* All User Permissions
* Create App with existing report suite
* Manage App Settings

   * Configure App&#39;s Mobile SDK options
   * Configure App&#39;s UI settings
   * Configure linked App Store apps
   * Configure App&#39;s Universal Link options
   * Configure Push Services certs and API keys
   * Create/Update/Activate/Deactivate/Duplicate/Archive/Delete Postbacks
   * Create/Update/Archive/Delete Link Destinations

* Create/Update/Archive Marketing Links
* Create/Import/Update/Delete Legacy Acquisition Links
* Create/Import/Update/Delete Places (Points of Interest) configuration
* Create/Update/Send/Schedule/Cancel/Duplicate/Archive/Delete Push Messages
* Create/Update/Activate/Deactivate/Duplicate/Archive/Delete In-App Messages

For more information about groups and users, see the following content in the Adobe Analytics documentation:

* [](https://experienceleague.adobe.com/docs/analytics/admin/admin-console/home.html)
* [Lägga till en användare i en grupp](https://experienceleague.adobe.com/docs/analytics/admin/admin-console/home.html)

### Mobile Services user

This role has view-only permissions and can provide feedback in the Mobile Services UI.

* Provide Feedback on Mobile Services UI
* View Apps

   >[!IMPORTANT]
   >
   >Users can only see the report suites for which they have access in Adobe Analytics.

* View App Settings

   * Download App SDK configuration
   * View all UI and SDK settings
   * View Variables and Metrics configuration
   * View Postbacks
   * View Link Destinations

* View and Run Reports
* View Marketing Links
* View and Export Legacy Acquisition Links
* View and Export Places (Points of Interest) configuration
* View Push Messages
* View In-App Messages
