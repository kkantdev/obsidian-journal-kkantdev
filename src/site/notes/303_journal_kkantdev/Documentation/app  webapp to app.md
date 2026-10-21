---
{"dg-publish":true,"permalink":"/303-journal-kkantdev/documentation/app-webapp-to-app/","dg-note-properties":{}}
---

# App Development Notes: React Native vs React

These notes explain how to choose between React Native and React, how offline and online features work, how to update an Android APK without reinstalling it, and how to build a Super Admin dashboard without using Next.js.

**Example project:** A College Mobile App where students receive college announcements, read messages, view events, and access other college services. Teachers manage permitted activities, while administrators manage users and features.

# 1. React Native — Building Android Apps

**React Native** is a framework for building mobile applications for Android and iOS using JavaScript or TypeScript and React concepts.

**Examples:** A college mobile app, messaging app, attendance app, or college management app.

|Framework / Tool|What it does|
|---|---|
|React Native|Builds the mobile app interface and functionality.|
|Expo|Makes React Native development and native integrations easier.|
|EAS Build|Builds the project into an Android APK or other supported build formats.|
|Expo Updates|Delivers compatible app-code updates without reinstalling the APK.|
|Supabase|Provides authentication, database, and backend services.|
|Expo SQLite|Saves messages and other data locally on the phone.|
|Firebase Cloud Messaging (FCM)|Sends push notifications to Android devices.|
|Git + GitHub|Stores and tracks project code.|

**Example:** I can build a College Mobile App using React Native and Expo, create an APK, and distribute it directly to students, teachers, and administrators.

The app does not need to be published on the Google Play Store to use this development approach.

---

# 2. How Offline Mode Works in React Native

Think about a messaging app: you open it without an internet connection and can still see messages that were previously downloaded.

This is called **offline-first functionality** when the application is designed to prioritize locally available data.

### Example: College Messaging

Suppose the college sends students announcements about holidays, examinations, events, and other activities.

**When the internet is available:**

1. The app connects to its backend.
2. It retrieves college announcements and messages.
3. It saves the messages in a local database.
4. It displays the messages on the screen.
5. When the college publishes a new announcement, the app can synchronize the new information.

**When the internet is unavailable:**

1. The app opens using its installed code.
2. It reads previously saved messages from SQLite.
3. It displays the saved messages.
4. New cloud messages cannot arrive until connectivity returns.

**When the internet returns:**

1. The app reconnects to the backend.
2. It retrieves new announcements and other changes.
3. It updates the local database.
4. The interface displays the latest information.

**Important:** An app cannot display a message that it has never downloaded or saved locally.

### Tools for offline mode

- **Expo SQLite:** Stores messages locally.
- **Supabase:** Stores messages in the cloud.
- **Expo Network:** Helps detect network connectivity.
- **React Native:** Displays the messages.

You must implement local storage and synchronization yourself. These tools do not automatically make every feature work offline.

---

# 3. How Online-Only Features Work

Suppose your College Mobile App has an attendance feature for teachers.

You want the Attendance button to remain visible even when the internet is unavailable, but you do not want teachers to submit attendance offline.

You can implement the following behaviour:

|Feature|Offline behaviour|Online behaviour|
|---|---|---|
|College messages|Display previously saved messages|Synchronize new messages|
|College announcements|Display cached announcements, if available|Fetch the latest announcements|
|Attendance|Show an internet-required message|Load and submit attendance|
|College events|Display cached events, if available|Fetch the latest event information|
|Profile|Display previously saved information|Fetch or update cloud information|
|Login|An existing session may remain available, subject to the security design|Authenticate or refresh the session|

**Security note:** Hiding or disabling a button is not sufficient security. The backend must independently verify the user's identity, role, and permissions.

For example, a student must not be able to submit attendance simply by modifying the app or making a direct API request.

---

# 4. How to Update an APK Without Reinstalling It

Suppose you have already distributed your College Mobile App to 300 students and teachers.

Later, the college wants to introduce a new feature, such as attendance tracking or an examination timetable.

**You do not necessarily need to create and distribute a new APK.** Compatible JavaScript and asset changes can be delivered through an over-the-air (OTA) update.

### Tools you need

|Tool|Purpose|
|---|---|
|React Native + Expo|Develop the mobile application.|
|EAS Build|Create the original APK and future native builds.|
|EAS Update|Publish compatible JavaScript and asset updates.|
|VS Code|Write and modify the code.|
|Terminal|Publish updates using commands.|

### Step-by-step update process

**Step 1: Build the original APK.**

Develop the application, configure EAS Build, and create the APK.

**Step 2: Distribute the APK.**

Provide the APK to students and teachers. They install it on their Android devices.

**Step 3: Develop a new feature.**

Suppose the college wants a new examination timetable screen. Open the project in VS Code and implement the screen.

**Step 4: Test your changes.**

Verify that the feature works with the existing native application and backend.

**Step 5: Publish the update.**

After configuring EAS Update, publish a compatible update from the terminal:

```
eas update --channel production --message "Add examination timetable"
```

**Step 6: Users receive the update.**

The app checks for compatible updates according to its configuration and downloads them. The updated code can be applied on a subsequent launch or restart.

Users generally do not need to reinstall the APK for compatible updates.

### Can you show an Update button and progress indicator?

Yes. You can build a custom update screen in the application.

For example:

```
New Update Available!

Version 1.2

What's New?
- Examination timetable added
- Improved college announcements
- Bug fixes

          [Update Now]
```

When the user taps **Update Now**, your app can check for and download the update, then display a progress indicator or status messages.

For example:

```
Downloading update...

       Please wait...
```

Once the update is ready, the app can reload to apply it.

**Important:** Do not assume that an exact download percentage is available. Display a percentage only if the download mechanism exposes suitable progress information. Otherwise, use a loading indicator and status messages.

Expo Updates provides the update mechanisms, but you must implement the custom interface and user-controlled update flow yourself.

### What changes require a new APK?

|Change|Usually requires a new APK?|
|---|---|
|Add a new screen using existing native capabilities|No|
|Add a button|No|
|Change colours or layout|No|
|Add attendance logic in JavaScript|No, provided the required native functionality already exists|
|Fix a JavaScript bug|No|
|Add a native Android library that is not included in the installed APK|Yes|
|Change native Android configuration|Often yes|
|Add certain native permissions or services|Often yes|

**Important:** OTA updates cannot introduce arbitrary new native Android functionality into an already installed APK. If a feature requires native changes, you must build and distribute a new APK.

For direct APK distribution, compatible OTA updates can work without the Google Play Store, provided the application and update configuration are set up correctly.

Official documentation:

- [EAS Build](https://docs.expo.dev/build/introduction/)
- [EAS Update](https://docs.expo.dev/eas-update/introduction/)

---

# 5. React — Building Web Applications

**React** is a JavaScript library for building web user interfaces.

Unlike React Native, a conventional React web app uses HTML, CSS, and JavaScript to run in a web browser.

**Examples:** A college website, online administration dashboard, student portal, or web-based management system.

### Tools commonly used with React

|Framework / Tool|What it does|
|---|---|
|React|Builds the web interface.|
|Vite|Creates and runs a React web project.|
|Vercel|Hosts the web application online.|
|Supabase|Provides authentication, database, and backend services.|
|IndexedDB|Stores structured data locally in the browser.|
|Service worker|Can support offline web app functionality and caching.|
|Git + GitHub|Tracks and stores project code.|

### How offline mode works in React

Suppose you build a web-based college messaging portal.

**When the user is online:**

1. React loads the interface.
2. The app retrieves college messages from the backend.
3. Previously retrieved messages are saved in IndexedDB.
4. New messages arrive through real-time communication or synchronization.

**When the user is offline:**

1. The browser loads cached application files, provided offline support has been configured.
2. React reads previously saved messages from IndexedDB.
3. The app displays those messages.
4. New messages become available when connectivity returns and synchronization resumes.

**Important:** React alone does not automatically provide offline support. You must implement caching, local storage, and synchronization.

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

For existing React projects, React + Capacitor may allow you to reuse more web code than rewriting the interface in React Native.

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

**Simple rule:** Use React for web-first projects and React Native for mobile-first projects. Use React + Capacitor when you want to package an existing React web app as an Android app.

---

# 6. Building a Super Admin Dashboard Without Next.js

Suppose your College Mobile App serves approximately 300 students and teachers.

You want three roles:

- **Super Admin:** Manages the overall application.
- **Teacher:** Manages permitted activities, such as attendance.
- **Student:** Reads college announcements, views events, and accesses permitted information.

You want to build the Android app and an administration dashboard without creating a separate Next.js project.

**Yes, you can use React Native + Expo with Expo's web support and React Native Web.**

There are two main approaches.

## Approach A: Put the Dashboard Inside the Android App

The Super Admin signs in to the same application and sees additional screens.

For example:

```
             College Mobile App
                      |
                      v
                    Login
                      |
                      v
                 Check Role
                      |
              +-------+-------+
              |       |       |
              v       v       v
           Student  Teacher  Super Admin
              |       |       |
              v       v       v
           Messages Attendance Manage Users
           Events    Groups    Manage Events
           Profile   Classes   View Reports
```

Everyone installs the same APK, but each role receives a different interface.

### How to build it

1. Create one React Native + Expo project.
2. Build the login screen.
3. Authenticate users through Supabase Auth.
4. Store role and college-membership information in the database.
5. Retrieve the user's permitted role and college membership after login.
6. Display the appropriate screens.
7. Protect every sensitive operation with backend authorization.

For example, students should not be able to access teacher-only attendance operations simply by navigating to a teacher's screen.

### Advantages

- One APK to distribute.
- One project to maintain.
- All roles use the same application.
- No separate web dashboard is necessary.

**Limitation:** Managing hundreds of users, viewing large reports, and editing lots of data can be less convenient on a phone.

## Approach B: Build a Web Dashboard Using the Same Project

Suppose you want to manage the college application from your laptop using a browser.

You can use Expo's web support to build a browser-based version of the application.

**You do not have to use Next.js.**

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
                v             v
          Students and    Super Admin
           Teachers       Dashboard
                |             |
                +------+------+
                       |
                       v
                    Supabase
                  Shared Backend
```

Both versions can share authentication, database access, and business logic while using different interfaces.

### Step-by-step implementation

**Step 1: Create the project.**

Start with a React Native + Expo project and configure web support.

**Step 2: Organize the interfaces.**

Create mobile screens for students and teachers, and desktop-oriented screens for administration.

Example project structure:

```
college-mobile-app/
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

This is an example structure; the exact organization depends on your Expo Router configuration.

**Step 3: Create platform-specific interfaces where necessary.**

React Native supports platform-specific files, such as:

```
AdminDashboard.native.tsx
AdminDashboard.web.tsx
```

The native version can provide a mobile-friendly interface, while the web version can use a desktop sidebar, tables, and wider reports.

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

**Step 7: Use the appropriate interface for each device.**

Students and teachers can use the Android app, while the Super Admin can access the web dashboard from a laptop.

You maintain one project with platform-specific interfaces where needed.

---

# 7. Supporting Multiple Colleges in the Future

Suppose you initially build the application for one college. Later, another college wants to use the same system.

You do not necessarily need to create a separate project for every college.

You can build **one application that supports multiple colleges**, with each college's data logically separated in the backend.

### Example

```
              College Mobile App
                       |
                       v
                    Login
                       |
                       v
                Identify College
                       |
             +---------+---------+
             |                   |
             v                   v
         College A            College B
             |                   |
       +-----+-----+       +-----+-----+
       |     |     |       |     |     |
       v     v     v       v     v     v
     Admin Teacher Student Admin Teacher Student
```

Each user should only access the college data and features they are authorized to use.

### Example database structure

|Table|Purpose|
|---|---|
|`colleges`|Stores college information.|
|`profiles`|Stores user profile information.|
|`college_memberships`|Connects users to colleges and their roles.|
|`groups`|Stores classes, departments, or groups.|
|`announcements`|Stores college announcements.|
|`events`|Stores college events.|
|`attendance`|Stores attendance records.|

For example, every announcement can be associated with a `college_id`. The backend then checks whether the signed-in user is authorized to access that college's announcements.

**Important security requirement:** Do not rely on the user interface to isolate college data. Enforce access rules in the backend using appropriate Supabase Row Level Security (RLS) policies and server-side authorization.

This approach lets you add colleges without duplicating the entire application.

---

# 8. Which Approach Should You Choose?

For a college mobile application, I recommend starting with a simple architecture and expanding it when necessary.

|Requirement|Recommended approach|
|---|---|
|Student mobile app|React Native + Expo|
|Teacher mobile app|Same React Native app|
|Super Admin using a phone|Same React Native app with additional role-based screens|
|Super Admin using a laptop|Expo Web or a separate React web dashboard|
|Shared authentication|Supabase Auth|
|Shared database|Supabase PostgreSQL|
|Android APK|EAS Build|
|Compatible code updates|Expo Updates|
|Offline messages|Expo SQLite|
|Push notifications|Firebase Cloud Messaging|
|Multiple colleges|Shared backend with college-specific authorization|
|Code version control|Git + GitHub|

### Suggested development plan

1. Build the mobile app with login and role-based screens.
2. Implement student, teacher, and Super Admin functionality.
3. Connect the application to Supabase.
4. Add college announcements, events, and attendance.
5. Implement offline message storage if required.
6. Configure push notifications.
7. Build and distribute the APK.
8. Add compatible OTA updates.
9. Add a web dashboard when laptop-based administration becomes necessary.
10. Introduce multi-college support when the application needs it.

You do not need to implement every feature in the first release.

---

# 9. Final Takeaways

- **React Native + Expo:** Best suited to a mobile-first application for Android and iOS.
- **React:** Best suited to conventional web applications and browser-based dashboards.
- **React + Capacitor:** Useful when you want to package an existing React website as a mobile app.
- **Electron:** Used to build desktop applications for Windows, macOS, and Linux.
- **Expo SQLite:** Can store previously downloaded messages and other information locally.
- **Expo Updates:** Can deliver compatible JavaScript and asset updates without reinstalling the APK.
- **Supabase:** Can provide shared authentication and database services for mobile and web applications.
- **Expo Web:** Lets you build a browser-based interface using supported React Native components without requiring Next.js.
- **Backend authorization:** Protects user roles, college data, and sensitive operations.

**The main idea:** You can build a College Mobile App with React Native + Expo, distribute its APK directly, support offline access to previously saved messages, and add compatible features through OTA updates. You can later add a browser-based Super Admin dashboard and support multiple colleges without maintaining an entirely separate application for each one.