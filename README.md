# first-docker-compose

This is to demonstrate how to scale via docker swarm 

## Note: 

App name in this case is getstartedlab

## To Start:

1. ```docker swarm init```
1. ```docker stack deploy -c docker-compose.yml <app name>```

## To Display Currently running:

1. ```docker service ls``` This is a collapsed view based on each individual service

1. ```docker service ps <app name>``` This will list each container in the system

1. ```docker container ls -q``` This will list each unique id of the containers

1. ```docker stack ps <app name>``` This will list each task within the stack

## To Scale:

1. Change the replica number within the docker-compose.yml to the desired number of containers.

1. Run the following command to update the stack to the desired replicas: ```docker stack deploy -c docker-compose.yml <app name>```

## To Take Down:

1. The app: ```docker stack rm <app name>```

1. The entire swarm: ```docker swarm leave --force```