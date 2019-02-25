## Swarm Notes:

This is a collection of notes on how to properly scale a docker container via docker swarm.

## To Create New VMs Via Hyperv:

1. Setup a switch in hyper v (assuming you have installed hyperv)
    1. Launch Hyper-V Manager
    1. Click Virtual Switch Manager in the right-hand menu
    1. Click Create Virtual Switch of type External
    1. Give it the name myswitch, and check the box to share your host machine’s active network adapter
1. Make several hyperv vms to load balance against
    1. ```docker-machine create -d hyperv --hyperv-virtual-switch "myswitch" <leader vm>```
    1. ```docker-machine create -d hyperv --hyperv-virtual-switch "myswitch" <slave vm>``` 
    1. To confirm they are created: ```docker-machine ls```
    1. To restart a machine: ```docker-machine start <node-name>```

## Initializing a Docker Swarm and Adding Nodes:

1. Initialize one vm to be the manager
    1. ```docker-machine ssh <leader node> "docker swarm init --advertise-addr <myvm1 ip>"``` Note that ```docker-machine ls``` will give you the ip needed.
        1. USE PORT 2377 NOT 2376
1. Setup the second to join the now existing swarm
    1. ```docker-machine ssh <slave node> "docker swarm join --token <token> <ip>:2377"```
1. Run the following to view the nodes within the swarm
    1. ```docker-machine ssh <leader node> "docker node ls"```
1. If you wish to start over you can run the following for each node
    1. ```docker-machine ssh <node-name> "docker swarm leave"```
