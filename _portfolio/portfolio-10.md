---
title: "devChat-App"
excerpt: "Flutter Video Chat App"
collection: portfolio
---

## Project Overview

## [Project Link](https://github.com/mohtasimbh/devChat-App)

## Description

Previouly we built a flutter chatting app mostly text and image based. This time we will build a new chatting app using flutter framework. This will include some cool features which covers both video and voice calling along with text and image sending as well as emoji.

Another main feature of this app is that, you can notification both for audio and video calling. If someone called you you will get notification and the other person will have to wait until you receive it. Both end will have calling sound. It's custom sound.

This chat app is also included here in this study app source code.

## Get Started

- Clone this repository
- Run `flutter packages get`
- Run `flutter run` (remember to open simulator or connect physical device, iOS auto run additional command `pod install`)

## Cool features of the app

- Video chat
- Voice chat
- Text chat
- Sending images
- Sending stickers
- Save chat in the local database
- Sync local database with remote database
- Both laravel and firebase backend
- Notification is send first as you do video
- Notification number and icons based on your chat message number
- Notification is received even if the app is killed
- User need to tap on the button to accept the video call
- Notification is send first as you do voice call
- There's sound on the other side as you call
- Caller also can hear the sound
- Every text message has notification
- Call ends automitically as you hang up the call
- Phone number message verification
- Multi line mesagge box as you type more
- Auto hide of message box as you are done
- Show chat time duration
- Audio video controller (buttons)

## ChatApp UI

![App UI](https://user-images.githubusercontent.com/61247278/223838120-25545547-53f8-43ee-a746-6f42b2a7e0ba.jpg)

## Technology used in this app

- Flutter framework
- Firebase service
- Agora SDK
- Laravel framework

The whole architecture is based on Flutter framework. We used Firebase service for chatting and storing user chat information including texts and images.

We used Agora SDK for video chat and voice chat.

We used Laravel Framework for basic backend service and where you can video basic user data.

![App UI](https://user-images.githubusercontent.com/61247278/223838152-73d318f3-4b65-4d29-8c7c-871ab4f63e29.jpg)

## App Deployment Locally

1. create a new flutter project.
2. copy all the files and folers like lib, assets and pubspec.yaml from the downloaded project in your new project.
3. make sure you create a firebase project with above project from terminal.
4. you need to make sure you connect this app with your own firebase project.
5. make sure you generate SHA1 and SHA256 key with your project.
6. create an account with Agora video sdk.
7. install the laravel application.
8. make sure that you have SSL with your domain.
9. make sure you replace the App ID and App Certificate.

## Laravel Backend

The backend is mostly used for to know how many users do you have and who they are. You may also maintain them from there.

![App UI](https://user-images.githubusercontent.com/61247278/223838032-1b5cb9ca-23a1-4743-91b5-0599f2f3bdd5.png)

Backend installation requirement

1. Prepare a domain
2. Have it with SSL
3. PHP verion 7.4 or higher
4. MySQL version 5.7 or higher

## Notification

See how notification works. It should be coming from your app to your server to your firebase account to your user. For this reason we have integrated Firebase Admin SDK with PHP.

![App UI](https://user-images.githubusercontent.com/61247278/223838091-5acc625f-2a9a-47b6-af18-f95a3c1c772e.jpg)

## Why use third party SDK

The reason why we use third party SDK to do it, because Flutter does not provide any higher level API to connect with video technology like WebRTC.

If a small team or some students try to do it, it would be almost very difficult to get the job done. Even if they do it, the video signal would be very bad and shaky. Apart from them they have to build up their own server to send the video signals to different users in different country.

They also need to spend thousands of dollars for building servers and decoding the signal.

Third party SDK solves these problems since they are dedicated to do it and they have a very big team to get the job done.

In this app, the way used it here is an example. It requires PHP and Agora integration.

![App UI](https://user-images.githubusercontent.com/61247278/223828037-3080bd0e-3197-435d-b5a2-e63960f7884a.jpg)

## Feedback

If you have any feedback, please reach out to me at shakilwell0@gmail.com
