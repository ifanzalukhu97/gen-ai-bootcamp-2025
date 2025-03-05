# Backend Server Technical Specs

## Business Goal:
A language learning school wants to build a prototype of learning portal which will act as three things:
- Inventory of possible vocabulary that can be learned
- Act as a  Learning record store (LRS), providing correct and wrong score on practice vocabulary
- A unified launchpad to launch different learning apps

## Technical Requirements:
- The backend will be built using .NET Core 8.0
- The database will be SQLite3
- The API always returns JSON
- There will be no authentication or authorization required
- Everything will be treated as a single user

## Database Schema:
We have the following tables:
- **words** - stored vocabulary words
  - id integer
  - word string
  - parts json

- **words_group** - join table for words and groups. Many-to-many relationship
  - id integer
  - word_id integer
  - group_id integer
  
- **groups** - thematic groups of words
  - id integer
  - name string
  - words_count integer

- **study_sessions** - records of study sessions grouping word_review_items
  - id integer
  - group_id integer
  - study_activity_id integer
  - created_at timestamp

- **study_activities** - a specific study activity, linking to a study session to group
  - id integer
  - name string
  - url string
  
- **word_review_items** - a record of word practice, determining if the word was correct or wrong
  - id integer
  - word_id integer
  - study_session_id integer
  - correct boolean
  - created_at timestamp

## API Endpoints:
- GET /api/dashboard/last_study_session
- GET /api/dashboard/study_progress
- GET /api/dashboard/quick_stats
- GET /api/study_activities
- GET /api/study_activities/:id
- GET /api/study_activities/:id/study_sessions
- POST /api/study_activities
  - required params : group_id, study_activity_id

- GET /api/words
  - pagination with 100 items per page
- GET /api/groups/:id/words

- GET /api/groups 
  - pagination with 100 items per page
- GET /api/groups/:id
- GET /api/groups/:id/study_sessions

- GET /api/study_sessions
- GET /api/study_sessions/:id
- GET /api/study_sessions/:id/words

- POST /api/reset_history
- POST /api/full_reset

- POST /api/study_sessions/:id/words/:word_id/review
  - required params : word_id, correct
