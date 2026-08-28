---
description: Running OpenBoxes in a container instead of building it locally.
---

# Running with Docker

If you don't need to modify the application itself — for example you're writing translations, reproducing a bug report, or testing against a specific release — running OpenBoxes in a container is faster than [setting it up locally](running-openboxes-locally.md).

{% hint style="info" %}
We provide [Docker Compose files](https://github.com/openboxes/openboxes/tree/develop/docker) that greatly simplify the process of starting up your application containers and hooking them up to your SQL server. We recommend using the compose files instead of trying to manually run and configure the containers yourself.
{% endhint %}

We assume that you have already configured your database server by this point — see [Configure the database instance](running-openboxes-locally.md#id-2.-configure-the-database-instance).

## Starting a container

To run an official release image:

```
docker run -p 8080:8080 --name=openboxes ghcr.io/openboxes/openboxes:latest
```

If you need a specific version, you can replace `latest` with that version (such as `v0.9.5`). [Release images](https://github.com/openboxes/openboxes/pkgs/container/openboxes) are published automatically for every tagged release.

To run an image you built yourself (see [Publish a Docker Image](../../for-maintainers/publish-a-docker-image.md)):

```
docker run -p 8080:8080 --name=openboxes openboxes/openboxes:latest
```

Then navigate to `http://localhost:8080/openboxes` to access your server.

## Overriding environment variables

When running the application locally, the default environment variables are likely adequate, but if you need to customize them for your specific setup, you can do so via a `.env` file.

* Create a `docker/.env` file ([see the .env.example file](https://github.com/openboxes/openboxes/blob/develop/docker/.env.example) for reference)
* Add the `--env-file` parameter to your docker run command, for example:

```
docker run --env-file=docker/.env -p 8080:8080 --name=openboxes openboxes/openboxes:latest
```

Alternatively, you can directly provide environment variables via the `--env` parameter:

```
docker run -p 8080:8080 --name=openboxes \
  --env DATASOURCE_USERNAME='openboxes' \
  --env DATASOURCE_PASSWORD='openboxes' \
  openboxes/openboxes:latest
```

## Persisting logs (journald)

If you'd like the application logs to be persisted after the container has been stopped or removed, run the container with the _journald_ logging driver:

```
docker run --env-file=docker/.env -p 8080:8080 --name=openboxes --log-driver=journald openboxes/openboxes:latest
```

The logs can then be accessed with:

```
journalctl -u docker CONTAINER_NAME=openboxes
```

## Connecting to a database on the host machine

{% hint style="info" %}
This process is much simpler via use of the [Docker Compose files](https://github.com/openboxes/openboxes/tree/develop/docker), and is specifically handled for you in [docker-compose-hostdb.yml](https://github.com/openboxes/openboxes/blob/develop/docker/docker-compose-hostdb.yml).
{% endhint %}

You can connect a containerized OpenBoxes instance to a SQL server that is running on the host by using the `host.docker.internal` keyword in the JDBC url.

To achieve this, override the `DATASOURCE_URL` environment variable and add the host gateway via the `--add-host` parameter:

```
docker run -p 8080:8080 --name=openboxes \
  --env DATASOURCE_URL='jdbc:mysql://host.docker.internal:3306/openboxes?useSSL=false' \
  --add-host host.docker.internal:host-gateway \
  openboxes/openboxes:latest
```

You will also need to set `bind.address=0.0.0.0` in your SQL configuration.
