---
title: Local Development Setup
tags: [mobile-app]
---

# Local Development Setup

## Prerequisites

Before setting up the Plum Village App locally, ensure you have:

- **Node.js** (LTS version recommended)
- **Yarn** package manager
- **Git** for version control
- **macOS** (required for iOS development)
- **Xcode** (for iOS development)
- **Android Studio** (for Android development)
- **Ruby** (for iOS CocoaPods)

## Initial Setup

Complete these steps once to set up your development environment:

### 1. Set Up React Native Environment

Follow the [React Native CLI Quickstart](https://reactnative.dev/docs/getting-started-without-a-framework) guide:
- Select your development OS and target platform(s)
- Skip the "Creating a new application" section
- Install required dependencies if not already present

### 2. Clone the Repository

```bash
git clone https://github.com/plumvillage/plumvillage-app.git
cd plumvillage-app
```

### 3. Install Dependencies

```bash
yarn install
```

## Platform-Specific Setup

### iOS Setup (macOS Only)

1. **Install Ruby version** (if needed):
   ```bash
   ruby --version
   # If version mismatch, install required Ruby version
   rbenv install  # or your Ruby version manager equivalent
   ```

2. **Install CocoaPods dependencies**:
   ```bash
   yarn pod-install
   ```

3. **Add Firebase configuration**:
   - Download `GoogleService-Info.plist` from Firebase Console
   - Place it at `ios/GoogleService-Info.plist`

### Android Setup

1. **Generate signing key**:
   ```bash
   # Follow React Native signing key guide
   keytool -genkeypair -v -storetype PKCS12 -keystore my-release-key.keystore -alias my-key-alias -keyalg RSA -keysize 2048 -validity 10000
   ```

2. **Configure keystore**:
   - Move `my-release-key.keystore` to `android/app/`
   - Create `android/keystore.properties`:
     ```
     storePassword=YOUR_STORE_PASSWORD
     keyPassword=YOUR_KEY_PASSWORD
     keyAlias=my-key-alias
     storeFile=my-release-key.keystore
     ```

3. **Add Firebase configuration**:
   - Download `google-services.json` from Firebase Console
   - Place it at `android/app/google-services.json`

## Running the App

Once setup is complete, you can run the app on simulators or physical devices.

:::info The app is configured to point to production firebase services by default. If you wish to point the app to local firestore and auth emulators, follow [Pointing app to emulators](#pointing-app-to-emulators).

### iOS

```bash
yarn ios
```

- Opens iOS Simulator automatically
- Use Xcode for different simulator models or physical devices
- Requires macOS and Xcode

### Android

```bash
yarn android
```

- Starts Android emulator automatically
- Will also run on a real device if connected and paired for development

### Pointing app to emulators

- Start firestore and auth emulators. Refer [plumvillage-firebase repo](https://github.com/plumvillage/plumvillage-firebase).

- `yarn start:dev`

- In a new terminal, `yarn ios` or `yarn android`.

## Troubleshooting

### Common Issues

- **Metro bundler issues**: Try `yarn start --reset-cache`
- **iOS build failures**: Clean build folder in Xcode
- **Android signing errors**: Verify keystore.properties paths
- **Pod install errors**: Try `cd ios && pod install --repo-update`

### Getting Help

If you encounter issues:
1. Check the [React Native troubleshooting guide](https://reactnative.dev/docs/troubleshooting)
2. Search existing issues in the repository
3. Create a new issue with detailed error information
