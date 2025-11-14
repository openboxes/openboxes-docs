# Creating A New Docker Image

### Creating a Docker Image

[OpenBoxes release images](https://github.com/openboxes/openboxes/pkgs/container/openboxes) are automatically published to GitHub packages whenever a commit is tagged for release (see [the workflow file](https://github.com/openboxes/openboxes/blob/develop/.github/workflows/docker-image.yml) for details). No manual work required.

However, if you ever need to manually create a Docker image for the application, you can do so by following these instructions:

#### Prerequisites

1. Install [Docker](https://docs.docker.com/) (20.04+)
2. Clone the [openboxes repository](https://github.com/openboxes/openboxes)
3. Set up an [openboxes database with a valid db user](https://openboxes.gitbook.io/contributor-guide/software-development/onboarding/running-openboxes-locally#id-2.-configure-the-database-instance)

#### Steps

1. Start Docker
2. Navigate to the root directory of the openboxes repository
3. Run `./gradlew prepareDocker -Dgrails.env=prod`
   1. This produces an executable `openboxes.war` file, then copies it and its configuration files to the `/build/docker` directory. Note that the generated WAR file contains an embedded Tomcat servlet.
4. Run `docker build --tag="openboxes/openboxes:latest" build/docker/`
   1. This will take in the WAR file and build a Docker image for the app.



### Running Docker Images

Once you have a Docker image (whether it's an official release or one you created yourself) you can use it to start up a containerized version of OpenBoxes.

We assume that you have already configured your database server by this point.

We provide [Docker Compose files](https://github.com/openboxes/openboxes/tree/develop/docker) that greatly simplify the process of starting up your application containers and hooking them up to your SQL server, but if you'd rather start your container manually via docker commands you can do so via the following:

If running an official release image, run the following:

* run `docker run -p 8080:8080 --name=openboxes ghcr.io/openboxes/openboxes:latest`&#x20;
  * If you need a specific version, you can replace `latest` with that version (such as `v0.9.5`)

If running a manually created image, run the following:

* `docker run -p 8080:8080 --name=openboxes openboxes/openboxes:latest`&#x20;

Then navigate to `http://localhost:8080/openboxes`  to access your server.

#### **Overriding Environment Variables**

When running the application locally, the default environment variables are likely adequate, but if you need to customize them for your specific setup, you can do so via a `.env` file.

* Create a `docker/.env` file ([see the .env.example file](https://github.com/openboxes/openboxes/blob/develop/docker/.env.example) for reference)&#x20;
* Add the `--env-file` parameter to your docker run command
  * For example:  `docker run --env-file=docker/.env -p 8080:8080 --name=openboxes openboxes/openboxes:latest`

Alternatively, you can directly provide environment variables via the `--env` parameter.

For example: `docker run -p 8080:8080 --name=openboxes --env DATASOURCE_USERNAME='openboxes' --env=DATASOURCE_PASSWORD='openboxes' openboxes/openboxes:latest`

#### **Persistable Logs (journald)**

If you'd like the application logs to be persisted after the container has been stopped/removed, run the docker container with _journald_ agent.

For example: `docker run --env-file=docker/.env -p 8080:8080 --name=openboxes --log-driver=journald openboxes/openboxes:latest`

The logs will then be able to be accessed with: `journalctl -u docker CONTAINER_NAME=openboxes`



#### **Running against a database server on the host machine**

You can connect a containerized OpenBoxes instance to a SQL server that is running on the host by using the `host.docker.internal` keyword in the JDBC url.

Again, this process is much simpler via use of the [Docker Compose files](https://github.com/openboxes/openboxes/tree/develop/docker), but if you want to do it manually, you can do so by overriding the `DATASOURCE_URL` environment variable and by adding the host gateway.

For example: `docker run -p 8080:8080 --name=openboxes --env DATASOURCE_URL='jdbc:mysql://host.docker.internal:3306/openboxes?useSSL=false' --add-host host.docker.internal:host-gateway openboxes/openboxes:latest`

You will also need to set `bind.address=0.0.0.0` in your SQL configuration.
