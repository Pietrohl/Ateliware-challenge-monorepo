# Ateliware Challenge - **Amazon**<font color="red">ia</font>

- [Ateliware Challenge - **Amazon**ia](#ateliware-challenge---amazonia)
  - [Demo](#demo)
  - [Technologies](#technologies)
  - [Architecture](#architecture)
  - [System Design Decisions](#system-design-decisions)
    - [Design problems found](#design-problems-found)
  - [Installation](#installation)
  - [Running the Project](#running-the-project)
    - [Local enviroment](#local-enviroment)
    - [Docker dev enviroment](#docker-dev-enviroment)
    - [Docker in prod configuration](#docker-in-prod-configuration)

## Demo

<http://18.231.57.237>

## Technologies

- Typescript
- Node.js 16.x.x
- Express.js 4.x.x
- SWC
- Awillix
- Jest
- Vite
- React 18.x.x
- Material UI (MUI)
- Styled-Components
- Zustand
- Redis
- Nginx

The technologies choosen for the project ware decided in order to achieve the best base for scalability, mantainability and system design.

## Architecture

![Architecture Diagram](/Diagram.jpg "Architecture Diagram")

## System Design Decisions

- Node was choosen since typescript is my most preferable language. A Node.js can be design in a non-blocking way for high demand processing functions, by creating extra workers and making use of the V8 async event driven execution.

- Express for the low level design flexibility, in this project Module Patter was used on the design of services, controllers and repositories.

- Awillix library was chosen to implement a IoC container without the need to use classes and decorators.

- SWC was chosen to compile the node .ts code, since is on avarage 20x faster than tsc and 10x than babel.

- Vite was chosen for the easy to create a spa react app with pre configured bundling.

- Zustand was chosen for state management since uses a similar aproach of redux but is simpler by joining the reducer actions and state parameters, but keeping the one same single data flow principle.

- Redis was chosen for the data persistence since there was no requirements for data reliablility and no multiple schemas. Redis is very performatic for this application.

- Nginx was chosen for reverse proxing and as public files server for its ease to use with docker.

- For the routing algorithm A* was chosen for it's performace on this type non-tree graph problem with only one goal node.

- On A* HashMaps data structure was chosen for saving the priority list of next nodes to evaluate and the visited nodes for path reversing. This was chosen over a B-tree or priority queue since is very easy to implement of JS.

### Design problems found

- A* is very demanding on memory space, and in javascript there is very little control on memory allocation and managament. Because of this there was a need to optmize a few times the algorithm for memory.

- Implementing the docker-compose and Dockerfiles needed a lot of trial and error.

- Base express skeleton took dificult to determine since there is a lot of flexibility and not much opinion from the framework.

## Installation

To use a mock API there is a need to install [Mockoon](https://mockoon.com/), and import the file from Ateliware-challenge-client/mockoon/data.json.

There is also a need to install [Node](https://nodejs.org/en) 16 or newer.

If you want to use docker, you will need to install Docker and Docker-compose also. Otherwise you will need manually install the node modules for both submodules.

```#!/bin/bash
# installing modules express project
cd Ateliware-challenge-server
npm install

# installing modules for vite project
cd ../Ateliware-challenge-client
npm install
```

## Running the Project

Depending on how the project was installed it's possible to run it also using one of three options:

### Local enviroment

to run the project in dev mode locally, you will need to start the express API and the vite dev server on each folder:

First setup enviroment variables for each submodule by creating a .env file in each submodule:

- Ateliware-challenge-server/.env example:
  
```
VITE_API_TARGET=
```

- Ateliware-challenge-server/.env

 ```
PORT=
REDIS_URL=
```

Then, run the fallowing commands on a bash/cmd terminal:

```#!/bin/bash
# running the express API
cd Ateliware-challenge-server
npm run dev

#running vite dev server
cd ../Ateliware-challenge-client
npm run dev
```

### Docker dev enviroment

if you have docker and docker-compose installed, you can run the project in a docker dev enviroment, with hot reload available for both repositories:

```#!/bin/bash
docker-compose build --no-cache
docker-compose up
```

### Docker in prod configuration

To run the project in a pruduction ready configuration:

```#!/bin/bash
docker-compose build -f production.yml --no-cache
docker-compose -f production.yml
```
