# Online Test Platform (No Student Login)

A complete bilingual Hindi/English online examination platform built with Node.js, Express and SQLite.

## Features
- Students start published tests without login/signup.
- Hindi/English interface.
- Instructions, countdown timer, question navigation, answer changes and auto-submit.
- Server-side scoring with positive and negative marking.
- Result summary and optional answer explanations.
- Persistent SQLite database for tests, questions and results.
- Admin login protected by a server-side environment password.
- Admin CRUD for tests/questions, publish/unpublish, timing changes, preview via student site, and CSV result export.

## Run locally
1. Install Node.js 20+.
2. Copy `.env.example` to `.env`.
3. Set strong values for `SESSION_SECRET` and `ADMIN_PASSWORD`.
4. Run `npm install`.
5. Run `npm start`.
6. Open `http://localhost:3000` for students and `http://localhost:3000/admin` for the admin panel.

## Deployment
Use a Node.js host that supports persistent disk/storage because the app stores SQLite and session data in `db/`.

Set these environment variables on the host:
- `NODE_ENV=production`
- `SESSION_SECRET=<long random secret>`
- `ADMIN_PASSWORD=<strong admin password>`
- `PORT` is normally supplied by the host.

Start command: `npm start`

**Important:** do not use an ephemeral filesystem for production. If the host's filesystem resets on redeploy, your SQLite database will be lost. Attach persistent storage or switch the database layer to PostgreSQL before using it for important exam records.

## Admin workflow
1. Open `/admin`.
2. Enter the server-side `ADMIN_PASSWORD`.
3. Click **New Test**.
4. Enter test name, subject, duration and instructions in Hindi/English.
5. Save the test.
6. Add questions, four options, correct answer, marks, negative marks and explanations.
7. Save each question.
8. Publish the test when ready.
9. Students will see published tests on `/`.
10. Use **Results** and **Export Results CSV** in the admin panel to review/download submissions.

## Security notes
- Student accounts are intentionally not used.
- The admin password is read from an environment variable and is never sent to the browser.
- Admin APIs require a server-side session.
- Submitted attempts are rejected if already submitted.
- Scoring is performed on the server, not trusted from the browser.
- For a high-stakes/public deployment, put the site behind HTTPS and consider adding rate limiting, CSRF protection, stronger admin authentication/2FA, backups, and PostgreSQL.
