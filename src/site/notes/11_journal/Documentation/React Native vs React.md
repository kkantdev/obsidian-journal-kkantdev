---
{"dg-publish":true,"permalink":"/11-journal/documentation/react-native-vs-react/","dg-note-properties":{}}
---

# App Development Notes: React Native vs React

These notes are for your Obsidian knowledge base. They explain which framework to use, how offline and online features work, how to update an APK without reinstalling it, and how to build a Super Admin dashboard without using Next.js.

# 1. React Native — Building Android Apps

**React Native** is a framework for building mobile applications for Android and iOS using JavaScript or TypeScript and React concepts.

Example: WhatsApp-like messaging app, NCC Claret, attendance app or a college management app.

|Framework / Tool|What it does|
|---|---|
|React Native|Builds the mobile app interface and functionality.|
|Expo|Makes React Native development and native integrations easier.|
|EAS Build|Builds your project into an Android APK.|
|Expo Updates|Delivers compatible app-code updates without reinstalling the APK.|
|Supabase|Provides authentication, database and backend services.|
|Expo SQLite|Saves messages and other data locally on the phone.|
|Firebase Cloud Messaging (FCM)|Sends push notifications to Android devices.|
|Git + GitHub|Stores and tracks your project code.|

**Simple example:** I can build an NCC Android app using React Native + Expo, create an APK, and distribute it directly to students and teachers.

You do not need to publish the app on the Google Play Store to use this development approach.

## 2. How offline mode works in React Native

Think about WhatsApp: you open it without an internet connection and can still see messages that were previously downloaded.

This is called **offline-first functionality** when the app is designed to prioritize locally available data.

### Example: WhatsApp-like messaging

**When the internet is available:**

1. The app connects to its backend.
2. It retrieves messages.
3. It saves the messages in a local database.
4. It displays them on the screen.
5. New messages arrive through the app's synchronization or real-time communication system.

**When the internet is unavailable:**

1. The app opens using its installed code.
2. It reads previously saved messages from SQLite.
3. It displays those messages.
4. New cloud messages cannot arrive until connectivity returns.

**When the internet returns:**

1. The app reconnects to the backend.
2. It retrieves new messages and other changes.
3. It updates the local database.
4. The interface displays the latest information.

Important: An app cannot display a message that it has never downloaded or saved locally.

### Tools for offline mode

- **Expo SQLite:** Stores messages locally.
- **Supabase:** Stores messages in the cloud.
- **Expo Network:** Helps detect network connectivity.
- **React Native:** Displays the messages.

You must implement the local storage and synchronization logic yourself. These tools do not automatically make every feature work offline.

## 3. How online-only features work

Suppose your NCC application has an attendance feature for teachers.

You want the Attendance button to remain visible even when the internet is unavailable, but you don't want teachers to mark attendance offline.

You can implement the following behaviour:

|Feature|Offline behaviour|Online behaviour|
|---|---|---|
|Messages|Display previously saved messages|Synchronize new messages|
|Events|Display cached events if available|Fetch the latest events|
|Attendance|Show an internet-required message|Load and submit attendance|
|Profile|Display previously saved information|Fetch or update cloud information|
|Login|Existing session may remain available, subject to your security design|Authenticate or refresh the session|

**Important:** Hiding or disabling a button is not sufficient security. Your backend must independently verify the user's identity, role and permissions.

# 4. How to update an APK without reinstalling it

Suppose you have already distributed your NCC app to 300 students and teachers.

Later, you want to add an attendance feature.

You don't necessarily need to create and distribute a new APK.

### Tools you need

|Tool|Purpose|
|---|---|
|React Native + Expo|Develop the app and its features.|
|EAS Build|Create the original APK and future native builds.|
|EAS Update|Publish compatible JavaScript and asset updates.|
|VS Code|Write and modify the code.|
|Terminal|Publish updates using commands.|

### Step-by-step update process

**Step 1: Build the original APK.**

Develop your app, configure EAS Build and create the APK.

**Step 2: Distribute the APK.**

Send the APK to students and teachers for installation. They install it once.

**Step 3: Develop a new feature.**

Open your project in VS Code and create the attendance screen.

**Step 4: Test your changes.**

Make sure the attendance feature works with your existing native app and backend.

**Step 5: Publish the update.**

After configuring EAS Update, you can publish a compatible update from the terminal:

```
eas update --channel production --message "Add attendance feature"
```

**Step 6: Users receive the update.**

The app checks for compatible updates according to its configuration and downloads them. The updated code can be applied on a subsequent launch or restart.

Users generally don't need to reinstall the APK.

### Can you show an Update button and progress bar?

Yes. You can create a custom screen:

```
New Update Available!

Version 1.2
- Attendance feature added
- Bug fixes

       [Update Now]
```

When the user taps the button, your app can check for and download the update, then show a progress indicator or status messages.

For example:

```
Downloading update...

        65%

Please wait...
```

Once the update is ready, the app can reload to apply it.

The exact percentage is only possible if the download mechanism exposes suitable progress information. Otherwise, use a loading indicator and status messages.

Expo Updates provides the update mechanisms, but you must implement the custom interface and user-controlled update flow yourself.

### What changes require a new APK?

|Change|Usually requires a new APK?|
|---|---|
|Add a new screen|No|
|Add a button|No|
|Change colours or layout|No|
|Add attendance logic in JavaScript|No|
|Fix a JavaScript bug|No|
|Add a native Android library that isn't included in the installed APK|Yes|
|Change native Android configuration|Often yes|
|Change certain native permissions or services|Often yes|

**Important:** EAS Update works for compatible JavaScript and asset changes. The installed APK must already contain the required native functionality.

For your direct APK distribution, users can receive compatible OTA updates without visiting the Play Store. However, if a new native build is required, you will need to distribute that APK separately.

Official documentation:

- [EAS Build](https://docs.expo.dev/build/introduction/)
- [EAS Update](https://docs.expo.dev/eas-update/introduction/)

---

# 5. React — Building Web Applications

**React** is a JavaScript library for building web user interfaces.

Unlike React Native, a conventional React web app uses HTML, CSS and JavaScript to run in a web browser.

Example: A college website, online dashboard, admin panel or web-based management system.

### Tools commonly used with React

|Framework / Tool|What it does|
|---|---|
|React|Builds the web interface.|
|Vite|Creates and runs a React web project.|
|Vercel|Hosts the web application online.|
|Supabase|Provides authentication, database and backend services.|
|IndexedDB|Stores structured data locally in the browser.|
|Service worker|Can support offline web app functionality and caching.|
|Git + GitHub|Tracks and stores project code.|

### How offline mode works in React

Suppose you build a WhatsApp-like web app.

When the user is online:

1. React loads the interface.
2. The app retrieves messages from the backend.
3. Previously retrieved messages are saved in IndexedDB.
4. New messages arrive through real-time communication or synchronization.

When the user is offline:

1. The browser loads the cached application files, provided you have configured offline support.
2. React reads previously saved messages from IndexedDB.
3. The app displays those messages.
4. New messages become available when connectivity returns and synchronization resumes.

**React alone does not automatically provide offline support.** You must implement caching, local storage and synchronization.

### Can React become an Android APK?

Yes. You can use **Capacitor** to package your React web application as an Android app.

|Tool|Purpose|
|---|---|
|React|Builds the web interface.|
|Capacitor|Connects the web app to native Android functionality and packages it as an Android app.|
|Android Studio|Helps build and inspect the Android project.|
|Capgo|Can deliver compatible web-code updates to installed Capacitor apps.|
|SQLite plugin|Can provide local database storage.|
|Convex or Supabase|Provides the cloud backend.|

For your existing React projects, React + Capacitor may allow you to reuse more of your existing web code than rewriting the interface in React Native.

### React vs React Native

|Feature|React|React Native|
|---|---|---|
|Primary purpose|Web applications|Mobile applications|
|Main interface technology|HTML and CSS|Native mobile components|
|Runs in a browser|Yes|With web support, such as React Native Web|
|Builds an Android APK directly|No; use a wrapper such as Capacitor|Yes, through a native build process|
|Offline support|Must be implemented|Must be implemented|
|Compatible OTA updates|Possible with suitable tooling|Possible with Expo Updates|
|Good for|Websites and web dashboards|Android and iOS apps|

**Simple rule:** Use React for web-first projects and React Native for mobile-first projects. Use React + Capacitor when you want to turn an existing React web app into an Android app.

---

# 6. Building a Super Admin Dashboard Using React Native Only

This is particularly relevant to your NCC Claret application.

Suppose your college has 300 students and you want three roles:

- **Super Admin:** You manage the application.
- **Teacher:** Teachers manage their assigned students and attendance.
- **Student:** Students view messages, events and their permitted information.

You want to build the Android app and an admin dashboard without creating a separate Next.js project.

**Yes, you can do this with React Native + Expo, using Expo's web support and React Native Web.**

There are two approaches.

### Approach A: Put the dashboard inside the Android app

The Super Admin signs in to the same app and sees additional screens.

For example:

```
NCC Claret App
      |
      v
     Login
      |
      v
  Check User Role
      |
  +---+-----------+
  |       |       |
  v       v       v
Student Teacher Super Admin
  |       |       |
  v       v       v
Events  Attendance Manage Users
Messages Groups    Manage Events
Profile Reports    Manage College
```

Here, everyone installs the same APK, but each role gets a different interface.

**How to build it:**

1. Create one React Native + Expo project.
2. Build the login screen.
3. Authenticate users through Supabase Auth.
4. Store each user's role in your database.
5. After login, retrieve the user's permitted role and college membership.
6. Display the appropriate screens.
7. Protect every sensitive operation with backend authorization.

For example, students shouldn't be able to mark attendance simply by manually navigating to the teacher's screen.

**Advantages:**

- One APK to distribute.
- One project to maintain.
- All roles use the same application.
- No separate web dashboard is necessary.

**Limitation:** Managing many students, viewing large reports and editing data can be less convenient on a phone.

### Approach B: Build a separate web dashboard using the same React Native project

Suppose you want to manage your college from your laptop using a browser.

You can use Expo's web support to build a browser-based version of your application.

You do not have to use Next.js.

Your architecture could look like this:

```
              One Project
                   |
          React Native + Expo
                   |
            +------+------+
            |             |
            v             v
       Android App     Web App
            |             |
       Students and    Super Admin
        Teachers       Dashboard
            |             |
            +------+------+
                   |
                   v
                Supabase
              Shared Backend
```

Both versions can share authentication, database access and business logic, while using different interfaces for mobile and desktop.

### Step-by-step implementation

**Step 1: Create the project.**

Start with a React Native + Expo project and configure web support.

**Step 2: Separate the interfaces.**

Create mobile screens for students and teachers, and desktop-oriented screens for administration.

For example:

```
ncc-claret/
├── app/
│   ├── login.tsx
│   ├── student/
│   │   ├── index.tsx
│   │   └── events.tsx
│   ├── teacher/
│   │   ├── index.tsx
│   │   └── attendance.tsx
│   └── admin/
│       ├── index.tsx
│       ├── users.tsx
│       └── reports.tsx
├── components/
│   ├── mobile/
│   ├── dashboard/
│   └── shared/
├── services/
│   ├── auth.ts
│   └── database.ts
└── package.json
```

This is an example structure. You would organize the files according to your Expo Router setup.

**Step 3: Make the interfaces platform-specific where necessary.**

React Native supports platform-specific files, such as:

```
AdminDashboard.native.tsx
AdminDashboard.web.tsx
```

The native version can provide a mobile-friendly interface, while the web version can use a desktop sidebar, tables and wider reports.

Shared components and services can still be reused.

**Step 4: Connect both versions to Supabase.**

Both interfaces use the same backend, but Supabase must enforce the correct role and data permissions.

**Step 5: Build the Android APK.**

Use EAS Build to produce the Android application for distribution.

**Step 6: Build the web application.**

You can export the web version using:

```
npx expo export --platform web
```

You can then host the exported files on a suitable static hosting service, such as Vercel.

**Step 7: Use the right interface for each device.**

Students and teachers can use the Android app, while the Super Admin can access the web dashboard from a laptop.

You would still maintain one project, with platform-specific interfaces where needed.

---

# 7. Which approach should you choose for NCC Claret?

For your first release, I recommend keeping things simple.

|Requirement|My recommendation|
|---|---|
|Student app|React Native + Expo|
|Teacher app|Same React Native app|
|Super Admin on a phone|Same React Native app|
|Super Admin on a laptop|Add Expo Web support|
|Shared authentication|Supabase Auth|
|Shared database|Supabase PostgreSQL|
|Android APK|EAS Build|
|Compatible updates|Expo Updates|
|Offline messages|Expo SQLite|
|Push notifications|Firebase Cloud Messaging|

### Your development plan

1. Build one mobile app with login and role-based screens.
2. Implement students, teachers and Super Admin.
3. Connect the app to Supabase.
4. Add cloud-based attendance and events.
5. Add offline message storage if required.
6. Build and distribute the APK.
7. Add the web dashboard when you need to manage the application from a laptop.

**Final takeaway:** You can use React Native + Expo for your Android app and its web dashboard without Next.js. Use one project, share the backend and common logic, and create separate interfaces where the mobile and desktop experiences require different designs.