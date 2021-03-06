> ### CodeIgniter4 codebase containing real world examples api (CRUD, auth, advanced patterns, etc).


### [Demo](http://codeigniter4-realworld-api.herokuapp.com/)


This codebase was created to demonstrate a fully functional REST API built with **CodeIgniter4**, including CRUD operations, authentication, routing, pagination, and more.

Hope you'll find this example helpful. Pull requests are welcome!

----------

# Getting started

## Installation

Please check the official CodeIgniter4 installation guide for server requirements before you start. [Official Documentation](https://codeigniter4.github.io/userguide/installation/index.html)


Clone the repository

    git clone https://github.com/agungsugiarto/codeigniter4-realworld-api.git

Switch to the repo folder

    cd codeigniter4-realworld-api

Install all the dependencies using composer

    composer install

Copy the example env file and make the required configuration changes in the .env file

    cp .env.example .env

Run the database migrations (**Set the database connection in .env before migrating**)

    php spark migrate

Start the local development server

    php spark serve

You can now access the server at http://localhost:8080

**TL;DR command list**

    git https://github.com/agungsugiarto/codeigniter4-realworld-api.git
    cd codeigniter4-realworld-api
    composer install
    cp .env.example .env
    
**Make sure you set the correct database connection information before running the migrations** [Environment variables](#environment-variables)

    php spark migrate
    php spark serve

## Database seeding

**Populate the database with seed data with relationships which includes users, articles, comments, tags, favorites and follows. This can help you to quickly start testing the api or couple a frontend and start using it with ready content.**

Run the database seeder and you're done

    php spark db:seed DatabaseSeeder

***Note*** : It's recommended to have a clean database before seeding. You can refresh your migrations at any point to clean the database by running the following command

    php spark migrate:refresh

## API Specification

> [Full API Spec](https://documenter.getpostman.com/view/1062493/TVYKYvnz)

----------

# Code overview

## Dependencies

- [codeigniter4-cors](https://github.com/agungsugiarto/codeigniter4-cors) - For handling Cross-Origin Resource Sharing (CORS)
- [codeigniter4-repository](https://github.com/agungsugiarto/codeigniter4-repository) - For Implementation of repository pattern for CodeIgniter 4
- [league/fractal](https://github.com/thephpleague/fractal) - For provides a presentation and transformation layer for complex data output, the like found in RESTful APIs, and works really well with JSON
- [firebase/php-jwt](https://github.com/firebase/php-jwt) - For authentication using JSON Web Tokens

## Folders

- `app/Config` - Contains all the application configuration files
- `app/Controllers` - Contains all the api controllers
- `app/Criteria` - Contains all the criteria are a way to build up specific query conditions
- `app/Database/Migrations` - Contains all the database migrations
- `app/Database/Seeds` - Contains the database seeder
- `app/Entities` - Contains all the classes as a first-class citizen in it’s database layer
- `app/Filters` - Contains the JWT auth filter and throttler
- `app/Models` - Contains all the models
- `app/Repository` - Contains all the repository object
- `app/Scopes` - Contains all the repository define which fields can be used to scope your queries by setting $searchable property
- `app/Transformers` - Contains all transformer output JSON
- `routes` - Contains all the api routes defined in `api.php` file

## Environment variables

- `.env` - Environment variables can be set in this file

***Note*** : You can quickly set the database information and other variables in this file and have the application fully working.

----------

# Testing API

Run the CodeIgniter4 development server

    php spark serve

The api can now be accessed at

    http://localhost:8080/api

Request headers

| **Required** 	| **Key**              	| **Value**            	|
|----------	|------------------	|------------------	|
| Yes      	| Content-Type     	| application/json 	|
| Yes      	| X-Requested-With 	| XMLHttpRequest   	|
| Optional 	| Authorization    	| Token {JWT}      	|

Refer the [api specification](#api-specification) for more info.

----------
 
# Authentication
 
This applications uses JSON Web Token (JWT) to handle authentication. The token is passed with each request using the `Authorization` header with `Token` scheme. The JWT authentication filter handles the validation and authentication of the token. Please check the following sources to learn more about JWT.
 
- https://jwt.io/introduction/
- https://self-issued.info/docs/draft-ietf-oauth-json-web-token.html

----------

# Cross-Origin Resource Sharing (CORS)
 
This applications has CORS enabled by default on all API endpoints. The CORS allowed origins can be changed by setting them in the config file. Please check the following sources to learn more about CORS.
 
- https://developer.mozilla.org/en-US/docs/Web/HTTP/Access_control_CORS
- https://en.wikipedia.org/wiki/Cross-origin_resource_sharing
- https://www.w3.org/TR/cors