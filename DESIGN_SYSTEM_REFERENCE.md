# 🎨 Flutter MockTest - Design System Quick Reference

## Color Palette

### Primary Colors
| Color | Hex Code | RGB | Usage |
|-------|----------|-----|-------|
| Primary Blue | `#2E5FB3` | 46, 95, 179 | Primary buttons, AppBar, headers |
| Dark Blue | `#1E3A8A` | 30, 58, 138 | Text, dark variants |
| Light Gray | `#F5F7FA` | 245, 247, 250 | Background start |
| Accent Gray | `#E8EEF7` | 232, 238, 247 | Background end |

### Status Colors
| Color | Hex Code | RGB | Usage |
|-------|----------|-----|-------|
| Success Green | `#10B981` | 16, 185, 129 | Correct answers, success states |
| Warning Orange | `#F59E0B` | 245, 158, 11 | Warnings, unanswered items |
| Error Red | `#EF4444` | 239, 68, 68 | Wrong answers, errors |
| Info Blue | `#3B82F6` | 59, 130, 246 | Information, secondary |

## Quick Copy-Paste Colors

```dart
// Primary
Color(0xFF2E5FB3)  // Primary Blue
Color(0xFF1E3A8A)  // Dark Blue

// Status
Color(0xFF10B981)  // Green (Success)
Color(0xFFF59E0B)  // Orange (Warning)
Color(0xFFEF4444)  // Red (Error)
Color(0xFF3B82F6)  // Blue (Info)

// Backgrounds
Color(0xFFF5F7FA)  // Light Gray BG
Color(0xFFE8EEF7)  // Accent Gray BG
```

## Typography Scale

```
Hero:       56pt, Bold (Score display)
Title Large: 32pt, Bold (Grade label)
Title:      20pt, Bold (Page titles, section headers)
Headline:   18pt, Bold (Subsections)
Body Large: 16pt, Regular (Question text)
Body:       14pt, Regular (Description, body content)
Label:      12pt, Regular (Labels, chips)
Caption:    11pt, Regular (Small text, hints)
```

## Spacing System

```
xs: 4px
sm: 8px
md: 12px
lg: 16px
xl: 20px
2xl: 24px
3xl: 28px
```

## Corner Radius

```
Small:   6px
Medium:  10px
Large:   12px
XL:      14px
Full:    20-25px (circles)
```

## Elevation & Shadows

```
Subtle:   elevation: 1-2
Standard: elevation: 3-4
Card:     elevation: 4-5
Modal:    elevation: 8-12
AppBar:   elevation: 8
```

## Component Guidelines

### Button Styles

**Primary Button (Blue)**
```dart
ElevatedButton.styleFrom(
  backgroundColor: Color(0xFF2E5FB3),
  shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(12)),
)
```

**Success Button (Green)**
```dart
ElevatedButton.styleFrom(
  backgroundColor: Colors.green[600],
  shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(12)),
)
```

**Outlined Button**
```dart
OutlinedButton.styleFrom(
  side: BorderSide(color: Colors.grey[400]!, width: 1.5),
  shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(12)),
)
```

### Card Styling

**Standard Card**
```dart
Container(
  decoration: BoxDecoration(
    color: Colors.white,
    borderRadius: BorderRadius.circular(12),
    boxShadow: [
      BoxShadow(
        color: Colors.black.withOpacity(0.06),
        blurRadius: 8,
        offset: Offset(0, 2),
      ),
    ],
  ),
)
```

**Gradient Card**
```dart
Container(
  decoration: BoxDecoration(
    gradient: LinearGradient(
      colors: [Color(0xFF2E5FB3), Color(0xFF1E3A8A)],
      begin: Alignment.topLeft,
      end: Alignment.bottomRight,
    ),
    borderRadius: BorderRadius.circular(16),
    boxShadow: [
      BoxShadow(
        color: Color(0xFF2E5FB3).withOpacity(0.3),
        blurRadius: 12,
        offset: Offset(0, 6),
      ),
    ],
  ),
)
```

### Background Gradient

```dart
Container(
  decoration: BoxDecoration(
    gradient: LinearGradient(
      begin: Alignment.topCenter,
      end: Alignment.bottomCenter,
      colors: [
        Color(0xFFF5F7FA),
        Color(0xFFE8EEF7),
      ],
    ),
  ),
)
```

## Animation Timings

```
Quick:   200ms (micro-interactions)
Normal:  300-400ms (standard transitions)
Slider:  1000ms (focus animations)
Page:    1200ms (complex animations)
```

## Icon Usage

```dart
Icons.check_circle_rounded      // Correct
Icons.cancel_rounded            // Wrong / Close
Icons.schedule                  // Timer
Icons.play_arrow                // Start
Icons.arrow_back                // Back
Icons.arrow_forward             // Next
Icons.home                      // Home
Icons.assignment                // Review
Icons.description               // Info
Icons.preview                   // Preview
Icons.help_outline              // Questions count
```

## Opacity Levels

```
Hover:    withOpacity(0.1)
Disabled: withOpacity(0.2)
Subtle:   withOpacity(0.3)
Medium:   withOpacity(0.5)
Strong:   withOpacity(0.7)
Opaque:   withOpacity(1.0)
```

## Device Breakpoints

```
Mobile:    < 600dp
Tablet:    600dp - 1200dp
Desktop:   > 1200dp
```

## Responsive Padding

```dart
// Mobile
padding: EdgeInsets.all(16),

// Tablet
@media(minWidth: 600)
padding: EdgeInsets.all(24),

// Desktop
@media(minWidth: 1200)
padding: EdgeInsets.all(32),
```

## Color Gradients Used

### App Gradient
```dart
LinearGradient(
  begin: Alignment.topCenter,
  end: Alignment.bottomCenter,
  colors: [Color(0xFFF5F7FA), Color(0xFFE8EEF7)],
)
```

### Blue Gradient (Headers)
```dart
LinearGradient(
  begin: Alignment.topLeft,
  end: Alignment.bottomRight,
  colors: [Color(0xFF2E5FB3), Color(0xFF1E3A8A)],
)
```

### Grade Gradient (Dynamic)
```dart
Color getGradeColor(double percentage) {
  if (percentage >= 80) return Color(0xFF10B981);
  if (percentage >= 60) return Color(0xFFF59E0B);
  return Color(0xFFEF4444);
}
```

## Animation Curves

```dart
Curves.easeOut       // Opening/appearing
Curves.easeInOut     // Smooth transitions
Curves.bounceOut     // Playful reveals
Curves.linear        // Steady progress
Curves.decelerate    // Natural ending
```

## Text Styles Presets

```dart
// Hero Text
TextStyle(fontSize: 56, fontWeight: FontWeight.bold, color: Colors.white)

// Title
TextStyle(fontSize: 20, fontWeight: FontWeight.bold, color: Color(0xFF1E3A8A))

// Body
TextStyle(fontSize: 14, color: Colors.grey[700])

// Small
TextStyle(fontSize: 12, color: Colors.grey[600], fontWeight: FontWeight.w500)
```

## Accessibility

### Contrast Ratios (WCAG AA)
- Text on color(0xFF2E5FB3): Use white or very light text
- Text on white: Use dark blue or black text
- Success green: Works with white or very dark text
- Error red: Works with white text

### Touch Targets
- Minimum size: 48x48 dp
- Buttons: 16dp padding on all sides
- Spacing between clickables: 8dp minimum

## Common Combinations

### Success State
- Color: #10B981 (Green)
- Icon: Icons.check_circle_rounded
- Text: White or dark

### Error State
- Color: #EF4444 (Red)
- Icon: Icons.cancel_rounded
- Text: White or dark

### Warning State
- Color: #F59E0B (Orange)
- Icon: Icons.warning_amber_rounded
- Text: Dark

### Info State
- Color: #2E5FB3 (Blue)
- Icon: Icons.info_rounded
- Text: White

## Loading States

```dart
// Loading spinner
CircularProgressIndicator(
  valueColor: AlwaysStoppedAnimation(Color(0xFF2E5FB3)),
  strokeWidth: 3,
)

// Loading text
Text('Loading...', style: TextStyle(fontSize: 14, color: Colors.grey[600]))
```

## Empty States

```dart
Center(
  child: Icon(Icons.inbox, size: 64, color: Colors.grey[400]),
  Text('No items found', style: TextStyle(color: Colors.grey[600])),
)
```

## Error States

```dart
Icon(Icons.error_outline, size: 64, color: Colors.red[400]),
Text('Error occurred', style: TextStyle(color: Colors.grey[700])),
ElevatedButton.icon(
  icon: Icon(Icons.refresh),
  label: Text('Retry'),
  style: ElevatedButton.styleFrom(backgroundColor: Color(0xFF2E5FB3)),
)
```

---

## Copy-Ready Code Snippets

### Full Background
```dart
Container(
  decoration: BoxDecoration(
    gradient: LinearGradient(
      begin: Alignment.topCenter,
      end: Alignment.bottomCenter,
      colors: [
        Color(0xFFF5F7FA),
        Color(0xFFE8EEF7),
      ],
    ),
  ),
  child: your_content_here,
)
```

### Floating Action Button Style
```dart
FloatingActionButton(
  onPressed: () {},
  backgroundColor: Color(0xFF2E5FB3),
  child: Icon(Icons.add),
)
```

### Chip Style
```dart
Chip(
  label: Text('Label'),
  backgroundColor: Color(0xFF2E5FB3).withOpacity(0.1),
  labelStyle: TextStyle(color: Color(0xFF2E5FB3)),
)
```

---

**Last Updated**: 2026-02-09  
**Version**: 1.0  
**Status**: Production Ready
