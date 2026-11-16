# Copilot instructions for Mergington High School Activities API

## Project overview
- This repository is a small FastAPI application for a high-school activities board.
- The API lives in `src/app.py`; the UI assets live in `src/static/` (`index.html`, `app.js`, and `styles.css`).
- The app uses an in-memory `activities` dictionary as its persistence layer, so restarting the server resets data.

## Architecture and coding patterns
- Keep API logic in `src/app.py` unless a task explicitly requires otherwise.
- Preserve the existing FastAPI patterns: simple route handlers, explicit validation, and `HTTPException` for 4xx responses.
- Treat `activities` as the canonical data source. Activity names are dictionary keys and `participants` is the list of signed-up student emails.
- When changing signup or unregister behavior, validate the activity exists before mutating the data, reject duplicates, and return clear error messages in the existing JSON style.
- Keep the front-end and API aligned. If the API contract changes, update `src/static/app.js` and related UI elements accordingly.

## Local workflow
- Run the app from the repository root with: `python -m uvicorn src.app:app --reload`
- For local browser testing, use the FastAPI docs at `/docs` or the static UI at `/static/index.html`.
- Use `requirements.txt` for dependencies and keep additions minimal and relevant.

## Quality expectations
- Prefer small, targeted changes over broad refactors.
- Keep code readable and consistent with the existing simple Python/FastAPI style.
- Do not introduce a database, new framework, or persistent storage unless the task asks for it.
- Add or adjust validation for changed behavior, especially around missing activities, duplicate signups, and invalid registrations.

## Verification
- For Python-only changes, validate with: `python -m compileall src`
- For endpoint or UI changes, smoke-test the relevant route(s) with the running app and confirm the affected behavior works in the browser or with `curl`.
- Keep validation focused on the changed behavior rather than running broad suites.
