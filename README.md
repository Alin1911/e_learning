# eLearning Platform

O platformă web de tip Learning Management System (LMS), construită pentru publicarea și parcurgerea cursurilor online, evaluare prin teste interactive și colaborare prin forum.

Acest proiect evidențiază un stack full‑stack modern (Laravel + Vue), un model clar de business (roluri, cursuri, progres, evaluare) și o arhitectură care poate fi extinsă pentru produse edtech reale.

## Ce face proiectul

- gestionare cursuri (creare, editare, publicare)
- lecții asociate cursurilor, inclusiv suport pentru video
- teste și exerciții cu mai multe tipuri de întrebări:
  - multiple choice (single / multiple answers)
  - ordering
  - fill in the blanks
  - numeric
- urmărirea progresului utilizatorilor și punctaj
- înscriere/renunțare la cursuri
- forumuri și topicuri pentru discuții
- sistem de roluri (admin / teacher / user) și cereri de rol
- secțiune de probleme/exerciții suplimentare

## Tehnologii folosite

### Backend
- **PHP 8.1+ / 8.2 (Docker)**
- **Laravel 10**
- **Eloquent ORM**
- **Laravel Sanctum** (endpoint API protejat pentru user)
- **MySQL**

### Frontend
- **Vue 3**
- **Vuex 4** (state management)
- **Bootstrap**
- **Sass**
- **Axios / Fetch API**

### Tooling & DevOps
- **Laravel Mix / Webpack** pentru build assets
- **Docker + Docker Compose** (app, nginx, mysql, phpMyAdmin)
- **PHPUnit** pentru testare
- **Prettier** și **PHP CS Fixer** pentru formatare

## Arhitectură (high-level)

Aplicația urmează modelul **MVC** din Laravel, cu frontend hibrid:
- **Blade templates** pentru layout și pagini server-rendered
- **Vue components** montate în aplicație pentru UI interactiv

Flux general:
1. Route-urile din `routes/web.php` trimit requesturile către controllere
2. Controllerele gestionează logica de business și relațiile dintre modele
3. Modelele Eloquent mapează entitățile din baza de date
4. Blade + Vue afișează datele și gestionează interacțiunile clientului

### Module principale
- `CourseController`, `LessonController`, `TestController`, `ExerciseController`
- `ForumController`, `ForumTopicController`, `ForumPostController`
- `RoleRequestController`, `UserController`, `ProblemController`

### Entități cheie
- `User`, `Role`, `RoleRequest`
- `Course`, `Lesson`, `Test`, `Exercise`
- `Forum`, `ForumTopic`, `ForumPost`
- `UserActivity`, `Category`, `CourseMetaTag`, `Problem`

## Structură proiect

```text
app/
  Http/Controllers/    # logica HTTP și business pe module
  Models/              # modele Eloquent și relații
resources/
  js/                  # componente Vue + store Vuex
  views/               # pagini Blade
routes/
  web.php              # rute principale ale aplicației
  api.php              # rute API
config/                # configurări Laravel
database/
  migrations/          # schema bazei de date
  seeders/             # seeders
```

## Instalare și rulare

### Varianta Docker (recomandat)

```bash
git clone <repo-url>
cd eLearning
cp .env.example .env
docker compose up -d --build
```

Apoi, în containerul PHP:

```bash
composer install
php artisan key:generate
php artisan migrate
php artisan storage:link
```

### Varianta locală

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

## Comenzi utile

```bash
# frontend build (dev)
npm run dev

# frontend build (production)
npm run build

# rulare teste
php artisan test

# formatare JS/Vue/CSS/Blade
npm run prettier

# formatare PHP
npm run php-format
# sau
composer format
```

## Roluri și scenarii de utilizare

- **Learner**: se înscrie la cursuri, parcurge lecții, susține teste, urmărește progresul
- **Teacher**: creează cursuri, lecții și evaluări, gestionează conținut educațional
- **Admin**: aprobă cereri de rol și supervizează platforma

## Notă pentru deployment

Fișierul `docker-compose.yml` este orientat spre dezvoltare locală. Pentru producție:
- mută credențialele în variabile de mediu sigure
- setează parole puternice și separate
- configurează HTTPS, backup și monitorizare

## Status proiect

Proiect funcțional pentru demo/portofoliu, potrivit pentru:
- prezentare tehnică la recrutare
- extindere cu funcționalități avansate (gamification, analytics, microservices)
- bază pentru MVP în zona EdTech

## Licență

Acest repository folosește licența MIT (conform proiectului Laravel).
