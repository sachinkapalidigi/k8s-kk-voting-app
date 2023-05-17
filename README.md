# Deploying with pods/deployments 

1. Create service deployments `kubectl create -f services`
*Above will create all services in the directory services*

2. Create pods only `kubectl create -f pods` *OR*
3. Create deployments which will create replica set and pods `kubectl create -f deployments` where pods and deployments are folder names.


## Info
1. There are 5 different containers
 - Python Voting app pod & container: pyp
 - Result App pod & container: rp
 - Postgres Pod: pg 
 - Redis Pod: red
 - Worker Pod: wp
2. Interlinked services
 - pyp looks to connect to pg through a service: postgres service(host: db)
 - wp looks to connect to pg and redis throught service: redis service(host: redis) and postgres service
 - rp looks to connect to redis through a service: redis service(host:redis)
 - pyp and rp are exposed to the outside world through NodePort services: voting-service & result-service(file names different)
 - Use `minikube service voting-service --url` & `minikube service result-service --url`
3. Start services first, postgres and redis deployments next. Rest after this. Since the containers may/maynot keep looking for service and might fail. 