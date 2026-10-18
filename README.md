# Online Examination System (PHP & MySQL)

A web-based examination and quiz application built with **PHP, MySQL, HTML, CSS, JavaScript, Bootstrap, and jQuery**. Students can create an account, sign in, take multiple-choice quizzes, review their results and previous attempts, and compare scores on a ranking page. Administrators can manage quizzes and questions, view registered users, review feedback, and monitor rankings.

> **Project status:** This repository contains a legacy PHP application and a MySQL database dump. It is suitable for learning, local testing, and further development. It should **not be exposed to the public internet or used with real student data as-is**. Read the [Security Notes](#security-notes) before running it.

**Repository:** [hasanuzzamanpriyam/Examination_system_PHP](https://github.com/hasanuzzamanpriyam/Examination_system_PHP)

---

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Technology Stack](#technology-stack)
- [Project Structure](#project-structure)
- [Requirements](#requirements)
- [Installation and Setup](#installation-and-setup)
- [How to Use](#how-to-use)
- [Database Structure](#database-structure)
- [Configuration](#configuration)
- [Troubleshooting](#troubleshooting)
- [Security Notes](#security-notes)
- [Limitations and Future Improvements](#limitations-and-future-improvements)
- [Contributing](#contributing)
- [License](#license)

## Overview

The Online Examination System provides a simple interface for hosting multiple-choice quizzes online. Quiz records, questions, answer choices, correct answers, user accounts, feedback, scores, and attempt history are stored in a MySQL database.

The application includes two main areas:

- **Student area:** registration and login, quiz selection, question answering, result summaries, attempt history, and rankings.
- **Administrator area:** quiz creation and removal, question setup, user management, ranking review, and feedback management.

The supplied `project.sql` file includes both the database schema and sample records. Review the sample records before importing them into any database that contains real data.

## Features

### Student features

- Create an account using basic profile information.
- Sign in and sign out.
- View the available quizzes, including quiz title, number of questions, marks, and time limit.
- Answer multiple-choice questions.
- View a result summary with correct answers, incorrect answers, and score.
- Review previous examination attempts from the history page.
- View the ranking table, ordered by score.
- Submit feedback or report a problem through the feedback page.

### Administrator features

- Open the administrator dashboard.
- View the available quizzes.
- Create a quiz by setting its title, question count, marks for correct and incorrect answers, time limit, tag, and description.
- Add questions with four answer options and designate the correct answer through the quiz-management workflow.
- Remove quizzes.
- View registered users and remove a user account.
- View rankings.
- Read and remove submitted feedback.

### Interface features

- Bootstrap-based layout and navigation.
- Local CSS, JavaScript, font, and image assets.
- Separate pages for the public homepage, student account area, feedback, and administrator dashboard.

> Feature behavior reflects the current repository implementation. Some interface elements and security controls are legacy or incomplete and may need updates for a modern deployment.

## Technology Stack

| Technology | Purpose |
|---|---|
| PHP | Server-side application logic and session handling |
| MySQL / MariaDB | Stores accounts, quizzes, questions, answers, scores, rankings, and feedback |
| MySQLi | PHP-to-MySQL database connection and queries |
| HTML / CSS | Page structure and styling |
| JavaScript | Browser-side behavior |
| Bootstrap | Responsive UI components and layout |
| jQuery | Browser-side interaction used by the existing interface |

The SQL dump was generated in a **PHP 5.6 / MySQL 5.7-era environment**. Newer PHP or MySQL versions may require compatibility fixes; test the project locally before using it in a shared environment.

## Project Structure

```text
Examination_system_PHP/
├── css/                           # Stylesheets and Bootstrap styles
├── fonts/                         # Font assets
├── image/                         # Images used by the interface
├── js/                            # JavaScript libraries and scripts
├── account.php                    # Student account, quizzes, results, history, rankings
├── admin.php                      # Administrator login handler
├── dash.php                       # Administrator dashboard and management screens
├── dbConnection.php               # MySQL connection configuration
├── feed.php                       # Feedback form submission handler
├── feedback.php                   # Feedback / report-a-problem page
├── index.php                      # Public homepage and sign-in / registration entry point
├── login.php                      # Student login handler
├── logout.php                     # Sign-out handler
├── project.sql                    # Database schema and sample data
├── sign.php                       # Student registration handler
├── update.php                     # Quiz, question, result, and administration actions
├── Online_exam_project_report.doc # Project report document
└── Online_exam_project_report.rar # Compressed project report archive
```

The repository may contain additional editor or temporary files; those are not required to run the application.

## Requirements

- Apache or another PHP-capable web server.
- PHP with the **MySQLi** extension enabled.
- MySQL or MariaDB.
- A browser such as Chrome, Firefox, Edge, or Safari.
- Git, or a way to download the repository as a ZIP file.

For a beginner-friendly local environment, you can use [XAMPP](https://www.apachefriends.org/), which bundles Apache, PHP, and MariaDB/MySQL tools. Because this is a legacy application, select a compatible PHP version for local testing and do not assume that every current PHP release will run it without changes.

## Installation and Setup

### 1. Download the project

Clone the repository:

```bash
git clone https://github.com/hasanuzzamanpriyam/Examination_system_PHP.git
```

Alternatively, download the repository ZIP from GitHub and extract it.

### 2. Place the project in your web-server directory

For XAMPP on Windows, place the folder under:

```text
C:\xampp\htdocs\Examination_system_PHP
```

For other Apache or local PHP environments, place it in the corresponding document root.

### 3. Start Apache and MySQL

Open the XAMPP Control Panel (or your equivalent server control panel) and start **Apache** and **MySQL**.

### 4. Create the database

Open phpMyAdmin, usually at `http://localhost/phpmyadmin`, and create a database named:

```text
project
```

The provided SQL file creates tables but does not create the database itself, so create `project` before importing it.

### 5. Import the SQL file

1. Select the `project` database in phpMyAdmin.
2. Open the **Import** tab.
3. Choose the repository's `project.sql` file.
4. Start the import and confirm that the tables were created.

The dump contains sample accounts, quiz questions, scores, rankings, and feedback. Use a fresh local database and remove or replace sample records before using your own data.

You can also import the SQL file from the MySQL command line, provided the database has already been created:

```bash
mysql -u root -p project < project.sql
```

If your local MySQL root account has no password, omit `-p` or press Enter when prompted, depending on your MySQL setup.

### 6. Configure the database connection

Open `dbConnection.php`. The current repository uses a local MySQL connection with the database name `project` and the default `root` username with an empty password:

```php
$con = new mysqli('localhost', 'root', '', 'project');
```

Change the host, username, password, and database name to match your local environment. For example, if you created a dedicated database user, use that account instead of `root`.

Do not commit production database passwords or other secrets to source control.

### 7. Open the application

Visit this URL in your browser:

```text
http://localhost/Examination_system_PHP/index.php
```

If you extracted the project to a folder with a different name, adjust the URL to match that folder.

### 8. Test the application locally

- Register a new student account from the homepage.
- Sign in and open the quiz list.
- Start a quiz and submit answers.
- Review the result and history pages.
- Open the feedback page and submit a test message.
- Test administrator workflows only in a local environment, after reviewing the seeded records and the security notes below.

The SQL dump includes sample administrator records, but those credentials are insecure legacy sample data. Review the `admin` table and change or remove the sample accounts before using the project beyond local testing. Do not reuse any credentials from the sample database.

## How to Use

### Student workflow

1. Open the homepage.
2. Register an account or sign in with an existing student account.
3. Browse the available quizzes.
4. Choose **Start** for a quiz and answer the multiple-choice questions.
5. Submit answers and review the result summary.
6. Use **History** to view saved results and **Ranking** to compare scores.
7. Sign out when finished.

The current implementation checks a student's history when displaying quizzes and provides a restart action for quizzes that have already been attempted. Review and test this behavior carefully if you change scoring or attempt rules.

### Administrator workflow

1. Open the **Admin Login** option on the homepage.
2. Authenticate with a configured administrator account.
3. Use the dashboard navigation to view users, rankings, and feedback.
4. Open the quiz section to create a quiz and then enter its questions and answer options.
5. Use the quiz-management pages to remove a quiz when required.

Administrator authentication and permissions need security improvements before this workflow is used on a public server.

## Database Structure

The supplied `project.sql` file defines the following tables:

| Table | Purpose |
|---|---|
| `admin` | Administrator email and password records |
| `user` | Student profile and login records |
| `quiz` | Quiz metadata, scoring rules, time limit, tag, and description |
| `questions` | Questions belonging to a quiz |
| `options` | Multiple-choice options for each question |
| `answer` | Correct-answer option identifiers for questions |
| `history` | Per-user quiz attempts and result details |
| `rank` | Overall score values used by the ranking page |
| `feedback` | Feedback messages submitted through the feedback form |

The schema is from an older project and does not use modern database constraints consistently. If you extend it, consider adding primary keys, indexes, foreign keys, appropriate column types, and migration scripts. Back up the database before changing the schema.

## Configuration

### Database settings

The database connection is centralized in `dbConnection.php`, which is included by multiple PHP pages. Keep the connection details consistent with the database you created.

### Local development

For local development:

- Keep the application bound to your local machine while assessing it.
- Use test data instead of real student information.
- Enable PHP error reporting only in your local development environment.
- Check the PHP and MySQL error logs when a page fails.

For deployment, use environment-based configuration or a configuration file kept outside the public web root, and ensure secrets are not committed to Git.

## Troubleshooting

### `Could not connect to mysql` or a database connection error

- Confirm that MySQL/MariaDB is running.
- Confirm that the database is named `project`.
- Check the username and password in `dbConnection.php`.
- Verify that PHP's MySQLi extension is enabled.

### `Unknown database 'project'`

Create the `project` database in phpMyAdmin first, then import `project.sql` into it.

### Page not found / HTTP 404

- Make sure the project folder is inside the server's document root.
- Confirm that Apache is running.
- Check that the URL folder name matches the extracted directory.

### SQL import errors

- Import into an empty `project` database to avoid table-name conflicts.
- Check the MySQL/MariaDB error message for incompatible SQL syntax or character-set settings.
- Back up any existing data before dropping tables or recreating the database.

### Blank page or PHP errors

- Check the PHP and Apache error logs.
- Confirm that the installed PHP version supports the legacy application's code.
- Test with a compatible local PHP environment before attempting upgrades.

## Security Notes

**This codebase should be treated as a learning project, not a production-ready examination platform.** Before deploying it or processing real student data, review and fix at least the following issues in the existing implementation:

- **Legacy password hashing:** student passwords are processed with MD5, and administrator password handling is not equivalent to modern password hashing. Replace this with PHP's `password_hash()` and `password_verify()` and migrate existing accounts appropriately.
- **SQL injection risks:** several handlers build SQL queries by concatenating request values into SQL statements. Use prepared statements for all user-supplied values.
- **Hard-coded administrator marker:** authorization checks rely on a fixed value in the session logic. Replace this with a proper authenticated role/permission model and validate authorization server-side on every privileged action.
- **Unsafe HTML output:** user names, quiz content, and feedback are rendered in pages. Escape output appropriately to reduce cross-site scripting (XSS) risks.
- **State-changing links:** some administrative actions are triggered with URL parameters. Use POST requests, CSRF tokens, and confirmation checks for state-changing operations.
- **Database privileges:** the current connection example uses the MySQL `root` account with an empty password. Create a restricted database user with only the permissions the application needs.
- **Sample data and credentials:** `project.sql` contains legacy sample records, including administrator and student records. Remove or replace them and never rely on sample credentials.
- **Session security and validation:** add secure session-cookie settings, regenerate session IDs after login, validate inputs on the server, and enforce access controls consistently.
- **Transport security:** use HTTPS when deployed and avoid exposing error details or database diagnostics to visitors.
- **Dependencies:** the repository includes older front-end assets. Review and update dependencies where appropriate, testing the interface after each upgrade.

Do not deploy this project publicly until these risks have been addressed and the application has been tested.

## Limitations and Future Improvements

Potential improvements for a maintained version include:

- Refactor database access into reusable functions or a small application architecture.
- Replace concatenated SQL with prepared statements throughout the codebase.
- Use secure password hashing and a clear student/administrator role system.
- Add CSRF protection, server-side validation, safer output encoding, and structured error handling.
- Improve quiz timing and server-side enforcement of exam duration.
- Add pagination and filtering for users, quizzes, attempts, and feedback.
- Add automated tests for registration, login, quiz submission, scoring, and administrator permissions.
- Modernize the UI and update the front-end dependencies.
- Add a documented configuration template and database migration process.
- Add screenshots or a demo link to this README when they become available.

## Contributing

Contributions and improvements are welcome.

1. Fork the repository.
2. Create a feature branch:

   ```bash
   git checkout -b feature/your-feature-name
   ```

3. Make your changes and test them locally.
4. Commit your changes with a clear message.
5. Push the branch and open a pull request describing the change and any testing performed.

For security-sensitive issues, avoid publishing exploitable details in a public issue; contact the repository maintainer through an appropriate private channel.

## License

No `LICENSE` file is currently included in the repository. Until a license is added, do not assume that the project is licensed for unrestricted reuse or redistribution. Confirm the original project's licensing terms and add an appropriate license file if you intend to distribute or maintain this code publicly.

---

**Maintainer / Repository Owner:** [hasanuzzamanpriyam](https://github.com/hasanuzzamanpriyam)
