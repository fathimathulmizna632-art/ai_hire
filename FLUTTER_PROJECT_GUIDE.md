# AI Hire Flutter App - Complete Project Guide

## 📋 Table of Contents
1. [Project Overview](#project-overview)
2. [Features](#features)
3. [Project Structure](#project-structure)
4. [Getting Started](#getting-started)
5. [Installation](#installation)
6. [Running the App](#running-the-app)
7. [Screen Descriptions](#screen-descriptions)
8. [Design System](#design-system)
9. [API Integration](#api-integration)
10. [Troubleshooting](#troubleshooting)

## 🎯 Project Overview

**AI Hire** is a comprehensive Flutter application designed for interview preparation and job seeking. Users can take mock tests, explore job opportunities, schedule interviews, and get feedback from interviewers.

**Target Users:**
- Job seekers preparing for interviews
- College students building interview skills
- Professional developers advancing their careers

**Key Metrics:**
- 8 complete screens (authentication + features)
- 12+ animations across all screens
- Modern Material 3 design
- Responsive layout support

## ✨ Features

### Authentication
- ✅ User login with email/password
- ✅ New user registration
- ✅ Forgot password with OTP verification
- ✅ Session management

### Core Features
- ✅ Mock test platform with multiple choice questions
- ✅ Interview scheduling and management
- ✅ Job/interview browsing and application
- ✅ User profile with editing
- ✅ Performance statistics
- ✅ Feedback submission system
- ✅ Complaint tracking and resolution
- ✅ App settings and preferences

### Design & UX
- ✅ Modern gradient backgrounds
- ✅ Smooth entrance animations
- ✅ Staggered list item animations
- ✅ Interactive form controls
- ✅ Loading states with spinners
- ✅ Error and success feedback
- ✅ Bottom navigation
- ✅ Drawer menu

## 📁 Project Structure

```
lib/
├── main.dart                          # App entry point & routing
├── screens/
│   ├── auth/
│   │   ├── login_screen.dart         # Email/password login (300+ lines)
│   │   ├── register_screen.dart       # New user registration (320+ lines)
│   │   └── forgot_password.dart       # Password recovery (280+ lines)
│   ├── home/
│   │   └── home_screen.dart          # Main dashboard (420+ lines)
│   ├── mocktest/
│   │   └── mocktest_list_screen.dart # Available tests (310+ lines)
│   ├── interviews/
│   │   └── interview_browse.dart     # Job postings (340+ lines)
│   ├── bookings/
│   │   └── booking_list_screen.dart  # Scheduled interviews (380+ lines)
│   ├── profile/
│   │   └── profile_screen.dart       # User profile (450+ lines)
│   ├── feedback/
│   │   └── feedback_screen.dart      # Feedback submission (280+ lines)
│   ├── complaints/
│   │   └── complaints_screen.dart    # Issue reporting (420+ lines)
│   └── settings/
│       └── settings_screen.dart      # App preferences (380+ lines)
├── models/                            # (To be added)
│   ├── user.dart
│   ├── mocktest.dart
│   ├── question.dart
│   ├── interview.dart
│   ├── booking.dart
│   └── feedback.dart
├── services/                          # (To be added)
│   ├── api_service.dart
│   ├── auth_service.dart
│   └── storage_service.dart
├── widgets/                           # (To be added - Shared components)
│   ├── custom_button.dart
│   ├── custom_card.dart
│   ├── app_header.dart
│   └── loading_widget.dart
└── constants/                         # (To be added)
    ├── colors.dart
    ├── strings.dart
    └── styles.dart

assets/
├── images/                            # (To be added)
├── icons/                             # (To be added)
└── fonts/                             # (Roboto included via Material)

pubspec.yaml                           # Project dependencies
```

## 🚀 Getting Started

### Prerequisites
- Flutter SDK (Latest stable version)
- Dart SDK (Included with Flutter)
- IDE: Android Studio, VS Code, or IntelliJ
- Git for version control

### Required Versions
```
Flutter: >=3.0.0
Dart: >=3.0.0
```

## 💾 Installation

### 1. Clone the Repository
```bash
cd c:\Users\ASUS\PycharmProjects\ai_hire
```

### 2. Get Flutter Dependencies
```bash
flutter pub get
```

### 3. Generate necessary files
```bash
flutter create .
```

### 4. Verify Installation
```bash
flutter doctor
```

## ▶️ Running the App

### Run on Emulator
```bash
# List available devices
flutter devices

# Run on default device
flutter run

# Run with verbose logging
flutter run -v

# Run in release mode
flutter run --release
```

### Run on Physical Device
```bash
# Enable USB debugging on Android device
# Connect device via USB
flutter devices
flutter run
```

### Run on Web Browser
```bash
flutter run -d chrome
```

### Run on Specific Device
```bash
flutter run -d <device_id>
```

## 📱 Screen Descriptions

### Authentication Screens

#### 1. **Splash Screen** (3 seconds)
- Animated logo with scale and fade transitions
- Blue gradient background
- Auto-navigates to login screen
- **File**: [`lib/main.dart`](lib/main.dart#L72-L132)

#### 2. **Login Screen**
- Email and password fields
- Password visibility toggle
- "Forgot Password?" link
- "Sign Up" navigation
- Loading state during authentication
- **Features**: Slide and fade animations
- **File**: [`lib/screens/auth/login_screen.dart`](lib/screens/auth/login_screen.dart)

#### 3. **Register Screen**
- Full name, email, phone inputs
- Password confirmation
- Animated form entrance
- Form validation
- **File**: [`lib/screens/auth/register_screen.dart`](lib/screens/auth/register_screen.dart)

#### 4. **Forgot Password Screen**
- Two-step process: Email → OTP → New Password
- OTP verification field
- Password reset form
- **File**: [`lib/screens/auth/forgot_password_screen.dart`](lib/screens/auth/forgot_password_screen.dart)

### Main App Screens

#### 5. **Home Screen** (Main Dashboard)
- Welcome card with gradient background
- Quick stats (Tests, Score, Interviews)
- Feature grid (4 main actions):
  - Mock Tests
  - Interviews
  - Bookings
  - Profile
- Recent activity timeline
- Bottom navigation bar
- Drawer menu with settings
- **Animations**: 
  - Fade in welcome card
  - Slide in stats row
  - Scale in feature cards (staggered)
- **File**: [`lib/screens/home/home_screen.dart`](lib/screens/home/home_screen.dart)

#### 6. **Mock Tests List Screen**
- Browse available mock tests
- Test cards showing:
  - Test title and description
  - Number of questions
  - Duration and difficulty level
  - Gradient header with icon
- "Start Test" button per test
- **Features**:
  - Animated test cards
  - Difficulty color coding (Green/Orange/Red)
- **File**: [`lib/screens/mocktest/mocktest_list_screen.dart`](lib/screens/mocktest/mocktest_list_screen.dart)

#### 7. **Interview Browse Screen**
- Search bar to find jobs
- Job listing with:
  - Position title and company
  - Location and salary range
  - Experience requirement
  - Active status badge
- "View Details" and "Apply" buttons
- **Features**:
  - Salary range display
  - Job type indicator
  - Staggered list animations
- **File**: [`lib/screens/interviews/interview_browse_screen.dart`](lib/screens/interviews/interview_browse_screen.dart)

#### 8. **Booking List Screen**
- View scheduled interviews
- Booking cards showing:
  - Company name and interview type
  - Interviewer information
  - Date and time
  - Status badge (Confirmed/Pending/Completed)
  - Interview details
- "Reschedule" and "Details" actions
- **Features**:
  - Color-coded status borders
  - Interview type icons
  - Action buttons per booking
- **File**: [`lib/screens/bookings/booking_list_screen.dart`](lib/screens/bookings/booking_list_screen.dart)

#### 9. **Profile Screen**
- User avatar with large display
- Editable profile fields:
  - Name, Email, Phone
  - Position, Location
- Statistics section (Tests, Success Rate, Interviews)
- Action buttons:
  - Settings
  - Change Password (modal)
- Edit mode toggle
- **Features**:
  - Inline field editing
  - Password change dialog
  - Profile statistics cards
- **File**: [`lib/screens/profile/profile_screen.dart`](lib/screens/profile/profile_screen.dart)

### Feature Screens

#### 10. **Feedback Screen**
- Rating system (1-5 stars, interactive)
- Feedback text area
- Submit button with loading state
- Consistent gradient header
- **Features**:
  - Star rating selector
  - Dynamic rating text
  - Success feedback after submission
- **File**: [`lib/screens/feedback/feedback_screen.dart`](lib/screens/feedback/feedback_screen.dart)

#### 11. **Complaints Screen**
- Category dropdown (Technical/Payment/Content/Other)
- Complaint description text area
- Submit button with loading
- View previous complaints with:
  - Status badges (Pending/In Progress/Resolved)
  - Reply section (if applicable)
  - Date tracking
- **Features**:
  - Complaint history with filtering
  - Reply visualization
  - Status color coding
- **File**: [`lib/screens/complaints/complaints_screen.dart`](lib/screens/complaints/complaints_screen.dart)

#### 12. **Settings Screen**
- Notification preferences
  - Push notifications toggle
  - Email updates toggle
- Appearance settings
  - Dark mode toggle (future feature)
- Account security
  - Change password dialog
  - Two-factor authentication
- Privacy & legal
  - Privacy policy link
  - Terms of service link
- About section
  - App version
  - Build number
- Danger zone
  - Delete account option with confirmation
- **Features**:
  - Toggle switches with visual feedback
  - Action dialogs
  - Info display section
- **File**: [`lib/screens/settings/settings_screen.dart`](lib/screens/settings/settings_screen.dart)

## 🎨 Design System

### Color Scheme
- **Primary**: `#2E5FB3` (Blue)
- **Dark**: `#1E3A8A` (Dark Blue)
- **Success**: `#10B981` (Green)
- **Warning**: `#F59E0B` (Orange)
- **Error**: `#EF4444` (Red)
- **Background**: Linear gradient from `#F5F7FA` to `#E8EEF7`

### Typography
- **Font Family**: Roboto (Google Fonts)
- **Sizes**: 11pt to 56pt with clear hierarchy
- **Weights**: Regular (400) and Bold (700)

### Animations
- **Duration**: 200ms to 1500ms based on element
- **Curves**: easeOut, easeInOut, linear
- **Types**: Fade, Slide, Scale, AnimatedContainer
- **Stagger Interval**: 150ms between list items

### Spacing
- Standard intervals: 4px, 8px, 12px, 16px, 20px, 24px, 28px
- Consistent padding across all screens
- Proper margins for visual hierarchy

### Components
- All buttons: 56px height, 12px border radius
- All cards: 14px border radius, soft shadow
- Input fields: 56px height, white background
- Icons: 16px to 60px with proper spacing

## 🔌 API Integration

### Current State
```
✅ Screens completed with mock data
⏳ API integration to be implemented
⏳ Database models to be created
```

### To Be Implemented

#### Authentication APIs
```
POST /api/auth/login
POST /api/auth/register
POST /api/auth/forgot-password
POST /api/auth/verify-otp
POST /api/auth/reset-password
```

#### Test APIs
```
GET /api/mocktests
GET /api/mocktests/:id
POST /api/mocktests/:id/submit
GET /api/results/:id
```

#### Interview APIs
```
GET /api/interviews
GET /api/interviews/:id
POST /api/interviews/:id/apply
GET /api/bookings
POST /api/bookings/:id/reschedule
```

#### User APIs
```
GET /api/profile
PUT /api/profile
POST /api/password/change
POST /api/feedback
POST /api/complaints
GET /api/complaints
```

## 🔧 Dependency Configuration

### Current pubspec.yaml
```yaml
dependencies:
  flutter:
    sdk: flutter

dev_dependencies:
  flutter_test:
    sdk: flutter
```

### To Be Added
```yaml
dependencies:
  http: ^1.1.0                    # For API calls
  shared_preferences: ^2.2.0      # For local storage
  intl: ^0.18.0                   # For date formatting
  provider: ^6.0.0                # For state management
  cached_network_image: ^3.2.0    # For image caching
  smooth_page_indicator: ^1.0.0   # For page dots
```

## 🐛 Troubleshooting

### Common Issues

#### Issue: "No devices found"
```bash
# Check connected devices
flutter devices

# For Android emulator
emulator @emulator_name

# For iOS simulator
open -a Simulator
```

#### Issue: "Gradle sync failed"
```bash
# Clean build cache
flutter clean

# Rebuild
flutter pub get
flutter run
```

#### Issue: "Firebase/Dependencies not found"
```bash
# Update dependencies
flutter pub upgrade

# Get all dependencies
flutter pub get
```

#### Issue: "Hot reload not working"
```bash
# Kill the app and restart
flutter run --no-fast-start
```

#### Issue: "Port 8080 already in use"
```bash
# Use different port
flutter run -d chrome --web-port=8081
```

## 📊 Performance Optimization

### Tips
1. Use `const` constructors where possible
2. Limit rebuilds with `shouldRebuild()` in providers
3. Use `RepaintBoundary` for expensive widgets
4. Lazy load images with `cached_network_image`
5. Profile with DevTools to find bottlenecks

## 🚦 Development Workflow

### Adding a New Screen
1. Create file in appropriate folder under `screens/`
2. Extend `StatefulWidget` with `SingleTickerProviderStateMixin`
3. Create `AnimationController` in `initState()`
4. Build UI with standard spacing (16px padding)
5. Add animations following the system
6. Add route to `main.dart`
7. Add navigation in relevant screens

### Modifying Existing Screen
1. Maintain animation pattern
2. Keep color scheme consistent
3. Use standard spacing intervals
4. Test on multiple screen sizes

## 📚 Best Practices

1. **Naming Convention**:
   - Screens: `*_screen.dart`
   - Widgets: `*_widget.dart`
   - Models: singular names (`user.dart`, `mocktest.dart`)
   - Services: `*_service.dart`

2. **Code Organization**:
   - Build methods should be < 300 lines
   - Extract complex widgets to separate methods
   - Use `_buildXxx()` for private widget methods

3. **Animation Pattern**:
   - Always use `SingleTickerProviderStateMixin`
   - Dispose animation controller in `dispose()`
   - Follow standard animation durations

4. **Error Handling**:
   - Show user-friendly error messages
   - Use try-catch for API calls
   - Validate form inputs

5. **Testing**:
   - Test navigation flow
   - Test animations smoothness
   - Test form validation
   - Test responsiveness on different screen sizes

## 📈 Future Enhancements

- [ ] Dark mode support
- [ ] Multi-language support
- [ ] Offline mode with local caching
- [ ] Push notifications
- [ ] Video interview feature
- [ ] Advanced analytics dashboard
- [ ] Social sharing of results
- [ ] Integration with resume upload
- [ ] AI-powered feedback system
- [ ] Gamification with badges/achievements

## 📞 Support & Issues

For issues or questions:
1. Check existing issues in repository
2. Create detailed bug report
3. Include device info and Flutter version
4. Provide reproduction steps

## 📄 License

This project is proprietary. All rights reserved.

---

**Version**: 1.0.0  
**Created**: February 9, 2026  
**Last Updated**: February 9, 2026  
**Flutter Version**: 3.0.0+  
**Dart Version**: 3.0.0+

**Quick Links**:
- [Design System](./FLUTTER_DESIGN_COMPLETE.md)
- [Flutter Documentation](https://flutter.dev/docs)
- [Material Design 3](https://m3.material.io/)
