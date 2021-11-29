# Greenlight API

Greenlight is an api, i implemented by following the book [Let's Go Further](https://lets-go-further.alexedwards.net/) by Alex Edwards

If you like what you see please consider buying the book, it was my first hands on book and i absolutely loved it and i recommend it strongly.

## Requeriments

If you are in Mac OS environment you can use brew to install the tools:

- [Go 1.17](https://go.dev/), language (brew install go@1.17)
- [migrate](https://github.com/golang-migrate/migrate), for database migrations (brew install golang-migrate)
- [PostgreSQL](https://www.postgresql.org/), database (brew install postgresql)
- [curl](https://curl.se/), just to make a http request as an example

## Get Started

1. Make sure you have the requeriments working correctly

2. Clone the repo

```bash
git clone https://github.com/ricardonunosr/greenlight.git
```

3. Create Database,User and install extension to database

```bash
psql postgres
CREATE DATABASE greenlight;
\c greenlight
CREATE ROLE greenlight WITH LOGIN PASSWORD 'pa55word';
CREATE EXTENSION IF NOT EXISTS citext;
```

4. Add this to your .zshrc or bashrc and then source it

```bash
export GREENLIGHT_DB_DSN='postgres://greenlight:pa55word@localhost/greenlight?sslmode=disable'
```

```bash
source ~/.zshrc
```

5. Executing the migrations

```bash
migrate -path=./migrations -database=$GREENLIGHT_DB_DSN up
```

6. Run the api

```bash
go run ./cmd/api
```

7. Make a POST,GET and DELETE requests to check if its working correctly

```bash
BODY='{"title":"Black Panther","year":2018,"runtime":"134 mins","genres":["sci-fi","action","adventure"]}'
```

```bash
curl -i -d "$BODY" localhost:4000/v1/movies
curl -i localhost:4000/v1/movies/1
curl -X DELETE localhost:4000/v1/movies/1
```
