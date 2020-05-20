---
title: Quarkus - Postgresql Database
---

## Step 3: Postgresql Database
Run postgresql database in a docker container
```bash
docker run --rm -d --name pd-database -p 5433:5432 -e POSTGRES_DB=pd -e POSTGRES_USER=pd -e POSTGRES_PASSWORD=pd postgres
```
Options passed:
<pre>
--detach, -d - Run container in background and print container ID
--publish, -p - Publish a container’s port(s) to the host
--name - Assign a name to the container
--env, -e - Set environment variables
</pre>

To start interacting with the database, we can use `docker exec` command to launch interactive shell running inside the container. 
Options `-i` allows us to make the container to wait for interaction from host but actual interaction from the console (terminal) 
is possible after we “allocate tty driver” with flag `-t`. This is an easy alternative to login to PostgreSQL and start exploring it.

```bash
> docker exec -it pgdocker sh

# psql -U pd
psql (12.2 (Debian 12.2-2.pgdg100+1))
Type "help" for help.

postgres=# \l

postgres=# select version();

postgres=# \c pd

pd=# \dt
```
