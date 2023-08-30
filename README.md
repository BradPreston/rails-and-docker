# Docker and Rails

This repo is the base repo to build Ruby on Rails apps using Docker, Ruby, and PostgreSQL.

  

#### Versions:

- Ruby 3.2.x

- Rails 7.x.x

  

## Next Steps

Use [docker compose run](https://docs.docker.com/engine/reference/commandline/compose_run/) to generate a skeleton Rails app

```

docker compose run --no-deps web rails new . --force --database=postgresql

```

  

Since the last command updated the Gemfile, the image will need to be rebuilt. The build command should only be necessary when the Gemfile or Dockerfile are updated.

```

docker compose build

```

Next, you'll need to setup the config to connect to the database. Replace the contents in `config/database.yml` with this

```

default: &default

adapter: postgresql

encoding: unicode

host: db

username: postgres

password: password

pool: 5

  

development:

<<: *default

database: [DEV DATABASE NAME]

  
  

test:

<<: *default

database: [TEST DATABASE NAME]

```

Replace [DEV DATABASE NAME] and [TEST DATABASE NAME] with the appropriate name your project requires for each database.
  

Now you can boot up the app 
```
docker compose up -d
```

Finally, you will create the database
```
docker compose run web rake db:create
```

---

  

To stop the project, run `docker compose down`. To restart the application, run `docker compose up -d`.

  

### Notes

This project is built from [awesome-compose](https://github.com/docker/awesome-compose/tree/master/official-documentation-samples/rails/) docker/rails config.