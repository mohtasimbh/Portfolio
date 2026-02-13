---
title: "devChat-App"
excerpt: "Flutter Video Chat App"
collection: portfolio
---

## Project Overview

# Flutter Video Chat App

## [Project Link](https://github.com/mohtasimbh/devChat-App)

A full featured Flutter chat application with video, voice, text, images, emoji, and real time notifications.

## Description

This project is a real time chat app built with Flutter. It supports video calling, voice calling, text messaging, and media sharing. Users receive call notifications even when the app is closed. Custom ringtone playback runs on both caller and receiver devices.

The app connects Flutter with Firebase, Agora SDK, and a Laravel backend to handle messaging, calling, user management, and push notifications.

## Core Features

- One to one video calling
- One to one voice calling
- Real time text messaging
- Image sharing
- Stickers and emoji support
- Local chat database
- Remote sync with backend
- Call notifications with ringtone
- Accept or reject incoming calls
- Notifications when app is closed
- Phone number verification
- Message counter notifications
- Chat duration tracking
- Multi line message input
- Auto hide message box
- Audio and video call controls

## Tech Stack

- Flutter
- Firebase Authentication
- Firebase Cloud Messaging
- Firebase Firestore
- Agora Video SDK
- Laravel backend
- MySQL database
- PHP Firebase Admin SDK

## Project Setup

### Flutter App

1. Clone the repository

   ```
   git clone <repo-url>
   cd project-folder
   ```

2. Install dependencies

   ```
   flutter pub get
   ```

3. Run the app

   ```
   flutter run
   ```

iOS requires:

```
cd ios
pod install
```

### Firebase Setup

- Create a Firebase project
- Connect Android and iOS apps
- Add SHA1 and SHA256 keys
- Enable Authentication
- Enable Firestore
- Enable Cloud Messaging
- Download configuration files

### Agora Setup

- Create an Agora developer account
- Generate App ID and certificate
- Replace keys inside the project

### Laravel Backend Setup

Backend handles user tracking and notification routing.

Requirements:

- Domain with SSL
- PHP 7.4 or higher
- MySQL 5.7 or higher

Steps:

1. Install Laravel backend
2. Configure database
3. Add Firebase Admin SDK credentials
4. Configure SSL domain
5. Start backend server

## Notification Flow

Call and message notifications follow this path:

App → Laravel server → Firebase → Target user

This setup ensures delivery even when the app is terminated.

## Why Use Third Party SDK

Video streaming requires stable infrastructure, encoding, and global routing. Building this stack from scratch requires large server resources and deep WebRTC expertise.

Agora provides:

- Global low latency routing
- Video encoding and decoding
- Reliable call stability
- Cross platform support

This reduces infrastructure cost and development time.

## Screenshots

![App UI](https://user-images.githubusercontent.com/61247278/223838120-25545547-53f8-43ee-a746-6f42b2a7e0ba.jpg)
![App UI](https://user-images.githubusercontent.com/61247278/223838152-73d318f3-4b65-4d29-8c7c-871ab4f63e29.jpg)
![App UI](https://user-images.githubusercontent.com/61247278/223838091-5acc625f-2a9a-47b6-af18-f95a3c1c772e.jpg)
![App UI](https://user-images.githubusercontent.com/61247278/223828037-3080bd0e-3197-435d-b5a2-e63960f7884a.jpg)

## Contribution

Open an issue before major changes. Pull requests are welcome.

## License

Add your preferred license here.---
title: "devChat-App"
excerpt: "Flutter Video Chat App"
collection: portfolio
---

## Project Overview

# Flutter Video Chat App

## [Project Link](https://github.com/mohtasimbh/devChat-App)

A full featured Flutter chat application with video, voice, text, images, emoji, and real time notifications.

## Description

This project is a real time chat app built with Flutter. It supports video calling, voice calling, text messaging, and media sharing. Users receive call notifications even when the app is closed. Custom ringtone playback runs on both caller and receiver devices.

The app connects Flutter with Firebase, Agora SDK, and a Laravel backend to handle messaging, calling, user management, and push notifications.

## Core Features

- One to one video calling
- One to one voice calling
- Real time text messaging
- Image sharing
- Stickers and emoji support
- Local chat database
- Remote sync with backend
- Call notifications with ringtone
- Accept or reject incoming calls
- Notifications when app is closed
- Phone number verification
- Message counter notifications
- Chat duration tracking
- Multi line message input
- Auto hide message box
- Audio and video call controls

## Tech Stack

- Flutter
- Firebase Authentication
- Firebase Cloud Messaging
- Firebase Firestore
- Agora Video SDK
- Laravel backend
- MySQL database
- PHP Firebase Admin SDK

## Project Setup

### Flutter App

1. Clone the repository

   ```
   git clone <repo-url>
   cd project-folder
   ```

2. Install dependencies

   ```
   flutter pub get
   ```

3. Run the app

   ```
   flutter run
   ```

iOS requires:

```
cd ios
pod install
```

### Firebase Setup

- Create a Firebase project
- Connect Android and iOS apps
- Add SHA1 and SHA256 keys
- Enable Authentication
- Enable Firestore
- Enable Cloud Messaging
- Download configuration files

### Agora Setup

- Create an Agora developer account
- Generate App ID and certificate
- Replace keys inside the project

### Laravel Backend Setup

Backend handles user tracking and notification routing.

Requirements:

- Domain with SSL
- PHP 7.4 or higher
- MySQL 5.7 or higher

Steps:

1. Install Laravel backend
2. Configure database
3. Add Firebase Admin SDK credentials
4. Configure SSL domain
5. Start backend server

## Notification Flow

Call and message notifications follow this path:

App → Laravel server → Firebase → Target user

This setup ensures delivery even when the app is terminated.

## Why Use Third Party SDK

Video streaming requires stable infrastructure, encoding, and global routing. Building this stack from scratch requires large server resources and deep WebRTC expertise.

Agora provides:

- Global low latency routing
- Video encoding and decoding
- Reliable call stability
- Cross platform support

This reduces infrastructure cost and development time.

## Screenshots

![App UI](https://user-images.githubusercontent.com/61247278/223838120-25545547-53f8-43ee-a746-6f42b2a7e0ba.jpg)
![App UI](https://user-images.githubusercontent.com/61247278/223838152-73d318f3-4b65-4d29-8c7c-871ab4f63e29.jpg)
![App UI](https://user-images.githubusercontent.com/61247278/223838091-5acc625f-2a9a-47b6-af18-f95a3c1c772e.jpg)
![App UI](https://user-images.githubusercontent.com/61247278/223828037-3080bd0e-3197-435d-b5a2-e63960f7884a.jpg)

## Contribution

Open an issue before major changes. Pull requests are welcome.

## License

Add your preferred license here.
