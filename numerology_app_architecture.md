# Numerology App — Architecture & Planning Document

---

## What is This App?

A cross-platform **Numerology Application** built using **Flutter**, capable of running on:

- Windows Desktop
- Android Mobile
- macOS (DMG)
- iOS
- Web (future scope)

The app calculates and displays numerological data including BN/DN numbers, Lo Shu Grid, and Vedic Grid — and saves user readings as custom `.numero` files on the device.

---

## Technology Choice

### Why Flutter?

Flutter is a UI framework by Google that lets you write code **once** and run it on multiple platforms — Android, Windows, macOS, iOS, and Web — all from a single codebase.

| Feature | Flutter |
|---|---|
| Android APK | ✅ |
| Windows EXE | ✅ |
| macOS DMG | ✅ |
| iOS IPA | ✅ |
| Web | ✅ |
| Native-like UI | ✅ |
| Hot Reload (live preview) | ✅ |

### Why Not Python?

Python is excellent for backend APIs, AI/ML, and data processing — but it cannot natively build mobile apps or generate store-ready files (APK, EXE, IPA, DMG). For this app, Flutter alone is sufficient.

> Python would only be needed in the future if cloud sync or multi-device access is required.

---

## App Architecture

### Project Folder Structure

```
lib/
├── main.dart                        # Entry point — detects platform and launches dashboard
│
├── core/                            # Business logic — no UI here
│   ├── bn_dn_calculator.dart        # All Birth Number & Destiny Number calculations
│   ├── loshu_grid.dart              # Lo Shu Grid generation logic
│   └── vedic_grid.dart              # Vedic Grid generation logic
│
├── config/                          # Layout configuration per platform
│   ├── desktop_config.dart          # Spacing, columns, font sizes for Windows/Desktop
│   └── mobile_config.dart           # Spacing, columns, font sizes for Android/Mobile
│
├── storage/                         # File management
│   └── file_manager.dart            # Save and read .numero files locally
│
└── dashboard.dart                   # Single dashboard UI for all platforms
```

---

## File Responsibilities

### `bn_dn_calculator.dart`
Contains all numerological calculation logic:
- Birth Number (BN)
- Destiny Number (DN)
- Any derived calculations

### `loshu_grid.dart`
Generates the Lo Shu Grid based on the user's date of birth.

### `vedic_grid.dart`
Generates the Vedic Grid based on the user's numerological data.

### `desktop_config.dart`
Holds layout values specific to desktop/Windows:
- Wider padding
- Multi-column grid layout
- Larger font sizes

### `mobile_config.dart`
Holds layout values specific to Android/Mobile:
- Compact padding
- Single column layout
- Smaller font sizes

### `dashboard.dart`
One single dashboard that:
- Imports from all core files
- Detects platform at runtime
- Picks the correct config automatically
- Displays BN/DN, Lo Shu Grid, and Vedic Grid

### `file_manager.dart`
Handles saving and loading `.numero` files locally on the device.

---

## How Platform Detection Works

Both config files are compiled into every build. When the app runs, it detects the platform automatically and picks the right config.

```dart
import 'dart:io';

class ConfigResolver {
  static bool get isDesktop =>
      Platform.isWindows || Platform.isMacOS || Platform.isLinux;

  static dynamic get config =>
      isDesktop ? DesktopConfig() : MobileConfig();
}
```

The **builder does not choose** the config — the **running app does**, at the moment it starts, based on what device it is running on.

---

## Dashboard Layout Behaviour

```
MOBILE (1 column)            DESKTOP (3 columns)
┌─────────────┐              ┌───────┬───────┬───────┐
│  BN / DN    │              │ BN/DN │ Loshu │ Vedic │
├─────────────┤              │       │ Grid  │ Grid  │
│  Loshu Grid │              └───────┴───────┴───────┘
├─────────────┤
│  Vedic Grid │
└─────────────┘
```

Same dashboard file — the config drives the layout automatically.

---

## Saving User Readings — `.numero` File

User readings are saved as custom `.numero` files directly on the device — no internet or server required.

### Example: `Albert.numero`
```
NAME: Albert
DOB: 1990-05-15
BIRTH NUMBER: 6
DESTINY NUMBER: 3
LOSHU GRID: [[1,2,3],[4,5,6],[7,8,9]]
VEDIC GRID: ...
DATE SAVED: 2024-01-15
```

### Save Location by Platform

| Platform | Location |
|---|---|
| Windows | `C:/Users/You/Documents/Albert.numero` |
| Android | Internal app storage |
| macOS | `/Users/You/Documents/Albert.numero` |

---

## User Flow

```
User enters Name + Date of Birth
            │
            ▼
Flutter calculates BN, DN, Lo Shu Grid, Vedic Grid
            │
            ▼
Dashboard displays all results
(Desktop: 3 columns | Mobile: 1 column)
            │
            ▼
User clicks Save
            │
            ▼
Albert.numero saved on device ✅
```

---

## Build Commands

### During Development (Testing)

```bash
flutter devices                        # See all available devices/emulators
flutter run -d windows                 # Run on Windows live
flutter run -d emulator-5554          # Run on Android Emulator
flutter run -d chrome                  # Run in browser
```

### Production Builds

```bash
flutter build apk                      # Android APK (direct install)
flutter build appbundle                # Android AAB (Google Play Store)
flutter build windows                  # Windows EXE
flutter build macos                    # macOS APP/DMG (must be on Mac)
flutter build ipa                      # iOS IPA (must be on Mac)
flutter build web                      # Web
```

### Store Uploads

| Store | File | Command |
|---|---|---|
| Google Play Store | `.aab` | `flutter build appbundle` |
| Microsoft Store | `.msix` | `flutter pub run msix:create` |
| Apple App Store | `.ipa` | `flutter build ipa` (Mac only) |

---

## What Flutter Handles — Summary

| Feature | Handled By |
|---|---|
| BN / DN Calculations | `bn_dn_calculator.dart` |
| Lo Shu Grid | `loshu_grid.dart` |
| Vedic Grid | `vedic_grid.dart` |
| Desktop UI Layout | `desktop_config.dart` |
| Mobile UI Layout | `mobile_config.dart` |
| Single Unified Dashboard | `dashboard.dart` |
| Save/Read `.numero` files | `file_manager.dart` |
| Windows Build | `flutter build windows` |
| Android Build | `flutter build apk` |
| Store-ready files | Platform build commands |

---

## Future Scope (If Needed)

If the app ever needs to sync readings across multiple devices or support user accounts, a **Python FastAPI backend** can be added:

```
Flutter App  ──────►  Python FastAPI  ──────►  Database
(Frontend)             (Backend API)            (Cloud Storage)
```

For now, since all data stays on the same device, **Flutter alone is sufficient**.

---

*Document prepared based on application planning discussion.*
*Framework: Flutter | Language: Dart | Platforms: Windows, Android, macOS, iOS, Web*
