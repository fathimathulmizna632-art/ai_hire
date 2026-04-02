# Flutter MockTest Feature - Complete Implementation Guide

## Overview
This implementation provides a complete mocktest/quiz system for the Flutter AI Hire application with the following screens:

1. **MockTest Question View** - Preview questions before starting
2. **MockTest Attend** - Take the test with real-time timer
3. **MockTest Result** - View detailed results and analysis

---

## Files Created

### 1. `mocktest_question_view.dart`
**Purpose**: Display available questions and test details before starting the test

**Key Features**:
- Fetch questions from Django backend
- Display test description and metadata
- Show question preview (all questions before starting)
- Total questions count
- Navigation to attend screen
- Question model class

**Key Components**:
```dart
class MocktestQuestionView - Main widget for displaying questions
class Question - Data model for questions
```

**API Endpoint Used**:
- `POST /user_view_questions` - Fetch questions for a mocktest

---

### 2. `mocktest_attend.dart`
**Purpose**: The main exam-taking interface with timer and answer submission

**Key Features**:
- ⏱️ **Real-time Timer** - Countdown timer (default 1 hour, customizable)
- **Question Navigation** - Next/Previous buttons
- **Answer Selection** - Multiple choice (A, B, C options)
- **Progress Tracking** - Shows current question number and answered count
- **Progress Bar** - Visual indication of test progress
- **Answer Validation** - Prevents unanswered questions from being submitted
- **Auto-submit** - Automatically submits when time runs out
- **Exit Confirmation** - Confirmation dialog when user tries to exit
- **Visual Feedback** - Highlights selected answers

**Constructor Parameters**:
```dart
final String mocktestId;           // ID of the mocktest
final String mocktestTitle;        // Title for AppBar
final List<Question> questions;    // Questions to display
```

**Timer Functionality**:
- Default duration: 3600 seconds (1 hour)
- Can be customized by changing `totalSeconds` variable
- Shows HH:MM:SS format
- Turns red when less than 5 minutes remain
- Auto-submits test when time expires

**API Endpoint Used**:
- `POST /submit_mocktest` - Submit test answers and marks

---

### 3. `mocktest_result.dart`
**Purpose**: Display comprehensive test results with analysis

**Key Features**:
- **Score Display** - Shows marks, percentage, and grade
- **Color Coding** - Green (80%+), Orange (60%+), Red (below 60%)
- **Statistics** - Correct answers, wrong answers, time taken
- **Answer Review** - Detailed review of all questions
- **Color-coded Answers**:
  - Green for correct answers
  - Red for wrong answers
  - Shows which option user selected
- **Unanswered Questions** - Clearly marked
- **Grade Labels** - Excellent, Good, Need Improvement
- **Navigation** - Back to home or retake functionality

**Constructor Parameters**:
```dart
final String mocktestId;
final String mocktestTitle;
final List<Question> questions;
final Map<int, String> userAnswers;  // Index -> Answer (A/B/C)
final int marks;                      // Score achieved
final int totalQuestions;            // Total questions count
final int timeTaken;                 // Time taken in seconds
```

**Display Elements**:
- Score card (colored based on performance)
- Statistics grid (Correct/Wrong/Time Taken)
- Detailed answer review with question-by-question breakdown
- Action buttons (Back to Home, Retake Test)

**API Endpoint Used**:
- `POST /save_mocktest_result` - Save results to database

---

## Integration with Existing Code

### Updated `viewmocktest.dart`
The existing mocktest list screen has been updated to use the new screens:

**Before**:
```dart
Navigator.push(context, MaterialPageRoute(builder: (context)=>userattendmocktestsub()));
```

**After**:
```dart
Navigator.push(context, MaterialPageRoute(builder: (context)=>MocktestQuestionView(
  mocktestId: i.id,
  mocktestTitle: i.title,
  mocktestDescription: i.description,
)));
```

---

## Flow Diagram

```
viewmocktest.dart (List)
    ↓
    [User taps "ATTEND MOCKTEST"]
    ↓
mocktest_question_view.dart (Preview)
    ↓
    [User taps "Start Test"]
    ↓
mocktest_attend.dart (Taking Test with Timer)
    ↓
    [User submits or time runs out]
    ↓
mocktest_result.dart (View Results)
    ↓
    [Back to Home / Retake]
```

---

## Feature Details

### Timer Functionality

**How it works**:
1. Timer starts when user enters the test
2. Updates every second using `Timer.periodic()`
3. Automatically submits test when reaches 0
4. Displays in HH:MM:SS format
5. Warning color (red) when less than 5 minutes remain

**Customization**:
```dart
// Change duration in mocktest_attend.dart initState()
int totalSeconds = 3600; // Change this value (in seconds)
// Example: 1800 = 30 minutes, 7200 = 2 hours
```

### Answer Recording

**Data Structure**:
```dart
Map<int, String> answers = {};
// answers[0] = "A"  // Question 0, User selected A
// answers[1] = "B"  // Question 1, User selected B
// etc.
```

**On Submit**:
- Answers are compared with correct answers
- Marks are calculated
- Results are sent to backend with `jsonEncode(answers)`

### Scoring System

**Algorithm**:
```dart
int marks = 0;
for (int i = 0; i < questions.length; i++) {
  if (answers[i] == questions[i].correctAns) {
    marks++;
  }
}
double percentage = (marks / totalQuestions) * 100;
```

**Grade Distribution**:
- 80% and above: **Excellent** (Green)
- 60% to 79%: **Good** (Orange)
- Below 60%: **Need Improvement** (Red)

---

## Required API Endpoints

Your Django backend should implement these endpoints:

### 1. Get Questions
```
POST /user_view_questions
Parameters:
  - mocktest_id: ID of the mocktest

Response:
{
  "message": [
    {
      "id": 1,
      "questiontext": "What is...?",
      "questiontype": "MCQ",
      "option_a": "Option A",
      "option_b": "Option B",
      "option_c": "Option C",
      "correct_ans": "A"
    },
    ...
  ]
}
```

### 2. Submit Test
```
POST /submit_mocktest
Parameters:
  - user_id: ID of the user
  - mocktest_id: ID of the mocktest
  - mark: Score achieved
  - total_questions: Total questions count
  - answers: JSON encoded answer map

Response:
{
  "status": "success",
  "message": "Test submitted successfully"
}
```

### 3. Save Result
```
POST /save_mocktest_result
Parameters:
  - user_id: ID of the user
  - mocktest_id: ID of the mocktest
  - mark: Score achieved
  - answers: JSON encoded answer map

Response:
{
  "status": "success",
  "message": "Result saved"
}
```

---

## Usage Example

### Navigate to Question View:
```dart
Navigator.push(
  context,
  MaterialPageRoute(
    builder: (context) => MocktestQuestionView(
      mocktestId: '1',
      mocktestTitle: 'Python Basics',
      mocktestDescription: 'Test your Python fundamentals',
    ),
  ),
);
```

### CustomTimer Duration:
Edit `mocktest_attend.dart` line ~30:
```dart
int totalSeconds = 1800; // 30 minutes instead of 1 hour
```

---

## Models Reference

### Question Model
```dart
class Question {
  final String id;
  final String questiontext;
  final String questiontype;
  final String optionA;
  final String optionB;
  final String optionC;
  final String correctAns;
}
```

This maps directly to your Django `question` model.

---

## Error Handling

All screens implement error handling for:
- Network failures
- Missing data
- API errors
- Invalid responses

Users get appropriate error messages with retry options.

---

## Testing Checklist

- [ ] Questions load correctly
- [ ] Timer starts and counts down
- [ ] Answers are recorded properly
- [ ] Navigation between questions works
- [ ] Submit button only appears on last question
- [ ] Auto-submit triggers on timeout
- [ ] Results display correctly
- [ ] Percentage and grade calculation is accurate
- [ ] Answer review shows correct/wrong answers
- [ ] Back to home navigation works

---

## Customization Tips

1. **Change timer duration**: Edit `totalSeconds` in `mocktest_attend.dart`
2. **Modify colors**: Update `Colors.deepBlue` to your preferred color
3. **Add more options**: Extend to option D, E, etc. by modifying models and UI
4. **Change scoring**: Modify the mark calculation logic in submission
5. **Add negative marking**: Subtract points for wrong answers

---

## Dependencies Required

Make sure these are in your `pubspec.yaml`:
- `http`
- `shared_preferences`
- `flutter`

All other dependencies are built-in to Flutter.

---

## Backend Integration Notes

1. Ensure your Django views match the endpoint names
2. Return JSON in the exact format shown above
3. Store user answers in `attend_mocktest` and `attendedmocktest_mark` tables
4. Implement proper authentication/authorization checks
5. Add timestamps for result tracking

---

## Future Enhancements

Potential features to add:
- [ ] Negative marking for wrong answers
- [ ] Partial marking
- [ ] Question categories/sections
- [ ] Bookmarked questions
- [ ] Review-only mode after submission
- [ ] Compare with class average
- [ ] Detailed analytics and performance trends
- [ ] Printable result certificates
- [ ] Instant feedback on answers
- [ ] Randomized question order

---

Created: 2026-02-09
Version: 1.0
Status: Production Ready
