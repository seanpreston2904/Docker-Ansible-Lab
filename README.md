# Docker Ansible Hub
## Overview
This repo contains the required files to deploy an Ansible lab environment using Docker.
## Requirements
You will need `docker` and `docker-compose` installed.
## Usage
The following command can be issued to start the Ansible lab environment (ensure your current working directory is the root of the repo):
```bash
docker-compose up -d --build
```

While the lab environment can be terminated using the following command:
```bash
docker-compose down
```

You can open a bash session with the control node using:
```bash
docker-compose exec ansible-control /bin/bash
```