# Myclaw Build Setup Guide

## Prerequisites

### For Android Development
```bash
# Install Flutter (if not already installed)
# Download from: https://flutter.dev/docs/get-started/install

# Verify installation
flutter doctor

# Install required components
flutter pub global activate fvm  # Flutter Version Manager (optional)
```

### For iOS Development (macOS only)
```bash
# Install Xcode Command Line Tools
xcode-select --install

# Install CocoaPods
sudo gem install cocoapods

# Setup iOS development
cd ios
pod repo update
pod install
cd ..
```

## Configuration Steps

### 1. Clone Repository
```bash
git clone https://github.com/kevinnexzen-sys/Myclaw-.git
cd Myclaw-
```

### 2. Get Dependencies
```bash
flutter pub get
```

### 3. Environment Setup
Create a `.env` file in the root directory:
```
SUPABASE_URL=your_supabase_url
SUPABASE_ANON_KEY=your_supabase_anon_key
GOOGLE_API_KEY=your_google_api_key
GROQ_API_KEY=your_groq_api_key
```

### 4. Generate Code
```bash
# Generate necessary code files
flutter pub run build_runner build --delete-conflicting-outputs
```

## Building for Android

### Development Build
```bash
flutter run
```

### Release APK (Single)
```bash
flutter build apk --release
# Output: build/app/outputs/flutter-apk/app-release.apk
```

### Release APK (Split by ABI)
```bash
flutter build apk --release --split-per-abi
# Outputs:
# - app-arm64-v8a-release.apk (64-bit ARM)
# - app-armeabi-v7a-release.apk (32-bit ARM)
# - app-x86_64-release.apk (x86-64)
```

### Android App Bundle (For Play Store)
```bash
flutter build appbundle --release
# Output: build/app/outputs/bundle/release/app-release.aab
```

## Building for iOS

### Development Build
```bash
flutter run -d ios
```

### Release Build
```bash
flutter build ios --release
# Output: build/ios/iphoneos/Runner.app
```

### Create IPA (For TestFlight/Distribution)
```bash
flutter build ipa --release
# Output: build/ios/iphoneos/Runner.ipa
```

## GitHub Actions CI/CD

The repository includes automated workflows that:

1. **Build Android APK** on every push to main/Myclaw branches
2. **Build iOS** on every push to main/Myclaw branches
3. **Create Releases** with built artifacts
4. **Auto-upload** APKs and AABs to release pages

### Manual Workflow Trigger
1. Go to GitHub Actions tab
2. Select "Build and Release Android APK"
3. Click "Run workflow"
4. Select branch (main or Myclaw)

## Code Signing (Optional)

### Android Signing
```bash
# Create keystore
keytool -genkey -v -keystore ~/myclaw-keystore.jks \
  -keyalg RSA -keysize 2048 -validity 10000 \
  -alias myclaw

# Reference in pubspec.yaml or use during build:
flutter build apk --release --keystore ~/myclaw-keystore.jks
```

### iOS Signing
Set up in Xcode:
1. Open ios/Runner.xcworkspace
2. Select Runner project
3. Go to Signing & Capabilities
4. Configure Team ID and signing certificate

## Troubleshooting Build Issues

### Flutter Not Found
```bash
export PATH="$PATH:$HOME/flutter/bin"
```

### Gradle Build Fails
```bash
cd android
./gradlew clean
cd ..
flutter clean
flutter pub get
flutter build apk --release
```

### Pod Install Fails (iOS)
```bash
cd ios
rm Podfile.lock
pod install
cd ..
```

### Permission Denied
```bash
chmod +x android/gradlew
chmod +x ios/Pods/...  # if needed
```

## Performance Optimization

### Reduce APK Size
```bash
flutter build apk --release --split-per-abi
```

### Enable ProGuard/R8 (Android)
Edit `android/app/build.gradle`:
```gradle
buildTypes {
    release {
        minifyEnabled true
        shrinkResources true
        proguardFiles getDefaultProguardFile('proguard-android-optimize.txt'), 'proguard-rules.pro'
    }
}
```

## Distribution

### Direct Distribution
- Host APK on your server/CDN
- Users download and manually install

### Google Play Store
1. Create Google Play Developer account ($25 one-time)
2. Create app listing
3. Upload AAB via Play Console
4. Complete store listing and review

### F-Droid (FOSS Alternative)
- Submit app to F-Droid
- Automatic builds from source
- No app review needed

## Additional Resources

- [Flutter Documentation](https://flutter.dev/docs)
- [Android Build Documentation](https://flutter.dev/docs/deployment/android)
- [iOS Build Documentation](https://flutter.dev/docs/deployment/ios)
- [GitHub Actions Documentation](https://docs.github.com/en/actions)