# Kflix (Laravel)

> A modern streaming discovery platform powered by the TMDB API, refactored from plain PHP into a Laravel 11 application.

**Original Project:** [CrochsDevs/Kflix---with-TMDB-Api](https://github.com/CrochsDevs/Kflix---with-TMDB-Api)

This is a fork of the original Kflix project, rebuilt and improved with a Laravel 11 architecture, Docker deployment, and a complete UI redesign.

---

## What We Improved

### 1. Architecture: Plain PHP to Laravel 11
- Refactored the entire codebase from raw PHP into a proper **Laravel 11** application
- Replaced scattered require/include calls with **MVC pattern** (Controllers, Blade views, Models)
- Converted all 8 pages from mixed HTML+PHP templates into clean **Blade components**
- Proper routing for all pages including API endpoints

### 2. Containerized Deployment (Docker)
- **Multi-stage Dockerfile** using composer:2 for dependency resolution and PHP 8.2 Apache for runtime
- **Docker Compose** with web + MySQL services (port mapping 8181:80)
- Bind mount for live code reload during development
- Fixed common Docker pitfalls (brace expansion, DNS resolution, bootstrap/cache permissions)

### 3. Complete UI Redesign
- **Mobile-first responsive** layout with bottom navigation bar
- Cohesive design system across all pages (movies, TV, player, watchlist, detail views)
- Fixed mobile panel alignment and unified CSS styling
- Redesigned the new-popular page layout to match the rest of the app

### 4. Watchlist / MyList Functionality
- Added full **watchlist** feature with Eloquent-style DB queries via the Watchlist model
- Integrated watchlist into the new-popular page
- Dedicated /watchlist page and /api/watchlist REST API endpoint
- Watchlist table auto-initialized via init.sql

### 5. Search and Filter Enhancements
- **TVController** now supports search and filter on the new-popular page
- Genre names properly displayed with filter functionality
- Heart toggle for adding/removing favorites works across all pages
- Fullscreen hotkey (F) now ignores input fields to avoid triggering while typing in search

### 6. Bug Fixes and Stability
- Fixed getenv() calls in database config (must be in constructor, not property declarations)
- Fixed public/index.php invalid new keyword before require
- Fixed bootstrap/app.php path resolution (dirname resolving to /var/www/html)
- Fixed APP_KEY generation in Docker (proper base64 key)
- Removed empty script tags
- CSRF verification properly configured: API routes excluded from CSRF middleware

### 7. Legacy PHP Compatibility
- Added .htaccess rewrite rules and Apache AllowOverride All config
- Legacy PHP file redirects mapped to Laravel routes for backward compatibility

---

## Tech Stack

- **Framework:** Laravel 11
- **PHP:** 8.2
- **Database:** MySQL
- **API:** TMDB (The Movie Database)
- **Server:** Apache 2.4 (Docker)
- **Frontend:** Blade templates, vanilla JS, custom CSS

---

## Quick Start with Docker

Clone the repo, configure .env with your TMDB API key and DB credentials, then run:

    docker compose up --build -d

App runs at http://localhost:8181

---

## Project Structure

    Kflix/
    +-- app/             Controllers, Services (TmdbService), Models (Watchlist)
    +-- config/          Laravel configuration
    +-- database/        Migrations, seeders
    +-- public/          Entry point, assets
    +-- resources/views/ Blade templates
    +-- routes/          Web and API routes
    +-- storage/         Logs, cache, compiled views
    +-- bootstrap/       App bootstrap
    +-- Dockerfile       Multi-stage build
    +-- docker-compose   Web + MySQL services
    +-- init.sql         Watchlist table schema
    +-- .env.example     Environment template

---

## License

See the original project for licensing details.
