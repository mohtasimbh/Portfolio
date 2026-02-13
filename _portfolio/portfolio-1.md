---
title: "IMAGEN"
excerpt: "Image Generator AI From Text"
collection: portfolio
---

**[Project Link](https://github.com/mohtasimbh/ImaGen)**

## Project Overview

AI powered text to image generator mobile app

## Description

ImaGen is a cross platform mobile app that turns text prompts into images using an AI backend. The project combines a Flutter frontend with a server side image generation service. It targets Android and iOS from a single codebase.

## Screenshots

![Capture1](https://user-images.githubusercontent.com/61247278/214334949-5b2d095d-c928-446c-89a6-5665289493b6.PNG)
![Capture2](https://user-images.githubusercontent.com/61247278/214334968-10e50e33-ee44-4e3e-b54d-6fa937247162.PNG)
![Capture3](https://user-images.githubusercontent.com/61247278/214334973-e69eb08c-07ee-4e46-bf5e-b6dfdc6a5be9.PNG)
![Capture4](https://user-images.githubusercontent.com/61247278/214334979-33e4cd4f-0872-48b2-b482-0691773677dd.PNG)
![Capture5](https://user-images.githubusercontent.com/61247278/214334983-94b3b8b4-dbbc-41bf-90d7-d7c03571416a.PNG)
![Capture6](https://user-images.githubusercontent.com/61247278/214334986-8200f683-bb93-4c19-909d-9c0536d1ecc2.PNG)
![Capture7](https://user-images.githubusercontent.com/61247278/214334989-3f258610-5717-4d41-8f69-d3084989a508.PNG)
![Capture8](https://user-images.githubusercontent.com/61247278/214334997-af5314c6-bb17-4785-a0ce-6a7a5ba581bb.PNG)
![Capture9](https://user-images.githubusercontent.com/61247278/214335003-79514709-84be-4e94-9caa-6413bdc70263.PNG)
![1](https://user-images.githubusercontent.com/61247278/214335242-43bf27dc-5cfa-4900-86d0-3cdb3d21b4f0.PNG)

## Features

- Text prompt to image generation
- Android and iOS support
- Shared Flutter UI and business logic
- Backend service for AI processing
- Local caching and network layer
- Basic test coverage

## Project Structure

```
android/     Android platform code
ios/         iOS platform code
lib/         Flutter UI and core logic
server/      Backend image generation service
assets/      Fonts and static resources
images/      Sample images and UI assets
test/        Unit and integration tests
```

## Tech Stack

- Flutter
- Dart
- Python backend service
- Provider for state management
- Dio for network requests
- Hive for local storage

## Installation

1. Clone the repository

   ```
   git clone https://github.com/mohtasimbh/ImaGen.git
   cd ImaGen
   ```

2. Install dependencies

   ```
   flutter pub get
   ```

3. Start the backend server

   ```
   cd server
   python main.py
   ```

4. Run the mobile app

   ```
   flutter run
   ```

## Usage

1. Launch the app on a device or emulator
2. Enter a text prompt
3. Tap the generate button
4. Wait for the image result

## Development Goals

- Improve prompt controls
- Add advanced generation settings
- Expand test coverage
- Optimize performance
- Improve UI polish

## Contribution

Pull requests are welcome. Open an issue first to discuss major changes.

## License

Add your preferred license here.
