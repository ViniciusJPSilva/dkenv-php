# DKEnv PHP

A Docker-based PHP development environment for local development. DK stands for Docker Kit, or Donkey Kong, depending on who asks.

## Features

- PHP 8.3 FPM
- Nginx
- Composer included
- MySQL support
- Docker Compose configuration
- Cross-platform compatibility

## Requirements

- Docker with Compose support

## Installation

### 1. Clone the repository

```
git clone https://github.com/ViniciusJPSilva/dkenv-php.git
cd dkenv-php
```

### 2. Create environment configuration

```
cp .env.example .env
```

Edit `.env` as needed for your local setup.

### 3. Build containers

```
docker compose build
```

### 4. Start services

```
docker compose up -d
```

The application will be accessible at `http://localhost:8080`.

## Project Structure

```
dkenv-php/
├── docker-compose.yml
├── .env.example
├── README.md
├── nginx/
│   └── default.conf
└── php/
    └── Dockerfile
```

## Available Services

### PHP-FPM

PHP 8.3 FPM service for executing PHP applications.

- Port: 9000 (internal)
- Volume: Application code mounted at `/var/www/html`

### Nginx

Web server for handling HTTP requests and routing to PHP-FPM.

- Port: 8080 (configurable via `.env`)
- Configuration: `nginx/default.conf`
- Volume: Application code mounted at `/var/www/html`

### MySQL

MySQL 8 service configured for local development.

## Usage

### Accessing the PHP application

Place your PHP application files inside the directory configured in `DKENV_PROJECT_PATH` (default: `./src`).

### Running Composer

Install dependencies using Composer:

```
docker compose exec php composer install
```

Update dependencies:

```
docker compose exec php composer update
```

### Running PHP commands

Execute PHP commands in the container:

```
docker compose exec php php -v
```

### Viewing logs

View container logs:

```
docker compose logs -f php
docker compose logs -f nginx
```

### Accessing MySQL

Connect using the credentials defined in `.env`:

```
docker compose exec mysql mysql -u root -p
```

## Stopping Containers

Stop all running containers:

```
docker compose stop
```

Stop and remove containers:

```
docker compose down
```

To also remove volumes (database data, etc.):

```
docker compose down -v
```

## License

This project is licensed under the MIT License. See the LICENSE file for details.
