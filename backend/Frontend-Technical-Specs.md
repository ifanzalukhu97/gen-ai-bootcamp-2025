# Frontend Technical Specs

## Pages

### Dashboard `/dashboard`

#### Purpose
The purpose of this page is to provide a summary of learning
and act as the default landing page for the application.

#### Components
This page contains the following components:
- Last Study Session
  - show last activity used
  - show when last activity used
  - summarizes wrong vs correct from last activity
  - has link the group
  
- Study Progress
  - total words study eg. 3/124
    - across all study session show the total words studied out of all possible words in our database
    - display a mastery progress eq. 0%

- Quick Stats
  - Success rate eq. 80%
  - total study session eq. 4
  - total active group eq. 3
  - study streak eq. 4 days
  
- Start Study Button
  - goes to study activities page

#### Needed API Endpoints
- GET /api/dashboard/last_study_session
- GET /api/dashboard/study_progress
- GET /api/dashboard/quick_stats


### Study Activities `/study_activities`

#### Purpose
The purpose of this page is to provide a list of study activities
with thumbnails, and it's name, and a button to lunch / view the activity.

#### Components
- Study Activity Card
  - Thumbnail of the activity
  - Name of the activity
  - Lunch Button to take us the lunch page
  - View Button to view more information about past study sessions for this study activity

#### Needed API Endpoints
- GET /api/study_activities


### Study Activity Details `/study_activities/:id`
#### Purpose
The purpose of this page is to provide more information about a specific study activity
and a list of past study sessions for this activity.

#### Components
- Thumbnail of the activity
- Name of the activity
- Lunch Button to take us the lunch page
- Study Activities Paginated List
  - id
  - activity name
  - group name
  - start time
  - end time (inferred from the last word review item submitted)
  - number of review items

#### Needed API Endpoints
- GET /api/study_activities/:id
- GET /api/study_activities/:id/study_sessions


### Study Activities Lunch `/study_activities/:id/lunch`
#### Purpose
The purpose of this page is to lunch a study activity.

#### Components
- Name of study activity
- Lunch form
  - select field for group
  - lunch now button

#### Behavior
After the form is submitted, a new tab opens with the study based on it's URL
provided in the database.

Also, the after form is submitted, the page will be redirected to the study session show page.

#### Needed API Endpoints
- POST /api/study_activities


### Word `/words`

#### Purpose
The purpose of this page is to show all words  in our database.

#### Components
- Paginated List of Words
  - Columns
      - word
      - correct count
      - wrong count
  - Pagination with 100 items per page
  - Clicking on a word will take us to the word show page

#### Needed API Endpoints
- GET /api/words


### Word Detail `/words/:id`

#### Purpose
The purpose of this page is to show more information about a specific word.

#### Components
- Word
- Study Statistics
  - Correct Count
  - Wrong Count
- Word Group
  - Show a series of pills eq. tags
  - When group name is clicked, it will take us to the group show page

#### Needed API Endpoints
- GET /api/words/:id


### Word Group `/groups`

#### Purpose
The purpose of this page is to show a list of groups in our database.

#### Components
- Paginated List of Groups
  - Columns
      - Group Name
      - Word Count
  - Clicking on a group will take us to the group show page

#### Needed API Endpoints
- GET /api/groups



### Group Detail `/groups/:id`

#### Purpose
The purpose of this page is to show more information about a specific group.

#### Components
- Group Name
- Group Statistics
  - Total Word Count
- Word in Group (Paginated List of Words)
  - Should use the same component as the word index page
- Study Sessions
  - Show use the same component as the study session index page

#### Needed API Endpoints
- GET /api/groups/:id (the name and group statistics)
- GET /api/groups/:id/words
- GET /api/groups/:id/study_sessions


### Study Session `/study_sessions`

#### Purpose
The purpose of this page is to show a list of study sessions in our database.

#### Components
- Paginated List of Study Sessions
  - Columns
      - Id 
      - Activity Name
      - Group Name
      - Start Time
      - End Time
      - Number of Review Items
  - Clicking on a study session will take us to the study session show page

#### Needed API Endpoints
- GET /api/study_sessions


### Study Session Detail `/study_sessions/:id`
#### Purpose
The purpose of this page is to show more information about a specific study session.

#### Components
- Study Session
  - Activity Name
  - Group Name
  - Start Time
  - End Time
  - Number of Review Items
- Word Review Items (Paginated List of Word)
  - Should use the same component as the word index page

#### Needed API Endpoints
- GET /api/study_sessions/:id
- GET /api/study_sessions/:id/words


### Settings Page `/settings`
#### Purpose
The purpose of this page is to make configuration changes to the application.

#### Components
- The theme switcher
  - light mode
  - dark mode
  - system mode
- Load Seed Data Button
- Reset History Button
  - this will delete all study sessions and word review items
- Full Reset Button
  - this will drop all tables and recreate with seed data

#### Needed API Endpoints
- POST /api/reset_history
- POST /api/full_reset