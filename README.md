# Docker Port Check using DockerToolbox 17.07.0-ce and Virtualbox 6.0 on WIN 7

#### Needed a really simple way to check port access externally from a docker machine before starting up applications, etc.  Docker has a nice hello-world to insure your docker machine is up and running and this helps to insure you're  ok with the ports as well.

Create the docker machine and build the runtime container
```
docker-machine create -d virtualbox default  
eval $(docker-machine env default)  
docker run hello-world  
docker build -t port-check-runtime .
``` 
```
Note: container "port-check" exposes it's http service on port 8000 and we redirect to the docker-machine
port 80 
```
```
docker run -d -p 80:8000 --name port-check port-check-runtime  
curl http://$(docker-machine ip default)
```
```
Note: If you prefer to use "localhost" instead of "$(docker-machine ip default)" you'll need to set the
VirtualBox NAT Router 
```
```
docker-machine stop
vboxmanage modifyvm default --natpf1 ,tcp,,80,,80
docker-machine start
  
docker start port-check
curl http://localhost
```  