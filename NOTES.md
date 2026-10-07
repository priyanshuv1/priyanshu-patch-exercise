# Patch Notes

## Changes

1. Fixed task search/status filtering in `TaskRepository`.
   The original SQL had incorrect AND/OR precedence, causing status filtering and archived-task filtering to behave incorrectly. Added parentheses so archived, search, and status conditions are applied correctly.

2. Removed the artificial `Thread.sleep()` delay from `TaskController`.
   The delay blocked request threads and made short searches unnecessarily slow.

3. Added 400ms debounce to frontend task searches in `useTasks`.
   This prevents an API request for every keystroke and only searches after the user stops typing.

4. Reset pagination to page 1 when search or status changes.
   This prevents empty pages when a new filter has fewer results.

5. Added pagination input validation.
   Invalid page/pageSize values are normalized to safe defaults instead of causing errors or meaningless responses.

## Validation

Tested status filtering through the API, invalid pagination values, search behavior, pagination reset, and the normal UI flow. Backend tests and frontend production build both pass.

## Not Changed

I did not rewrite the existing architecture or replace the database/query approach because the assignment is timeboxed and the existing structure was sufficient for these fixes.

## Biggest Remaining Risk

The frontend still depends on the backend API being available and does not have comprehensive automated UI tests. More extensive testing could catch edge cases not covered by the manual smoke tests.

## Tools / AI

Used terminal tools, curl, browser DevTools, and AI assistance to inspect the code, identify likely issues, and validate focused fixes. All changes were reviewed and tested manually.