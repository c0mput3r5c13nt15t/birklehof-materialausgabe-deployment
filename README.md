# birklehof-materialausgabe-deployment

## Prerequisites
1. [Install Docker](https://docs.docker.com/engine/install/ubuntu/)
2. [Deploy Portainer](https://docs.portainer.io/v/ce-2.11/start/install/server/docker/linux) (optional)
3. Set MaxSessions in /etc/ssh/sshd_config (on remote host) to something like 200

## Deployment
1. Copy the .env.local.example file in the nextjs folder to .env.local and modify it
2. Run `DOCKER_HOST="ssh://user@ip" docker-compose up -d`