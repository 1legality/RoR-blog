# README
This is just the ruby on rails tutorial joined to Docker for rapid development.

# Steps
## build the projet

``` bash
docker-compose run web rails new . --force --no-deps --database=postgresql
```

Give current user ownership of created files/folders
```bash
sudo chown -R $USER:$USER .
```

## Connect the Database

Replace the content in config/database.yml

``` yml
default: &default
  adapter: postgresql
  encoding: unicode
  host: db
  username: postgres
  password:
  pool: 5

development:
  <<: *default
  database: myapp_development


test:
  <<: *default
  database: myapp_test

```

You can now boot the app with docker-compose up:

``` bash
docker-compose up
```
If all’s well, you should see some PostgreSQL output.

``` bash
rails_db_1 is up-to-date
Creating rails_web_1 ... done
Attaching to rails_db_1, rails_web_1
db_1   | PostgreSQL init process complete; ready for start up.
db_1   |
db_1   | 2018-03-21 20:18:37.437 UTC [1] LOG:  listening on IPv4 address "0.0.0.0", port 5432
db_1   | 2018-03-21 20:18:37.437 UTC [1] LOG:  listening on IPv6 address "::", port 5432
db_1   | 2018-03-21 20:18:37.443 UTC [1] LOG:  listening on Unix socket "/var/run/postgresql/.s.PGSQL.5432"
db_1   | 2018-03-21 20:18:37.726 UTC [55] LOG:  database system was shut down at 2018-03-21 20:18:37 UTC
db_1   | 2018-03-21 20:18:37.772 UTC [1] LOG:  database system is ready to accept connections
```

Finally, you need to create the database. In another terminal, run:
``` bash
docker-compose run web rake db:create
```
Here is an example of the output from that command:
``` bash
$ docker-compose run web rake db:create
Starting rails_db_1 ... done
Created database 'myapp_development'
Created database 'myapp_test'
```

go to http://localhost:3000 on a web browser to see the Rails Welcome.

## Enter the docker terminal
- Use `docker ps` to get the name of the existing container.
- Use the command `docker exec -it <container id> /bin/bash` to get a bash shell in the container.
