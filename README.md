# Purpose
### Doc example requerements
The current documents represents an example to a minimal documentation needed over each project develooped and looks a complete specification of Dependencies, undestand the needed configuration to Build, Relase and Run and provide a verificable mecanish to mount a development environment, fully runnable in a localhost environment

# Project Name - Code Name if Exists
Shown in this section a description of module, specially attention to describe the scope of domain. Include a short description of their functionallity. You can use short descriptions with the name of the pattern that represents or if a common piece of arquitecture. E.g: Credential Federator facade over Google Firebase.
When you use a custom implementation to solve a piece of domain, please indicate that. E.g. Custom chat over mongo based in XMPP protocol or Custom OAuth2 implementation

## Getting Started
### Dependencies
Describe a list of services dependencies needed to run the project, their version and the source from you obtain the pieces.
You must think that the developer have their own version of services, OS and tools and needs mounts a new environment according the dependencies described here.
This section does not include package.json 

- [Docker compose version 3.8 or upper](https://docs.docker.com/compose/compose-file/compose-versioning/)
- [NodeJS v18)(https://nodejs.org/es/about/releases/)
- [Python 3.9)(https://www.python.org/downloads/)
- [Anaconda CUDA needed](https://www.anaconda.com/)
- New Relic account

Be explicit, this list is used by the DevOps/DevSecOps teams to approve/reject a deploy in controlled infrastructure.
The sense if that a guys, could mount the entire project witout any other assitance that this list

### About the infrastructure
Do you have backing services to run entirelly this project? Explain it here (a list is enought)
- API Services based on NodeJS, containerized into a node:12.7-alpine
- AWS S3 cdn storage, mocked in the container 
- MySQL database based on  official container
- A reverse proxy based on a nginx lastet version from docker hub

If you have a diagram, you could link the file here


### Setup
Be explicit, step by step, and ensure in your local environment that the instructions could be replicate.
Thinks that this steps must be executed by a devops that is not informed about languages, default setups or any config that there are not explicitally explained here
An example below

#### 1. Config environment

##### 1.1. The .env file
Setup environment variables for dev/qa, you can see an example on .env.example or simply override your .env file
```
$ cp .env.example .env
```
If you need a complete reference see the Environment value reference section below

##### 1.2 The /app/environments/environment.dev.ts file
Setup your environment value for developement overriding when compile your code, used by the parameters --configuration when you run ng serve, see this reference
You can simply override your environment.dev.ts file with environment.dev.example
```
$ cd ./src/environments
$ cp environment.dev.example environment.dev.ts
```

#### 2. Install modules node_modules
Over the folder ./ run npm i
```
$ npm i
```

#### 3. Mount the stack using docker-compose
Over the folder ./ run docker-compose up or docker-compose up -d --build, by default in development use a merge of docker-compose.yml & docker-compose.override.yml
```
$ docker-compose up -d --build
```
#### 4. Check the model
The stack mount a mysql server and a dbadminer, accesible via localhost:8000, default password for root is example.
You can run the script stored in ./docker/db.sql that provide an initial structure and data

#### 5. Test the stack
In your browser test the address

open in your browser http://localhost:9001/project/
or make a GET using curl
```
$ curl -G http://localhost:9001/project/
```

5.1 Health check
```
** Front **
$ curl -G http://localhost:9001/project/

** API
$ curl -G http://localhost:9001/api/healthcheck.php

** API + BD Connect (select an id item from accidents table)
$ curl -G http://localhost:9001/api/item?id=<a guid uid>>

** S3 Helper
$ curl -G http://localhost:9001/s3helper/buckets/list

** Reverse proxy (nginx)
$ curl -G http://localhost:9001/healthcheck

** DB Adminer
$ curl -G http://localhost:8000
```

6. Check if your bucket exists or create
This first version haven't enought control about unexpected errors over infra.
You need a bucket created over mock to put (upload) files
Use mock-helper to create it. The bucket used is <>
You can use the follow commands
```
$ curl -X GET http://localhost:9001/s3helper/buckets/list
$ curl -X POST http://localhost:9001/s3helper/buckets/create?bucket=bucket project
$ curl -X GET http://localhost:9001/s3helper/buckets/list
```

#### 6. Run a test
Over the folder .... runs XXX, that contains a batery of test with the happy path
```
$ npm test
```

### Environment values reference
In this section describe each environment value, even when was depecreated
Provide a .env.example (or similar) with the local environment configured

Do you have services exclusivelly in the cloud?
Don't upload in the local example the team credential (even if a dev team credential), but indicates in ENV config list that must config in mandatory way.

This is an example, does not assume that the reader have info about the context

``` 
TAG: autogenerated valued by scripts
APP_NAME: XXX (fixed)
NODE_ENV: development|production, see reference
API_SERVER_PORT: form submit api server, mapped to access directly without pass through the reverse proxy
API_SERVER_URL:  route to access to api server (PHP)  through the reverse proxy (nginx), eg:  http://localhost:9001/api
FRONT_SERVER_PORT:(deprecated), front (angular) running into a docker container, mapped to access directly without pass through the reverse proxy
DB_HOST: used in the connection string by the API Server, store form data into mysql. The database server is only available behind the DMZ, is not exposed. You can use the name assigned to the container into the network defined in docker-compose.override.yml. By default the value is db
DB_USERNAME: user (no root, with restricted grants) to save data on db. The username has a relation with the script creation file stored in /docker/db.sql, eg: userdesa
DB_PASSWORD: password of DB_USERNAME, eg: password
DB_DATABASE:  schema to save form data, related with the params above, eg: databasemop
DB_ROOT_PASSWORD: for scripting or admin purposes, setted into docker-compose.override.yml
DB_ADMINER_PORT: mysql admin web based, accesible via browser without pass through the reverse proxy, eg: http://localhost:8000, variable value eg: 8000

....
``` 


## TO - DO
List the technical debt in an explicit way. This is not a list of items in backlog, referes exclusivally to the knowed technical debt that culd have a problem to understand the real state of the project

- [ ] Stack environment with Authtentication filter
- [ ] Unit test happy path
- [ ] docker-compose.dev or local 
- [ ] New Relic or log monitor
- [ ] Non-blocking function if X Services if not allowed



