# eLearning Platform

A Learning Management System (LMS) web platform built for publishing and taking online courses, interactive test-based assessment, and collaboration through forums.

This project showcases a modern full-stack setup (Laravel + Vue), a clear business model (roles, courses, progress, assessment), and an architecture that can be extended into real edtech products.

## What the project does

- course management (create, edit, publish)
- lessons linked to courses, including video support
- tests and exercises with multiple question types:
  - multiple choice (single / multiple answers)
  - ordering
  - fill in the blanks
  - numeric
- user progress and score tracking
- enroll/unenroll in courses
- forums and topics for discussion
- role system (admin / teacher / user) and role requests
- additional problems/exercises section

## Technologies used

### Backend
- **PHP 8.1+ / 8.2 (Docker)**
- **Laravel 10**
- **Eloquent ORM**
- **Laravel Sanctum** (protected API endpoint for users)
- **MySQL**

### Frontend
- **Vue 3**
- **Vuex 4** (state management)
- **Bootstrap**
- **Sass**
- **Axios / Fetch API**

### Tooling & DevOps
- **Laravel Mix / Webpack** for asset builds
- **Docker + Docker Compose** (app, nginx, mysql, phpMyAdmin)
- **PHPUnit** for testing
- **Prettier** and **PHP CS Fixer** for formatting

## Architecture (high-level)

The application follows Laravel's **MVC** model, with a hybrid frontend:
- **Blade templates** for layout and server-rendered pages
- **Vue components** mounted in the app for interactive UI

General flow:
1. Routes in `routes/web.php` send requests to controllers
2. Controllers manage business logic and model relationships
3. Eloquent models map database entities
4. Blade + Vue display data and handle client-side interactions

### Main modules
- `CourseController`, `LessonController`, `TestController`, `ExerciseController`
- `ForumController`, `ForumTopicController`, `ForumPostController`
- `RoleRequestController`, `UserController`, `ProblemController`

### Key entities
- `User`, `Role`, `RoleRequest`
- `Course`, `Lesson`, `Test`, `Exercise`
- `Forum`, `ForumTopic`, `ForumPost`
- `UserActivity`, `Category`, `CourseMetaTag`, `Problem`

## Project structure

```text
app/
  Http/Controllers/    # HTTP and module business logic
  Models/              # Eloquent models and relationships
resources/
  js/                  # Vue components + Vuex store
  views/               # Blade pages
routes/
  web.php              # main application routes
  api.php              # API routes
config/                # Laravel configuration
database/
  migrations/          # database schema
  seeders/             # seeders
```

## Installation and running

### Docker setup (recommended)

```bash
git clone <repo-url>
cd eLearning
cp .env.example .env
docker compose up -d --build
```

Then, in the PHP container:

```bash
composer install
php artisan key:generate
php artisan migrate
php artisan storage:link
```

### Local setup

Prerequisites:
- PHP 8.1+
- Composer
- Node.js + npm
- MySQL

```bash
cp .env.example .env
composer install
npm install
php artisan key:generate
php artisan migrate
php artisan storage:link
npm run dev
php artisan serve
```

## Useful commands

```bash
# frontend build (dev)
npm run dev

# frontend build (production)
npm run build

# run tests
php artisan test

# format JS/Vue/CSS/Blade
npm run prettier

# format PHP
npm run php-format
# or
composer format
```

## Roles and usage scenarios

- **Learner**: enrolls in courses, completes lessons, takes tests, tracks progress
- **Teacher**: creates courses, lessons, and assessments; manages educational content
- **Admin**: approves role requests and oversees the platform

## Deployment note

The `docker-compose.yml` file is oriented toward local development. For production:
- move credentials to secure environment variables
- set strong, separate passwords
- configure HTTPS, backups, and monitoring

## Project status

A functional demo/portfolio project, suitable for:
- technical showcase for recruiting
- extension with advanced features (gamification, analytics, microservices)
- an MVP base in the EdTech space

## License

This repository uses the MIT license (as in the Laravel project).
