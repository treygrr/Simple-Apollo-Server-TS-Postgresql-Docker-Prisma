# Simple Apollo Server + TS + Postgresql + Docker + Prisma
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
   1. If you plan on using the containers to run the project use ```DATABASE_URL="postgresql://admin:passwordHere@postgres:5432/retaildb?schema=public"``` note: that @postgres is the domain within the container service that the node container will use to connect to the db from the node container.
   1. If you plan on using tools running on your system for node use ```DATABASE_URL="postgresql://admin:passwordHere@0.0.0.0:5432/retaildb?schema=public"``` note: that @0.0.0.0:5432 is the domain that the database container is available on your host/local machine. You can set this up with /etc/hosts modifications and point ```0.0.0.0 postgres``` if you want. For sanity and covering bases please configure as needed.

1. Configure .env environment variables as needed
1. To start the project in docker
   -  ```docker compose up -d```
1. SSH to "container"
   - ```docker exec -it node sh```
   - ```docker exec -it postgres sh```
1. Attach to running container process output
   - ```docker attach node```
   - ```docker attach postgres```

# If you don't have [NVM](https://github.com/nvm-sh/nvm)
## Use full commands in Node Container
1. ```yarn prisma migrate dev```
   - This will create a migration for changes that have occurred within prisma/schema.prisma
1. ```yarn```
   - Installs node dependencies for the project
1. ```yarn dev```
   - Starts the development server and runs it on your configured port
1. ```yarn compile```
   - Build the project and outputs contents to /dist folder

# If you have NVM
1. Run ```nvm use``` in the base directory. This will install and switch to the version of node configured for this project.
## Use full commands for node project
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

This starts a container named "node" that has Node Version 18 installed. The working director for the container is ```/usr/app```. Running the above script to SSH into the container should drop you into the aforementioned directory. Since the "working directory" is configured to ```/usr/app```.

Any files that change on your local system as you work will be symlinked into the Node container and should trigger a reload of the dev environment for maximum testing and iteration speed.

Everything in this directory is mounted into /usr/app

Node will not start if postgres container is not running.

Postgres data will get mounted the the volume called postgres-data on your host system.

# Technology used in this project.
## Documentation:
1. [Docker Compose](https://docs.docker.com/compose/)
   1. Container orchestration for dev, allowing you to get new machines up and running quickly.
1. [Node](https://nodejs.org/en/docs/)
   1. Node.js® is a JavaScript runtime built on Chrome's V8 JavaScript engine.
1. [Apollo Server](https://www.apollographql.com/docs/apollo-server/)
   1. Apollo Server is an open-source, spec-compliant GraphQL server that's compatible with any GraphQL client
1. [Prisma](https://www.prisma.io/docs/reference)
   1. Prisma is a next-generation Node.js and TypeScript ORM for PostgreSQL, MySQL, SQL Server, SQLite, MongoDB, and CockroachDB.
1. [Postgres](https://hub.docker.com/_/postgres)
   1. My favorite database - is a powerful, open source object-relational database system with over 35 years of active development that has earned it a strong reputation for reliability, feature robustness, and performance.
1. [Typescript](https://www.typescriptlang.org/)
   1. Because you value your teams sanity - TypeScript is a strongly typed programming language that builds on JavaScript, giving you better tooling at any scale.