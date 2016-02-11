# docker-port-check using DockerToolbox-1.10.0 and Virtualbox

### Needed a realy simple way to check port access on a docker machine before starting up applications, etc.  Docker has a nice hello-world to insure your docker machine is up and running and this helps to insure you're ok with the ports as well.



docker-machine create -d virtualbox default

eval $(docker-machine env default)

docker run hello-world

docker build -t docker-port-check .

Open port for virtual machine "default" using "Network" settings

docker run -i -t -p 80:8000 docker-port-check

curl http://localhost:80
