# QGIS Docker Images

This repository automates the build of QGIS desktop and QGIS server Docker images.

## Desktop

[![Docker Hub](https://img.shields.io/docker/pulls/qgis/qgis)](https://hub.docker.com/r/qgis/qgis)

- [Documentation](./desktop/README.md)

## Server

[![Docker Hub](https://img.shields.io/docker/pulls/qgis/qgis-server)](https://hub.docker.com/r/qgis/qgis-server)

- [Documentation](./server/README.md)

## Quick Start

### Prerequisites
- Docker and Docker Compose installed

### Running QGIS Server

1. Start the containers:
```bash
docker-compose up -d
```

2. Add your QGIS project files to `test/data/` following this structure:
```
test/data/
  └── your_project/
      └── your_project.qgs
```

3. Access your project via WMS/WFS:
```
http://127.0.0.1:8010/ogc/your_project/?SERVICE=WMS&REQUEST=GetCapabilities
```

### Configuration Fixes Applied

This setup includes fixes for common deployment issues:

1. **Nginx Configuration Path**: Updated `docker-compose.yml` to use the correct nginx config:
   - Changed: `./conf/nginx-fcgi-sample.conf` → `./server/conf/nginx-fcgi-sample.conf`

2. **Container Name Resolution**: Updated nginx upstream configuration to match the actual container naming:
   - Changed: `oq-qgis-server_qgis-server_1:9993` → `qgis-docker-main_qgis-server_1:9993`
   - Location: `server/conf/nginx-fcgi-sample.conf:47`

These changes ensure nginx can properly communicate with the QGIS server container.
