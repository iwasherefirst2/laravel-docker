# About

This repository contains everything you need to get started to run a 
Laravel 5 / 6 / 7 application with Docker in 3 minutes. It is made for legacy projects that cannot be upgraded to Laravel 8 in near future but would like to use docker.

This package is not needed for Laravel 8 and upwards, as Laravel versions from 8 upwards ships with a wrapper for docker, called [Laravel Sail](https://laravel.com/docs/sail).

## Table of Contents

- [Setup](#setup)
    - [1. Copy files](#step-1-copy-files-in-your-directory)
    - [2. Execute Docker](#step-2-execute-docker)
    - [3. Run Composer](#step-3-install-composer-dependencies)
- [Enhancements](#enhancements)

# Setup

Its required that one has [docker-compose](https://docs.docker.com/compose/install/) on the machine installed.

## Step 1: Copy files in your directory

We assume that you add this to an existing project, as since Laravel 8 docker ships in by default.

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


## Step 3: Install Composer dependencies

Bash into your container:

  ```sh
  docker-compose exec app bash
  ```

Install composer dependencies (this may also take a moment):

  ```sh
  composer install
  ```

and finally generate a key

  ```sh
  php artisan key:generate
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






