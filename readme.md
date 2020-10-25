# About

This repo contains everything you need to get started to run a 
Laravel application with Docker in 3 minutes.

Its required that one has [docker-compose](https://docs.docker.com/compose/install/) installed.

# Setup

## Step 1: Copy files in your directory

### New project

1. Download a new Laravel version from https://github.com/laravel/laravel/ by selecting the required branch or use the [laravel installer](https://laravel.com/docs/8.x#via-laravel-installer) to get the latest version.

2. Copy the files from this repository in the same folder as your Laravel project folder.

### Existing project

Copy all files except `.env` and `readme.md` in your current project folder. Overwrite the credentions from your `.env` locally with those provided here. If you dont want to overwrite database name and user, then please adjust the file in `docker-compose/mysql/init/01-databaes.sql` according to your needs.

## Step 2: Execute docker

Run container

  ```sh
  docker-compose up -d --build
  ```

this may take a moment. After the container has been setup, check the status with

  ```sh
  docker-compose ps
  ```

you should see three containers are running.


## Step 3: Install dependencies

Bash into your container:

  ```sh
  docker-compose exec app bash
  ```

Install composer dependencies (this may also take a moment):

  ```sh
  docker-compose composer install
  ```

and finally generate a key

  ```sh
  docker-compose php artisan key:generate
  ```

:tada: Congratulations. Your app should now be accessible under `localhost:8005`

# Enhancements

I like to use the following aliases to avoid going into the container every time:

  ```
  alias phpunit="docker-compose exec app vendor/bin/phpunit"
  alias artisan="docker-compose exec app php artisan"
  alias composer="docker-compose exec app composer"
  ```

Also, if you want to keep you laravel docker container
running after a restart of your computer, you may add

  ```
  restart: unless-stopped
  ```

to each of your services (app,db,nginx).






