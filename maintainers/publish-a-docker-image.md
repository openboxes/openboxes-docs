---
description: How release images are published, and how to build one by hand if you need to.
---

# Publish a Docker Image

[OpenBoxes release images](https://github.com/openboxes/openboxes/pkgs/container/openboxes) are automatically published to GitHub Packages whenever a commit is tagged for release (see [the workflow file](https://github.com/openboxes/openboxes/blob/develop/.github/workflows/docker-image.yml) for details). **No manual work is required as part of a normal release** — see [Cut a Release](cut-a-release.md).

If you ever need to manually create a Docker image for the application, follow these instructions.

## Prerequisites

1. Install [Docker](https://docs.docker.com/) (any Docker Engine v24 or later should do)
2. Clone the [openboxes repository](https://github.com/openboxes/openboxes)
3. Set up an [openboxes database with a valid db user](/contribute-code/set-up-your-environment/running-openboxes-locally#id-2.-configure-the-database-instance)

## Steps

1. Start Docker
2. Navigate to the root directory of the openboxes repository
3. Run `./gradlew prepareDocker -Dgrails.env=prod`
   1. This produces an executable `openboxes.war` file, then copies it and its configuration files to the `/build/docker` directory. Note that the generated WAR file contains an embedded Tomcat servlet.
4. Run `docker build --tag="openboxes/openboxes:latest" build/docker/`
   1. This will take in the WAR file and build a Docker image for the app.

To run the image you've just built, see [Running with Docker](/contribute-code/set-up-your-environment/running-with-docker).
