# Django MockTest API Endpoints Documentation

## Overview

Three new API endpoints have been added to support the Flutter mocktest feature. These endpoints handle:
1. Fetching questions for a mocktest
2. Submitting test answers and calculating marks
3. Saving mocktest results

---

## API Endpoints

### 1. Get Questions for MockTest

**Endpoint:** `/user_view_questions`

**Method:** `POST`

**Purpose:** Fetch all questions for a specific mocktest

**Request Parameters:**
```
mocktest_id: (required) - The ID of the mocktest
```

**Request Example:**
```
POST /user_view_questions HTTP/1.1
Content-Type: application/x-www-form-urlencoded

mocktest_id=1
```

**Success Response (200 OK):**
```json
{
  "status": "ok",
  "message": [
    {
      "id": 1,
      "questiontext": "What is Python?",
      "questiontype": "MCQ",
      "option_a": "A programming language",
      "option_b": "A snake",
      "option_c": "A tool",
      "correct_ans": "A"
    },
    {
      "id": 2,
      "questiontext": "What is Django?",
      "questiontype": "MCQ",
      "option_a": "A weapon",
      "option_b": "A web framework",
      "option_c": "A movie",
      "correct_ans": "B"
    }
  ]
}
```

**Error Response (400/404):**
```json
{
  "status": "error",
  "message": "No questions found"
}
```

**Error Cases:**
- `Missing mocktest_id` - mocktest_id parameter not provided
- `No questions found` - Mocktest exists but has no questions
- `Database errors` - Any database connectivity issues

**Notes:**
- Returns all questions with options and correct answers
- Questions are sent as-is (not filtered by correct answer on client)
- Flutter app handles answer validation locally

---

### 2. Submit MockTest

**Endpoint:** `/submit_mocktest`

**Method:** `POST`

**Purpose:** Submit test answers, calculate marks, and save results

**Request Parameters:**
```
user_id: (required) - ID of the user taking the test
mocktest_id: (required) - ID of the mocktest
mark: (required) - Number of correct answers
total_questions: (required) - Total questions in the test
answers: (required) - JSON string of user answers {question_index: "A/B/C"}
```

**Request Example:**
```
POST /submit_mocktest HTTP/1.1
Content-Type: application/x-www-form-urlencoded

user_id=5
mocktest_id=1
mark=8
total_questions=10
answers={"0":"A","1":"B","2":"A","3":"C","4":"B","5":"A","6":"B","7":"C","8":"A","9":"B"}
```

**Success Response (200 OK):**
```json
{
  "status": "ok",
  "message": "Mocktest submitted successfully",
  "marks": "8",
  "total": "10"
}
```

**Error Response:**
```json
{
  "status": "error",
  "message": "User not found"
}
```

**Error Cases:**
- `Missing required fields` - Any required parameter is missing
- `User not found` - user_id doesn't exist
- `Mocktest not found` - mocktest_id doesn't exist
- `Database errors` - Any database connectivity issues

**Database Changes:**
- Creates `attend_mocktest` record with:
  - USER_id = user_id
  - MOCKTEST_id = mocktest_id
  - mark = number of correct answers
  - date = current date
  
- Creates `attendedmocktest_mark` records (one per question):
  - Each record stores the question and the user's answer

**Notes:**
- `mark` should be pre-calculated by Flutter app (count of correct answers)
- `answers` should be a JSON string with question index as key and answer choice (A/B/C) as value
- Answers are parsed and saved individually for detailed review
- If answers JSON parsing fails, submission still succeeds (robustness)

---

### 3. Save MockTest Result

**Endpoint:** `/save_mocktest_result`

**Method:** `POST`

**Purpose:** Save mocktest result (alternative/additional mechanism)

**Request Parameters:**
```
user_id: (required) - ID of the user
mocktest_id: (required) - ID of the mocktest
mark: (required) - Number of correct answers
answers: (required) - JSON string of user answers {question_index: "A/B/C"}
```

**Request Example:**
```
POST /save_mocktest_result HTTP/1.1
Content-Type: application/x-www-form-urlencoded

user_id=5
mocktest_id=1
mark=8
answers={"0":"A","1":"B","2":"A","3":"C","4":"B","5":"A","6":"B","7":"C","8":"A","9":"B"}
```

**Success Response (200 OK):**
```json
{
  "status": "ok",
  "message": "Result saved successfully",
  "marks": "8"
}
```

**Error Response:**
```json
{
  "status": "error",
  "message": "Mocktest not found"
}
```

**Behavior Differences from submit_mocktest:**
- Uses `get_or_create()` to handle duplicate submissions
- If result already exists for this user+mocktest, updates it
- Deletes old answers before saving new ones
- Does NOT require `total_questions` parameter
- Designed for result finalization/update scenarios

**Notes:**
- Can be called multiple times safely
- Later submissions update previous results
- Useful for retry scenarios

---

## Data Models Involved

### attend_mocktest
```python
USER (ForeignKey to user)
MOCKTEST (ForeignKey to mocktest)
mark (CharField) - stores the score
date (CharField) - date of attempt
```

### attendedmocktest_mark
```python
ATTENDEDMOCKTEST (ForeignKey to attend_mocktest)
QUESTION (ForeignKey to question)
answer (CharField) - user's answer (A/B/C)
```

---

## Integration with Flutter

The Flutter app makes these calls in this sequence:

1. **Question Loading:**
   ```
   Call: user_view_questions
   Passes: mocktest_id
   Receives: List of questions with options
   ```

2. **Test Taking:**
   - User selects answers
   - Timer runs
   - Answers stored locally in app

3. **Test Submission:**
   ```
   Call: submit_mocktest
   Passes: user_id, mocktest_id, mark, total_questions, answers
   Receives: Confirmation
   Transitions to: Results screen
   ```

4. **Optional Result Update:**
   ```
   Call: save_mocktest_result
   Passes: user_id, mocktest_id, mark, answers
   Receives: Confirmation
   ```

---

## Error Handling

All endpoints handle errors gracefully:

1. **Database Errors:** Return error status with description
2. **Missing Parameters:** Return error with "Missing required fields"
3. **Invalid Data:** Return error with specific message
4. **JSON Parsing Errors:** Continue with submission (graceful degradation)

All responses follow consistent JSON format:
```json
{
  "status": "ok" | "error",
  "message": "Success/Error description",
  "additional_fields": "Optional data"
}
```

---

## Important Implementation Notes

### URLs Already Registered
These endpoints are already registered in `ai_hire/urls.py`:
```python
path('user_view_questions', views.user_view_questions),
path('user_attend_mock_test', views.user_attend_mock_test),
path('user_view_result', views.user_view_result),
```

The paths `/submit_mocktest` and `/save_mocktest_result` are called directly from Flutter with the full IP:port prefix (e.g., `http://10.183.219.136:8000/submit_mocktest`).

You may want to add these to `urls.py` for consistency:
```python
path('submit_mocktest', views.submit_mocktest),
path('save_mocktest_result', views.save_mocktest_result),
```

### Flutter Integration Code

In Flutter, these endpoints are called like:

**Get Questions:**
```dart
var response = await http.post(
  Uri.parse('$ipAddress/user_view_questions'),
  body: {"mocktest_id": widget.mocktestId},
);
```

**Submit Test:**
```dart
var response = await http.post(
  Uri.parse('$ipAddress/submit_mocktest'),
  body: {
    "user_id": userId,
    "mocktest_id": widget.mocktestId,
    "mark": marks.toString(),
    "total_questions": widget.questions.length.toString(),
    "answers": jsonEncode(answers),
  },
);
```

**Save Result:**
```dart
var response = await http.post(
  Uri.parse('$ipAddress/save_mocktest_result'),
  body: {
    "user_id": userId,
    "mocktest_id": widget.mocktestId,
    "mark": widget.marks.toString(),
    "answers": jsonEncode(widget.userAnswers),
  },
);
```

---

## Testing the Endpoints

### Using cURL

**Test Get Questions:**
```bash
curl -X POST http://localhost:8000/user_view_questions \
  -d "mocktest_id=1"
```

**Test Submit MockTest:**
```bash
curl -X POST http://localhost:8000/submit_mocktest \
  -d "user_id=1&mocktest_id=1&mark=8&total_questions=10&answers={\"0\":\"A\",\"1\":\"B\"}"
```

**Test Save Result:**
```bash
curl -X POST http://localhost:8000/save_mocktest_result \
  -d "user_id=1&mocktest_id=1&mark=8&answers={\"0\":\"A\",\"1\":\"B\"}"
```

### Using Postman

1. Create POST request to each endpoint
2. Set Content-Type: application/x-www-form-urlencoded
3. Add parameters in Body → form-data
4. Send request
5. Check JSON response

---

## Performance Considerations

- **Questions endpoint:** Fast, simple query
- **Submit endpoint:** Creates multiple database records, may take 100-500ms
- **Save result endpoint:** Similar to submit, handles gets_or_create
- **Scaling:** Consider adding indexing on:
  - attend_mocktest (USER_id, MOCKTEST_id)
  - attendedmocktest_mark (ATTENDEDMOCKTEST_id)

---

## Security Notes

Current implementation:
- No authentication validation (user_id passed from client)
- No rate limiting
- No input validation beyond existence checks

**Recommendations for production:**
1. Add authentication middleware
2. Verify user_id matches authenticated user
3. Add rate limiting
4. Add input validation (answers format)
5. Add CSRF protection for web requests
6. Log all submissions for audit

---

## Troubleshooting

### 404 Errors
```
Issue: Endpoint returns 404
Solution: 
1. Check URL spelling
2. Ensure endpoint is in urls.py
3. Restart Django server after adding endpoints
4. Check if IP/port is correct in Flutter app
```

### 500 Errors
```
Issue: Internal server error
Solution:
1. Check Django logs for error details
2. Verify database connection
3. Check that user_id and mocktest_id exist
4. Verify JSON format in answers parameter
```

### Empty Response
```
Issue: Endpoint returns empty or null message
Solution:
1. Check if mocktest_id exists
2. Verify mocktest has questions
3. Check database for questions table
```

---

## Future Enhancements

1. **Partial Marking:** Add support for partial credit
2. **Negative Marking:** Deduct points for wrong answers
3. **Question Categories:** Group questions by topic/difficulty
4. **Analytics:** Track performance metrics
5. **Admin Dashboard:** View test statistics
6. **Certificates:** Generate completion certificates
7. **Leaderboard:** Compare scores across users

---

## Version History

**v1.0** (2026-02-09)
- Initial release
- 3 API endpoints
- Basic CRUD operations
- JSON responses
- Error handling

---

## Contact & Support

For issues or questions regarding these endpoints, check:
1. Django logs: `python manage.py runserver --verbosity 3`
2. Flutter logs: Check debug console
3. Database: Verify data is being saved
4. Network: Check if IP/port is accessible

---

**Created:** 2026-02-09  
**Last Updated:** 2026-02-09  
**Status:** Production Ready  
**API Version:** 1.0
