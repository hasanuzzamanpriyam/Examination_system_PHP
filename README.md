# Online Examination System in PHP & MySQL

A web-based **Online Examination & Quiz Management System** built with Core PHP, MySQL, Bootstrap 3, and jQuery. This platform allows educational institutions and instructors to create, manage, and evaluate multiple-choice examinations online while providing students with an intuitive interface to take tests, view instant results, track their history, and compete on a global leaderboard.

---

## Features

### Student / User Portal
* **User Registration & Authentication:** Students can sign up with their name, gender, college/institution, email, and mobile number, and log in securely (`sign.php`, `login.php`).
* **Available Quizzes Dashboard:** Displays all active quizzes along with the total number of questions, maximum marks, time limit, and topic tags (`account.php?q=1`).
* **Interactive Examination Interface:** Clean multiple-choice question (MCQ) interface for attempting quizzes step-by-step.
* **Instant Automated Grading:** Immediately evaluates answers upon submission, calculating positive marks for correct answers and deducting negative marks for incorrect ones:
  $$\text{Total Score} = (\text{Right Answers} \times \text{Marks per Right Answer}) - (\text{Wrong Answers} \times \text{Negative Marks})$$
* **Exam History:** Allows students to review all previously attempted quizzes, including questions solved, right/wrong counts, and final scores (`account.php?q=2`).
* **Global Ranking / Leaderboard:** Dynamically ranks students across the platform based on their cumulative scores across quizzes (`account.php?q=3`).
* **Feedback System:** Enables users to submit feedback, bug reports, or suggestions directly to the system administrator (`feedback.php`, `feed.php`).

### Administrator Portal
* **Dedicated Admin Dashboard:** Protected login modal and management panel (`admin.php`, `dash.php`).
* **User Management:** View a complete list of registered students (Name, Gender, College, Email, Mobile) and delete accounts when necessary (`dash.php?q=1`).
* **Leaderboard Monitoring:** View global student rankings and cumulative scores (`dash.php?q=2`).
* **Feedback Inbox:** Read and manage user-submitted feedback messages along with submission dates and timestamps (`dash.php?q=3`).
* **Multi-Step Quiz Creation:**
  * **Step 1:** Define quiz metadata including Quiz Title, Total Questions, Marks for Right Answer, Negative Marks for Wrong Answer, Time Limit (in minutes), `#tag` for searching, and a description (`dash.php?q=4`).
  * **Step 2:** Input each question, provide four multiple-choice options ($a, b, c, d$), and select the correct answer key (`dash.php?q=4&step=2`).
* **Quiz Removal:** Easily delete outdated quizzes and their associated questions/scores from the system (`dash.php?q=5`).

---

## Technology Stack

* **Backend:** PHP (Core PHP 5.x / 7.x / 8.x with `mysqli` extension)
* **Database:** MySQL / MariaDB
* **Frontend:** HTML5, CSS3, JavaScript
* **Frameworks & Libraries:**
  * Bootstrap 3.3 (`bootstrap.min.css`, `bootstrap-theme.min.css`, `bootstrap.min.js`)
  * jQuery (`jquery.js`)
  * Modernizr (`modernizr.js`)
* **Typography & Icons:** Custom TrueType fonts (`gothic.ttf`, `typo.ttf`) and Bootstrap Glyphicons

---

## Project Directory Structure

```text
Examination_system_PHP/
├── css/
│   ├── bootstrap-theme.min.css          # Bootstrap 3 theme stylesheet
│   ├── bootstrap.min.css                # Core Bootstrap 3 stylesheet
│   ├── emty.txt                         # Placeholder file
│   ├── font.css                         # Custom font-face definitions
│   └── main.css                         # Custom application styling & layout rules
├── fonts/
│   ├── emty.txt                         # Placeholder file
│   ├── glyphicons-halflings-regular.*   # Bootstrap Glyphicons font files (eot, svg, ttf, woff, woff2)
│   ├── gothic.ttf                       # Custom Gothic font
│   └── typo.ttf                         # Custom Typography font
├── image/
│   ├── CAM00121.jpg                     # Developer / profile image asset
│   ├── bg.jpg                           # Main landing page background image
│   ├── bg1.jpg                          # Secondary background image
│   ├── cd-icon-menu.svg                 # Navigation menu SVG icon
│   └── emty.md                          # Placeholder file
├── js/
│   ├── bootstrap.js                     # Unminified Bootstrap JavaScript
│   ├── bootstrap.min.js                 # Minified Bootstrap JavaScript
│   ├── emty.txt                         # Placeholder file
│   ├── jquery.js                        # jQuery library
│   ├── main.js                          # Custom client-side scripts
│   └── modernizr.js                     # Feature detection library
├── Online_exam_project_report.doc       # Detailed academic project report (MS Word)
├── Online_exam_project_report.rar       # Compressed archive of the project report
├── account.php                          # Student dashboard (take quiz, view history & rankings)
├── admin.php                            # Administrator login authentication handler
├── dash.php                             # Administrator dashboard (manage users, quizzes, feedback)
├── dbConnection.php                     # MySQL database connection configuration
├── feed.php                             # Backend processor for user feedback submissions
├── feedback.php                         # Public/User feedback form page
├── index.php                            # Main landing page (User Sign-up, User Login, Admin Login)
├── login.php                            # Student login authentication handler
├── logout.php                           # Session termination and redirect script
├── project.sql                          # MySQL database dump (schema + initial seed data)
├── sign.php                             # Student registration processor
└── update.php                           # Core controller for quiz evaluation, creation & deletion
```

---

## Database Schema (`project.sql`)

The database (`project`) consists of **9 relational tables**:

| Table Name | Description | Key Columns |
| :--- | :--- | :--- |
| `admin` | Stores administrator login credentials. | `admin_id`, `email`, `password` |
| `user` | Stores registered student profiles and MD5-hashed passwords. | `name`, `gender`, `college`, `email` (PK), `mob`, `password` |
| `quiz` | Stores metadata and scoring rules for each examination. | `eid`, `title`, `sahi` (right marks), `wrong`, `total`, `time`, `intro`, `tag`, `date` |
| `questions` | Stores individual questions linked to a specific quiz (`eid`). | `eid`, `qid`, `qns`, `choice`, `sn` |
| `options` | Stores the 4 multiple-choice options for each question (`qid`). | `qid`, `option`, `optionid` |
| `answer` | Maps each question (`qid`) to its correct option ID (`ansid`). | `qid`, `ansid` |
| `history` | Tracks each user's quiz attempts, scores, and right/wrong counts. | `email`, `eid`, `score`, `level`, `sahi`, `wrong`, `date` |
| `rank` | Maintains the cumulative leaderboard score for each student. | `email`, `score`, `time` |
| `feedback` | Stores messages submitted via the feedback form. | `id`, `name`, `email`, `subject`, `feedback`, `date`, `time` |

---

## Installation & Local Setup Guide

### Prerequisites
* A local web server environment such as **XAMPP**, **WAMP**, **MAMP**, or **LAMP**.
* **PHP** (7.0+ recommended) with the `mysqli` extension enabled.
* **MySQL** or **MariaDB** database server and **phpMyAdmin**.

### Step-by-Step Setup

1. **Clone or Extract the Project**
   * Copy the project folder into your web server's root directory:
     * **XAMPP:** `C:/xampp/htdocs/online-exam/`
     * **WAMP:** `C:/wamp64/www/online-exam/`
     * **LAMP (Linux):** `/var/www/html/online-exam/`

2. **Start Server Services**
   * Open your XAMPP/WAMP Control Panel and start **Apache** and **MySQL**.

3. **Create and Import the Database**
   * Open your browser and navigate to `http://localhost/phpmyadmin/`.
   * Click on **New** in the left sidebar and create a database named:
     ```sql
     project
     ```
   * Select the newly created `project` database, click the **Import** tab at the top, choose the `project.sql` file from the project root directory, and click **Go**.

4. **Configure Database Connection**
   * Open `dbConnection.php` in a code editor and verify that the credentials match your local MySQL setup:
     ```php
     <?php
     // Default configuration in dbConnection.php
     $con = new mysqli('localhost', 'root', '', 'project') or die("Could not connect to mysql" . mysqli_error($con));
     ?>
     ```

5. **Run the Application**
   * Open your web browser and visit:
     ```text
     http://localhost/online-exam/
     ```

---

## Default Login Credentials

### Administrator Access
To access the Admin Dashboard, click **Admin Login** in the bottom/footer bar of `index.php` and use either of the pre-configured accounts from `project.sql`:

* **Account 1:**
  * **Email:** `sunnygkp10@gmail.com`
  * **Password:** `123456`
* **Account 2:**
  * **Email:** `admin@admin.com`
  * **Password:** `admin`

### Student Access
* You can register a new student account directly from the sign-up form on the home page (`index.php`), or log in using one of the sample accounts included in `project.sql`.

---

## Security & Modernization Recommendations

If you plan to deploy this project in a production environment, consider implementing the following upgrades:
1. **Password Hashing:** Replace legacy `md5()` password hashing in `sign.php` and `login.php` with PHP's modern `password_hash()` and `password_verify()` functions.
2. **Prepared Statements:** Refactor raw SQL queries in `login.php`, `admin.php`, `sign.php`, and `update.php` to use parameterized `mysqli` prepared statements or `PDO` to prevent SQL Injection.
3. **Input Sanitization:** Sanitize user-generated fields (such as student names, quiz titles, and feedback entries) with `htmlspecialchars()` to protect against Cross-Site Scripting (XSS).
4. **Enforced Server-Side Timer:** Add a countdown timer on `account.php` backed by server-side timestamp validation in `update.php` to auto-submit quizzes when the allotted time expires.

---

## Documentation

A complete academic project report is included in the repository:
* `Online_exam_project_report.doc` (and its compressed backup `Online_exam_project_report.rar`) containing system analysis, ER diagrams, data flow diagrams (DFDs), and testing documentation.
