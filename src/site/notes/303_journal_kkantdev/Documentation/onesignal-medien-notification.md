---
{"dg-publish":true,"permalink":"/303-journal-kkantdev/documentation/onesignal-medien-notification/","dg-note-properties":{}}
---

# How to Add Push Notifications to a Web App Wrapped as an APK

## 1. Deploy Your Web App

Create your web application using any platform or framework, such as Lovable, Next.js, or React.

- Deploy the application online.
    
- Copy the live website URL.
    
- Make sure the website is accessible publicly and is not running on localhost.
    

## 2. Create an App in Median.co

1. Open [Median.co](https://median.co/) and create an account.
    
2. Create a new app and enter your deployed website URL.
    
3. Configure your Android app settings.
    
4. Under **Deploy & Build**, find and copy the Android package name. You will need it when setting up Firebase.
    

## 3. Enable OneSignal in Median.co

1. Open your app in Median App Studio.
    
2. Navigate to **Native Plugins → OneSignal**.
    
3. Enable the plugin.
    
4. Keep Legacy Mode disabled for a new integration.
    
5. Leave the App ID field ready for the next step.
    

## 4. Create a OneSignal App

1. Open [OneSignal](https://app.onesignal.com/) and create an account.
    
2. Create a new application.
    
3. Select **Google Android (FCM)** because you want notifications in your Android APK.
    
4. Open **Settings → Keys & IDs** and copy the OneSignal App ID.
    

## 5. Connect Firebase to OneSignal

1. Open the [Firebase Console](https://console.firebase.google.com/) and create a project.
    
2. Add an Android app to the Firebase project.
    
3. Enter the exact Android package name copied from Median.co.
    
4. Register the app. Download `google-services.json` if you want to keep a copy for reference; it is not the service account file required by OneSignal.
    
5. Open **Project Settings → Service accounts**.
    
6. Generate a new private key and download the service account JSON file.
    
7. Return to OneSignal and open **Settings → Push & In-App → Google Android (FCM)**.
    
8. Upload the service account JSON file and save the configuration.


## Step 2 — Connect Firebase to OneSignal

This is the Android delivery setup. Firebase Cloud Messaging (FCM) allows OneSignal to deliver notifications to your Android devices.

![](https://www.google.com/s2/favicons?domain=https://docs.median.co&sz=32)

Median.co

![Firebase Tutorial: Getting Started | Kodeco](https://images.openai.com/static-rsc-4/grYr6NseMQ5_w9TslG3p0nGUVOnqbzcVUE90SGIi8TMjhRZ8ifzQJe8C_zcNfvRGzEBNK8S1O1j05Jnd6TzHvZ3n04sRkEGsS5omnRSME03oudr-Du3Hyz7us90UoVeWY6mO_MOHAuVyV3eUWgci5IE8dmtpPWLEXJzDlvjbm40?purpose=inline)

A. Create a Firebase project

Open the [Firebase Console](https://console.firebase.google.com/) and create a project.

![How to Create a Firebase Project and Generate an FCM Private Key File](https://images.openai.com/static-rsc-4/rQrSGH1mI-cHV8ZEvEy3ndoGtTV7hIJ4v7mOsxDjJ6Zaz0Er7blNtRz1sXXmbWgwPiD_kwz0dRNB_y-Qf0cEjDgA4q-kcsYKvTD9VYhA8ATAeEpjBLpxoPhMvfkrsf8fBE0N4ub3kqYTyeq5y5L2yFivt_xOssUsEQMWQk-HE1Y?purpose=inline)

B. Enable Firebase Cloud Messaging

Open Project Settings → Cloud Messaging and verify that the FCM API is enabled.

![Push Notifications in Android | Vonage Client SDK Documentation](https://images.openai.com/static-rsc-4/JUVdcXeglXkqgcupGgGq9zIdg9t51k8VPLcalUBAc_N4w_f0gt7yvovqBx9EuOztBbr5Ouc8HeQ1MVS_PPzf4ejsFdUuVr1-DmLmTSsbxvyMKYKfIBDey_1nQ-lEjRVIR8gIiwYtZ7zObXegvEfyCW47rX15NPlTOT4DtjD3xIg?purpose=inline)

C. Generate the service account JSON

Open Project Settings → Service accounts → Generate new private key. Download the JSON file and keep it private.

![Android Firebase credentials - OneSignal](https://images.openai.com/static-rsc-4/UV1fXGTKwOKHaHeSn-jESNZSn7jVmSpnhsBEPCGBjUrRckbcQaaubyNMHVaKH33Omd4KzE36mlp52ihIrFbSUYhsojEGh3QB7CRfV66mwU08JPT-ohyGw0RfimWyihlZdPbqJNYLmyMuiuZ0GvAxXeo5aRpiAfzknLxWA34TH0M?purpose=inline)

D. Upload it to OneSignal

In OneSignal, open Settings → Push & In-App → Google Android (FCM) and upload the JSON file.

**Important:** Keep the service account JSON file private. Never upload it to GitHub or include it in your frontend code.

## 6. Connect OneSignal to Median.co

1. Return to Median App Studio.
    
2. Open **Native Plugins → OneSignal**.
    
3. Paste the OneSignal App ID into the App ID field.
    
4. Save the configuration.
    
5. Rebuild your Android APK.
    

## 7. Test Push Notifications

1. Install the newly built APK on your Android phone.
    
2. Open the app and grant notification permission.
    
3. Verify that the device is subscribed in OneSignal.
    
4. Send a test notification from the OneSignal dashboard.
    
5. Check that the notification appears on your phone.
    

Once the test succeeds, you can send notifications to subscribed users through OneSignal.

## Official Links

- Median.co: [https://median.co/](https://median.co/)
    
- Median OneSignal Guide: [https://docs.median.co/docs/onesignal](https://docs.median.co/docs/onesignal)
    
- OneSignal: [https://app.onesignal.com/](https://app.onesignal.com/)
    
- Firebase Console: [https://console.firebase.google.com/](https://console.firebase.google.com/)
    

**Note:** Creating the app and entering the App ID is not enough by itself. Firebase FCM credentials must be configured, the updated APK must be installed, and notification permission must be granted before you can verify delivery.