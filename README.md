# ACSS - Automated Course Scheduling System

## Project Description
The Automated Course Scheduling System (ACSS) is a web-based application designed to streamline the process of managing academic schedules for various roles within an educational institution, including Admin, Director, Dean, Chair, and Faculty. It provides functionalities for user management, course and classroom management, schedule generation, activity logging, and profile management.

## Recent Updates and Modifications

This section outlines the recent improvements and bug fixes implemented in the system.

### 1. PHP Header Issue Resolution
**Issue:** Previously, the system encountered "Warning: http_response_code(): Cannot set response code - headers already sent" errors. This occurred because output (e.g., HTML from a view) was being sent to the browser before the HTTP status code could be set by `http_response_code()`.
**Resolution:** The routing logic in `public/index.php` was refactored. Specifically, `break;` statements following controller calls in various `switch` cases (within `handleDirectorRoutes`, `handleDeanRoutes`, `handleChairRoutes`, and public routes) were replaced with `exit;`. This ensures that script execution terminates immediately after a controller has handled a request and rendered its output, preventing any further attempts to modify HTTP headers.

### 2. UI/UX Improvement: Sidebar Footer Positioning
**Issue:** In the admin interface, the sidebar footer (containing "Online" status) would sometimes overlap clickable elements within the sidebar when scrolling, leading to a poor user experience.
**Resolution:** The styling for the sidebar footer in `src/views/admin/layout.php` was adjusted. The `absolute bottom-0 left-0 right-0` positioning was removed, and `mt-auto` was added. This change ensures that the footer is now part of the natural document flow within the scrollable sidebar, allowing it to scroll along with the navigation items and preventing any overlap.

### 3. PHP Deprecation Notices (htmlspecialchars)
**Issue:** Deprecation warnings related to `htmlspecialchars()` being called with `null` values were reported in `src/views/admin/profile.php`.
**Resolution:** Upon inspection, it was found that the relevant lines in `src/views/admin/profile.php` already correctly utilize the null coalescing operator (`?? ''`) to provide an empty string default when a variable might be `null`. This indicates that the deprecation notices were either from an older version of the codebase or a caching issue, and the fix was already in place. No further code modifications were required for this specific issue.

### 4. UI/UX Improvement: Admin Sidebar Footer Text
**Issue:** The admin sidebar footer displayed "VPAA System," which was inconsistent with the "Admin" role.
**Resolution:** The text "VPAA System" in `src/views/admin/layout.php` was changed to "Admin System" for clarity and consistency with the administrative role.
