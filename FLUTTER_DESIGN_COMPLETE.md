# AI Hire Flutter App - Complete Design System

## 📱 Project Overview

The AI Hire Flutter application is a comprehensive interview preparation platform designed with modern UI/UX principles. The app helps users prepare for interviews through mock tests, interview scheduling, and skill assessment.

## 🎨 Design Architecture

### Color Palette

**Primary Colors:**
- Primary Blue: `#2E5FB3` - Used for main CTAs, headers
- Dark Blue: `#1E3A8A` - Used for text and emphasis
- Background Gradient: `#F5F7FA` to `#E8EEF7`

**Status Colors:**
- Success (Green): `#10B981` - Confirmed, passed, active
- Warning (Orange): `#F59E0B` - In progress, pending
- Error (Red): `#EF4444` - Failed, issues
- Info (Blue): `#3B82F6` - Additional information

**Neutral Tones:**
- White: `#FFFFFF` - Card backgrounds
- Light Gray: `#E5E7EB` - Dividers
- Medium Gray: `#9CA3AF` - Hints, disabled
- Dark Gray: `#374151` - Secondary text

### Typography System

| Level | Size | Weight | Usage |
|-------|------|--------|-------|
| Hero | 48pt | Bold | Splash screen title |
| Heading 1 | 28-32pt | Bold | Screen titles |
| Heading 2 | 20-24pt | Bold | Section headers |
| Heading 3 | 16-18pt | Bold | Card titles |
| Body 1 | 14pt | Regular | Main text |
| Body 2 | 13pt | Regular | Secondary text |
| Caption | 11-12pt | Regular | Hints, labels |

### Spacing System

Standard spacing intervals (used consistently throughout):
- `4px` - Micro spacing (icon padding)
- `8px` - Small spacing (adjacent elements)
- `12px` - Medium spacing (sections)
- `16px` - Standard spacing (main padding)
- `20px` - Large spacing (between major sections)
- `24px` - Extra large spacing
- `28px` - Maximum spacing (screen margins)

### Border & Corner Radius

- Standard border radius: `12-14px` for cards and containers
- Button border radius: `8-10px` for consistency
- Avatar/circles: `20-25px` radius for badges
- Icon buttons: `12px` radius

## 📊 Screen Hierarchy

### Authentication Flow
1. **SplashScreen** - Entry point with animated logo (3-second delay)
2. **LoginScreen** - Email/password authentication with forgot password link
3. **RegisterScreen** - New user registration with validation
4. **ForgotPasswordScreen** - Multi-step OTP verification and password reset

### Main App Flow (After Login)
1. **HomeScreen** - Main dashboard with quick stats and feature grid
2. **MocktestListScreen** - Browse and start mock tests
3. **InterviewBrowseScreen** - Explore job opportunities
4. **BookingListScreen** - Manage scheduled interviews
5. **ProfileScreen** - User profile with editing capabilities

### Feature Screens
6. **FeedbackScreen** - Rate and submit feedback with star rating
7. **ComplaintsScreen** - Report issues with category selection
8. **SettingsScreen** - App preferences and account settings

## 🎭 Animation System

### Animation Types

| Type | Duration | Usage |
|------|----------|-------|
| Scale | 1000ms | Large element entrance |
| Fade | 800ms | Content appearance |
| Slide | 1000-1200ms | Navigation transitions |
| Stagger | 150ms interval | List items |
| Micro | 200ms | Button interactions |

### Animation Curves
- `Curves.easeOut` - Entrance animations
- `Curves.easeInOut` - Smooth transitions
- `Curves.linear` - Progress indicators
- `Interval(start, end)` - Staggered animations

### Example Animation Pattern
```dart
SlideTransition(
  position: Tween<Offset>(
    begin: const Offset(0, -0.3),
    end: Offset.zero,
  ).animate(
    CurvedAnimation(
      parent: _animationController,
      curve: Curves.easeOut,
    ),
  ),
  child: YourWidget(),
)
```

## 🧩 Component Library

### Cards
- **StandardCard**: White background, 12px radius, soft shadow
- **GradientCard**: Linear gradient with gradient icons
- **ActionCard**: Interactive card with buttons
- **StatCard**: Display statistics with emphasis color

### Buttons
- **PrimaryButton**: Solid background (#2E5FB3), white text
- **SecondaryButton**: Outline style
- **IconButton**: Icon with optional label
- **ButtonStates**: Normal, Disabled, Loading

### Input Fields
- **TextField**: White background, 12px radius, prefix icon
- **PasswordField**: Toggle visibility icon
- **DropdownField**: Custom styled dropdown

### Lists
- **UserListItem**: Avatar, name, status
- **TestListItem**: Icon, title, metadata, CTA
- **ActivityItem**: Timeline dot, title, timestamp

## 📐 Layout Patterns

### Standard Screen Layout
```
[AppBar]
[Optional Header Card - Animated]
[Content Section 1 - Fade In]
  - Section Title
  - Content Cards
[Content Section 2]
  - Cards/Lists
[Bottom Navigation / Drawer]
```

### Card Layout Pattern
```
[Gradient Header] OR [Colored Top Border]
  [Icon Container]
  [Title]
  [Subtitle/Description]
[Divider]
[Content Area]
  [Details/Stats]
[Action Buttons]
  [Primary Button] [Secondary Button]
```

## 🎬 Animation Choreography

### Screen Entry Animation (Staggered)
1. **0-300ms**: Header slides up and fades in
2. **300-600ms**: Stats row slides in from left
3. **600-1000ms**: Feature cards scale in with stagger
4. **1000-1500ms**: Content fades in

### List Item Animation (Per Item)
- Item 1: Start at 100ms, duration 500ms
- Item 2: Start at 250ms, duration 500ms
- Item 3: Start at 400ms, duration 500ms
- Etc. (150ms stagger interval)

## 🌳 Project Structure

```
lib/
├── main.dart                 # App entry & routes
├── screens/
│   ├── auth/
│   │   ├── login_screen.dart
│   │   ├── register_screen.dart
│   │   └── forgot_password_screen.dart
│   ├── home/
│   │   └── home_screen.dart
│   ├── mocktest/
│   │   └── mocktest_list_screen.dart
│   ├── interviews/
│   │   └── interview_browse_screen.dart
│   ├── bookings/
│   │   └── booking_list_screen.dart
│   ├── profile/
│   │   └── profile_screen.dart
│   ├── feedback/
│   │   └── feedback_screen.dart
│   ├── complaints/
│   │   └── complaints_screen.dart
│   └── settings/
│       └── settings_screen.dart
├── models/
│   ├── user.dart
│   ├── mocktest.dart
│   ├── interview.dart
│   └── booking.dart
├── services/
│   ├── api_service.dart
│   ├── auth_service.dart
│   └── storage_service.dart
├── widgets/
│   ├── custom_button.dart
│   ├── custom_card.dart
│   ├── app_header.dart
│   └── loading_widget.dart
└── constants/
    ├── colors.dart
    └── styles.dart
```

## 🔄 Navigation Flow

```
SplashScreen
    ↓
LoginScreen ←→ RegisterScreen
    ↓          ↑
ForgotPasswordScreen
    ↓
HomeScreen (Main Hub)
    ├→ MocktestListScreen
    ├→ InterviewBrowseScreen
    ├→ BookingListScreen
    ├→ ProfileScreen
    │   └→ SettingsScreen
    ├→ FeedbackScreen
    ├→ ComplaintsScreen
    └→ SettingsScreen
```

## 🎯 Design Principles

1. **Consistency**: Same components, spacing, and animations throughout
2. **Clarity**: Clear hierarchy and visual feedback
3. **Performance**: Smooth animations (60fps target)
4. **Accessibility**: Good contrast ratios, touch targets ≥48x48pts
5. **Responsive**: Works on various device sizes
6. **Modern**: Material 3 design principles

## 📱 Responsive Design

### Breakpoints
- Mobile: < 600dp
- Tablet: 600-840dp
- Desktop: > 840dp

### Key Responsive Elements
- Lists adapt column count based on width
- Cards expand to fill available space
- Text scales based on screen width
- Padding increases on larger screens

## 🌟 Key Features

### Interactive Elements
- Smooth button animations on press
- Icon state changes (e.g., eye icon for password)
- Card elevation changes on hover/press
- Progress indicators during loading
- Toast/Snackbar notifications

### Feedback Mechanisms
- Loading spinners during API calls
- Success/error messages
- Animated state transitions
- Visual status indicators (colors)

### Data Visualization
- Star ratings (5-point scale)
- Progress bars
- Statistics cards
- Status badges with colors

## 🚀 Implementation Tips

### Creating New Screens
1. Extend `StatefulWidget` with single `TickerProviderStateMixin`
2. Create `AnimationController` in `initState`
3. Build layout with standard spacing (16px padding)
4. Wrap main content in transition widgets
5. Use gradient backgrounds consistently

### Consistent Styling
```dart
// Always use these for consistency
backgroundColor: const Color(0xFFF5F7FA),
appBarColor: const Color(0xFF2E5FB3),
textColor: const Color(0xFF1E3A8A),
successColor: const Color(0xFF10B981),
```

### Animation Template
```dart
FadeTransition(
  opacity: Tween<double>(begin: 0, end: 1).animate(
    CurvedAnimation(parent: _animationController, curve: Curves.easeIn),
  ),
  child: MyWidget(),
)
```

## 🔧 Configuration

### Theme Setup (main.dart)
```dart
theme: ThemeData(
  useMaterial3: true,
  colorScheme: ColorScheme.fromSeed(seedColor: const Color(0xFF2E5FB3)),
  fontFamily: 'Roboto',
  scaffoldBackgroundColor: const Color(0xFFF5F7FA),
)
```

## 📚 Dependencies

- `flutter`: Core framework
- `material`: UI components
- `http`: API calls (to be added)
- `shared_preferences`: Local storage (to be added)
- `intl`: Localization (to be added)

## ✅ Quality Checklist

- [ ] All screens follow color palette
- [ ] All text uses typography system
- [ ] All spacing uses 4px-based system
- [ ] All cards use 12-14px border radius
- [ ] All buttons have loading states
- [ ] All lists have animations
- [ ] All screens have app bar
- [ ] All dialogs follow design patterns
- [ ] Dark mode considered (future)
- [ ] Accessibility standards met

---

**Last Updated**: February 9, 2026  
**Version**: 1.0.0  
**Designer**: AI Hire Design System
