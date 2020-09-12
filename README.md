# Postgres Docker Container

This is a simple postgres database setup on a docker container.

## Setup
1. Install Docker<br>
`$ brew update`<br>
`$ brew install docker`
2. Install PostgresSQL<br>
`$ brew install postgresql`
3. Build the docker container<br>
`$ make build`
4. Run the docker container<br>
`$ docker run --rm -P --name pg_test eg_postgresql`
- `--rm`: removes the container once the process finishes or when shut down
- `-P`: exposes the ports
5. Find the exposed port for the docker container and run postgres onto it<br>
`$ docker ps`<br>

<pre><code>CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS                     NAMES
51909bf79497        eg_postgresql       "/usr/lib/postgresql…"   About a minute ago   Up About a minute   0.0.0.0:32768->5432/tcp   pg_test`
</code></pre>

`$ psql -h localhost -p 32768 -d docker -U docker --password` 

Password is `docker`, this can be changed on line 27 in the Dockerfile.

6. Can now execute queries in the psql interface. Example below:
<pre><code>docker=# \l;
docker=# CREATE DATABASE hackathon;
docker=# CREATE SCHEMA users;
docker=# CREATE TABLE users.users (
    userid      TEXT    NOT NULL    PRIMARY KEY,
    username    TEXT    NOT NULL,
    password    TEXT    NOT NULL
);
docker=# SELECT * FROM users.users;
 userid | username | password
--------+----------+----------
(0 rows)
</code></pre>