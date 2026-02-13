---
title: "Lagbe E-commerce Platform"
excerpt: "E-commerce Platform that facilitates online shopping"
collection: portfolio
---

## Project Overview

[Web](https://github.com/mohtasimbh/Lagbe_E-commerce_Web) \
[App](https://github.com/mohtasimbh/Lagbe_E-commerce_App)

Lagbe is a full e-commerce solution that includes both a web storefront and a cross platform mobile app. The system allows users to browse products, manage carts, and interact with a modern shopping interface across devices.

## Overview

This project is split into two main parts:

- Lagbe E-commerce Web
- Lagbe E-commerce Mobile App

Both projects share the same product ecosystem and are designed to work together as a unified shopping platform.

## Lagbe E-commerce Web

### Description

A browser based e-commerce storefront optimized for responsive layouts. Users browse products, view product details, and interact with a shopping interface from desktop or mobile browsers.

### Features

- Product listing pages
- Product detail view
- Search and filtering
- Shopping cart interface
- Responsive design
- Ready to deploy static build

### Tech Stack

- Flutter Web build
- HTML wrapper
- JavaScript compiled output

### Web Project Structure

```
assets/         Static images and UI assets
canvaskit/      Flutter web canvas files
icons/          Web icons
index.html      Web entry file
main.dart.js    Compiled Flutter web script
manifest.json   Web manifest
version.json    Version metadata
```

### Run Web Locally

```
git clone https://github.com/mohtasimbh/Lagbe_E-commerce_Web.git
flutter build web
python3 -m http.server 8000
```

Open browser at:

```
http://localhost:8000
```

---

## Lagbe E-commerce Mobile App

### Description

A Flutter based mobile shopping app for Android and iOS. The app connects with Firebase services and provides a mobile optimized e-commerce experience.

### Features

- Product browsing with images
- Add to cart workflow
- Firebase authentication
- Firestore product storage
- Android support
- iOS support
- Responsive UI layout

### Tech Stack

- Flutter framework
- Dart
- Firebase Authentication
- Firestore database
- Provider state management

### Mobile Project Structure

```
android/        Android platform code
ios/            iOS platform code
lib/            App source code
assets/images/  Product and UI assets
functions/      Backend helpers
web/            Web build output
test/           Unit and widget tests
```

### Run Mobile App

```
git clone https://github.com/mohtasimbh/Lagbe_E-commerce_App.git
cd Lagbe_E-commerce_App
flutter pub get
flutter run
```

### Firebase Setup

- Create Firebase project
- Add Android and iOS apps
- Download config files
- Enable Authentication
- Enable Firestore

Files required:

- google-services.json
- GoogleService-Info.plist

## Development Ideas

- Payment gateway integration
- Order tracking
- User profiles
- Product categories
- Admin dashboard
- Backend API integration

## Contribution

Open an issue before major changes. Pull requests are welcome.

## License

Add your preferred license here.
