## Gradle Docker Container based on Alpine Linux

[![Gradle Image][GradleImage]][GradleWebsite]

[![][MicrobadgeLayers]](https://microbadger.com/images/juliano/gradle:3.2-jdk7 "Get your own image badge on microbadger.com")
[![][MicrobadgeVersion]](https://microbadger.com/images/juliano/gradle:3.2-jdk7 "Get your own version badge on microbadger.com")

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

To cache the project dependencies just create a data volume container and mount it:

```bash
docker create -v /gradle/caches --name gradle-cache juliano/gradle /bin/true
docker run --rm -v $PWD/:/app --volumes-from gradle-cache juliano/gradle clean test war
```

## Docker Compose

Working with Docker Compose is equally simple. Create a [named volume][ComposeNamedVolumes] for cache:

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
      - gradle-cache:/gradle/cache

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
[MicrobadgeLayers]: https://images.microbadger.com/badges/image/juliano/gradle:3.2-jdk7.svg
[MicrobadgeVersion]: https://images.microbadger.com/badges/version/juliano/gradle:3.2-jdk7.svg
[ComposeNamedVolumes]: https://docs.docker.com/compose/compose-file/#/volumes-volumedriver

