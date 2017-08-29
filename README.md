This is a Docker image of [BungeeCord](https://www.spigotmc.org/wiki/bungeecord/)
and is intended to be used at the front-end of a cluster of
[itzg/minecraft-server](https://hub.docker.com/r/itzg/minecraft-server/) containers.

[![Docker Automated buil](https://img.shields.io/docker/automated/thenetyeti/docker-bungeecord.svg)](https://hub.docker.com/r/thenetyeti/docker-bungeecord/)[![Docker Build Statu](https://img.shields.io/docker/build/thenetyeti/docker-bungeecord.svg)](https://hub.docker.com/r/thenetyeti/docker-bungeecord/)[![Docker Pulls](https://img.shields.io/docker/pulls/thenetyeti/docker-bungeecord.svg)](https://hub.docker.com/r/thenetyeti/docker-bungeecord/)[![Docker Stars](https://img.shields.io/docker/stars/thenetyeti/docker-bungeecord.svg?maxAge=2592000)](https://hub.docker.com/r/thenetyeti/docker-bungeecord/)[![](https://images.microbadger.com/badges/image/thenetyeti/docker-bungeecord.svg)](https://microbadger.com/images/thenetyeti/docker-bungeecord "Get your own image badge on microbadger.com")[![](https://images.microbadger.com/badges/version/thenetyeti/docker-bungeecord.svg)](https://microbadger.com/images/thenetyeti/docker-bungeecord "Get your own version badge on microbadger.com")

## Environment Settings

* **BUNGEE_JOB_ID**=lastStableBuild

  The Jenkins job ID of the artifact to download and run and is used when
  deriving the default value of `BUNGEE_JAR_URL`

* **BUNGEE_BASE_URL**=https://ci.md-5.net/job/BungeeCord

  Used to derive the default value of `BUNGEE_JAR_URL`

* **BUNGEE_JAR_URL**=${BUNGEE_BASE_URL}/${BUNGEE_JOB_ID}/artifact/bootstrap/target/BungeeCord.jar

  If set, can specify a custom, fully qualified URL  of the BungeeCord.jar

* **MEMORY**=512m

  The Java memory heap size to specify to the JVM.

* **INIT_MEMORY**=${MEMORY}

  Can be set to use a different initial heap size.

* **MAX_MEMORY**=${MEMORY}

  Can be set to use a different max heap size.

* **JVM_OPTS**

  Additional -X options to pass to the JVM.

## Volumes

* **/server**

  The working directory where BungeeCord is started. This is the directory
  where its `config.yml` will be loaded.
  
* **/plugins**

  Plugins will be copied across from this directory before the server is started.

## Ports

* **25577**

  The listening port of BungeeCord, which you will typically want to port map
  to the standard Minecraft server port of 25565 using:

  ```
  -p 25565:25577
  ```

## Scenarios

### Running non-root

This image may be run as a non-root user but does require an attached `/server`
volume that is writable by that uid, such as:

    docker run ... -e UID=$uid -e GID=$gid -v $(pwd)/data:/server itzg/bungeecord
