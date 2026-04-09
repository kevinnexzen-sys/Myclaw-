# Myclaw - Installation Guide

## 📱 Mobile Installation

### Android

#### Option 1: Download Pre-built APK
1. Go to [Releases](https://github.com/kevinnexzen-sys/Myclaw-/releases)
2. Download the latest APK file:
   - **app-arm64-v8a-release.apk** (Recommended for modern devices)
   - **app-armeabi-v7a-release.apk** (For older devices)
   - **app-x86_64-release.apk** (For emulators)

#### Option 2: Install via APK
1. Enable "Unknown Sources" on your Android device:
   - Go to Settings > Security
   - Enable "Unknown Sources"
2. Download the APK from releases
3. Tap the downloaded file to install
4. Grant necessary permissions when prompted

#### Option 3: Google Play Store (Coming Soon)
We're working on publishing Myclaw to the Google Play Store for easier installation.

### iOS

#### Build from Source (Mac Required)
```bash
git clone https://github.com/kevinnexzen-sys/Myclaw-.git
cd Myclaw-
flutter pub get
flutter build ios --release
```

## 💻 System Requirements

### Android
- Minimum Android 8.0 (API 26)
- ~150 MB free storage
- Internet connection required

### iOS
- iOS 12.0 or higher
- ~200 MB free storage
- Internet connection required

## 🚀 First Run

1. **Grant Permissions**: Allow microphone, camera, and other necessary permissions
2. **Configure Supabase**: Enter your Supabase credentials (or use demo mode)
3. **Setup Voice**: Configure speech recognition settings
4. **Connect Devices**: Link your PC or other devices for remote control

## 🔒 Permissions Required

- **Microphone**: For voice input
- **Camera**: For optional video features
- **Storage**: For caching and logs
- **Network**: For cloud sync and PC control
- **Overlay**: For floating widgets

## 🆘 Troubleshooting

### App Won't Install
- Ensure "Unknown Sources" is enabled
- Check available storage (minimum 150 MB)
- Try clearing Google Play Store cache

### App Crashes on Startup
- Clear app cache: Settings > Apps > Myclaw > Clear Cache
- Reinstall the app
- Check internet connection

### Voice Recognition Not Working
- Enable microphone permission
- Check internet connection (required for voice API)
- Restart the app

### PC Control Not Responding
- Ensure both devices are on the same network
- Check PC is awake and connected
- Verify firewall settings allow connection

## 📞 Support

For issues and feature requests, visit: [GitHub Issues](https://github.com/kevinnexzen-sys/Myclaw-/issues)

## 📝 Build from Source

### Requirements
- Flutter 3.19.0 or higher
- Dart SDK
- Android SDK (for Android builds)
- Xcode (for iOS builds)

### Steps
```bash
# Clone repository
git clone https://github.com/kevinnexzen-sys/Myclaw-.git
cd Myclaw-

# Get dependencies
flutter pub get

# Build APK
flutter build apk --release

# Build iOS
flutter build ios --release
```