## Minified Gradle Docker Container based on Alpine Linux

[![Gradle Image][GradleImage]][GradleWebsite]

[![][MicrobadgeLayers]](https://microbadger.com/images/juliano/gradle "Get your own image badge on microbadger.com") [![][MicrobadgeVersion]](https://microbadger.com/images/juliano/gradle "Get your own version badge on microbadger.com")

## Get the Image
```bash
docker pull juliano/gradle
```

## Usage

The container requires that the project folder is mounted to the `/app` volume. You can use any gradle command, so let's clean, test and generate a war file:

```bash
docker run --rm -v /path/to/project:/app juliano/gradle clean test war
```

or inside the project directory:

```bash
docker run --rm -v $PWD:/app juliano/gradle clean test war
```

### Dependency cache

To cache the project dependencies just create a [named volume][ComposeNamedVolumes] and mount the directory `/gradle/caches` on it:

```bash
docker volume create --name gradle-cache
docker run --rm -v $PWD/:/app -v gradle-cache:/gradle/caches juliano/gradle clean test war
```

## Docker Compose

Working with Docker Compose is equally simple. Create the named volume:

```bash
docker volume create --name gradle-cache
```

Configure the `docker-compose.yml`:

```yml
version: '2'

services:

  gradle:
    image: juliano/gradle
    volumes:
      - ./:/app
      - gradle-cache:/gradle/caches

volumes:
  gradle-cache:
    external: true
```

And run:

```bash
docker-compose run gradle clean test war
```

[GradleImage]: https://gradle.org/wp-content/uploads/2016/07/Gradle.svg
[GradleWebsite]: https://gradle.org/
[MicrobadgeLayers]: https://images.microbadger.com/badges/image/juliano/gradle:3.3-jdk8.svg
[MicrobadgeVersion]: https://images.microbadger.com/badges/version/juliano/gradle:3.3-jdk8.svg
[ComposeNamedVolumes]: https://docs.docker.com/compose/compose-file/#/volumes-volumedriver

