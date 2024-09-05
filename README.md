# A GeoServer docker image

This Dockerfile can be used to create images for all geoserver versions since 2.5.

* Based on the official [`tomcat` docker image](https://hub.docker.com/_/tomcat), in particular:
  * Tomcat 9
  * JDK11 (eclipse temurin)
  * Ubuntu Jammy (22.04 LTS)
* GeoServer installation is configurable and supports
  * Dynamic installation of extensions
  * Custom fonts (e.g. for SLD styling)
  * CORS
  * Additional libraries
  * PostgreSQL JNDI
  * HTTPS

This README.md file covers use of official docker image, additional [build](BUILD.md) and [release](RELEASE.md) instructions are available.

## How to run official release?

To pull an official image use ``docker.osgeo.org/geoserver:{{VERSION}}``, e.g.:

```shell
docker pull docker.osgeo.org/geoserver:2.25.2
```

Check <http://localhost/geoserver> to see the geoserver page,
and login with geoserver default `admin:geoserver` credentials.

**IMPORTANT NOTE:** Please change the default ``geoserver`` and ``master`` passwords.

## How to start a GeoServer without sample data?

This image populates ``/opt/geoserver_data/`` with demo data by default. For production scenarios this is typically not desired.

The environment variable `SKIP_DEMO_DATA` can be set to `true` to create an empty data directory.

```shell
docker run -it -p 80:8080 \
  --env SKIP_DEMO_DATA=true \
  docker.osgeo.org/geoserver:2.25.2
```

## How to set the application context path?

By default, GeoServer is served from <http://localhost/geoserver>. Use the environment variable `WEBAPP_CONTEXT` to change the context path.

## Troubleshooting

### How to watch geoserver.log from host?

To watch ``geoserver.log`` of a running container:

```shell
docker exec -it {CONTAINER_ID} tail -f /opt/geoserver_data/logs/geoserver.log
```
