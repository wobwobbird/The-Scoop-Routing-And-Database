# The-Scoop (Routing & Database Task)

Task for the CodeAcademy course **Create a Back-End App with JavaScript**

## Add Comment Functionality and YAML Persistence

### Purpose
This PR implements the missing comment system for The Scoop web application, allowing users to create, edit, delete, and vote on comments. Additionally, it adds YAML-based database persistence to maintain data across server restarts.

### Changes Made

#### Comment System Implementation
- **Database Structure**: Added `comments` object and `nextCommentId` counter to the database
- **Routes**: Implemented 5 new comment routes:
  - `POST /comments` - Create new comments
  - `PUT /comments/:id` - Update comment body
  - `DELETE /comments/:id` - Delete comments and clean up references
  - `PUT /comments/:id/upvote` - Upvote comments
  - `PUT /comments/:id/downvote` - Downvote comments
- **Handler Functions**: Created all corresponding route handlers following the existing article pattern, including proper validation, error handling, and bidirectional linking between comments, users, and articles

#### YAML Persistence (Bonus)
- **saveDatabase()**: Saves the current database state to `config.yml` after each request
- **loadDatabase()**: Loads database from `config.yml` on server startup with error handling for missing files
- Uses the `figg` library for YAML file operations

### Testing
- All tests pass successfully using the provided test suite (`npm test`)
- Verified edge cases including missing IDs, invalid usernames, non-existent articles, and proper error handling
- Confirmed data persistence works correctly across server restarts

### Technical Details
- All comment routes follow the same patterns as existing article routes for consistency
- Proper cleanup of comment references in both user and article objects when comments are deleted
- Error handling includes appropriate HTTP status codes (400, 404, 201, 200, 204)
- YAML persistence includes try/catch error handling to gracefully handle missing config files on first run
