# RabbitMQ
## On Docker

#### We have to use files in rabbitmq-docker for deploy rabbitmq like container on docker

`cd ./rabbitmq-docker`

`docker-compose build`

`docker-compose up -d`

# RabbitMQ on kubernetes (StatefulSet)

#### At first we have to deploy rbac role

`kubernetes apply -f rabbitmq_rbac.yaml`

#### Add Persistent volume and Persistent Volume claim

`kubernetes apply -f rabbitmq_pv.yaml`

`kubernetes apply -f rabbitmq_pvc.yaml`

#### Add internal service & service for LoadBalancer

`kubernetes apply -f rabbitmq_service.yaml`

`kubernetes apply -f rabbitmq_service_ext.yaml`

#### Add configurations

**Clusters VIP** - you must change this value to your k8s clusters virtual IP

**clusters.domainname** - you must change this value to your k8s cluster's domainname

`kubernetes apply -f rabbitmq_configmap.yaml`


#### At the end deploy statefulset

**clusters.domainname** - you must change this value to your k8s cluster's domainname

`kubernetes apply -f rabbitmq_statefulset.yaml`


#### Add admin user

`rabbitmqctl add_user admin admin123`

`rabbitmqctl set_user_tags admin administrator`

`rabbitmqctl set_permissions -p / admin ".*" ".*" ".*"`
