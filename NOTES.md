# Patch notes

## Summary of changes

- Grouped the title/description search conditions so archive and status filters apply to every match in the Spring query and both SQL reference files.
- Changed the default task ordering to oldest-created first across the backend and SQL references.
- Removed the artificial per-request delay. Invalid status, page, and pageSize inputs now receive HTTP 400 responses, and pagination index arithmetic avoids integer overflow.
- Cancelled obsolete frontend requests, cleared loading/error state reliably, and reset to page 1 when search or status filters change.

## What I chose not to change

The repository still loads every matching task before slicing a page in memory. I left that larger pagination change out to keep this patch focused.

## Biggest remaining risk

As the task table grows, fetching all matching rows for each request can consume excess memory and increase response time. Database-level pagination and a matching count query should be the next improvement.

## Tools and AI

I used Copilot SDK in VS Code to inspect the code and help implement the focused fixes. I reviewed the changes and verified them with frontend and backend builds plus live API smoke checks. The backend currently has no automated test sources.
