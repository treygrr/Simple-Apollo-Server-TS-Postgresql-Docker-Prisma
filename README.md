# Simple Apollo Server + TS + Postgresql + Docker
The overall goal of this project is to allow a user to pull this with only docker on their machine and get up and running with development.

If you are able to run `docker run hello-world` you are all set

## Windows Docker Install: 
  - Ensure that Virtualization is enabled in your bios
  - All subsequent commands need to be ran from and administrative powershell
  - ```wsl --install```
  - If you see help text after running the above command you have WSL installed
  - ```wsl --install -d ubuntu```

## Windows: From here you need to upgrade WSL 1 to WSL 2

The wsl --set-version command can be used to downgrade from WSL 2 to WSL 1 or to update previously installed Linux distributions from WSL 1 to WSL 2.
  - [Download WSL 2 Kernel Package](https://learn.microsoft.com/en-us/windows/wsl/install-manual#step-4---download-the-linux-kernel-update-package) and install
  - ```wsl --set-default-version 2```
  - ```wsl --install -d ubuntu```
  - Install Docker Desktop

## Linux
Install from your favorite flavor package manager

## Mac
```brew install docker```

# Running the Project
1. Copy .env.example to .env
1. Configure .env environment variables as needed
1. To start the project in docker
   -  ```docker compose up -d```
1. SSH to "container"
   - ```docker exec -it node sh```
   - ```docker exec -it postgres sh```
1. Attach to running container process output
   - ```docker attach node```
   - ```docker attach postgres```

## Use full commands in Node Container
1. ```yarn prisma migrate dev```
   - This will create a migration for changes that have occurred within prisma/schema.prisma
1. ```yarn```
   - Installs node dependencies for the project
1. ```yarn dev```
   - Starts the development server and runs it on your configured port
1. ```yarn compile```
   - Build the project and outputs contents to /dist folder

# Docker
The docker file called docker-compose.yml is the configuration and orchestration software for this repository. 

This starts a container named "node" that has Node Version 18 installed. The working director for the container is /usr/app. Running the above script to SSH into the container should drop you into this directory as the working directory is configure to /usr/app as well. 

Any files that change on your local system as you work will be symlinked into the Node container and should trigger a reload of the dev environment for maximum testing and iteration speed.

Everything in this directory is mounted into /usr/app

Node will not start if postgres container is not running.

Postgres data will get mounted the the volume called postgres-data on your host system.