# vagrant

* Complete provision of platform with Vagrant
![Vagrant Diagrom](./img/vagrant.png)

You need Vagrant to be able to launch the full stack.

    vagrant up

in this stack is to be provisioned:

    - Swarm Cluster
    - Registry
    - Jenkins
    - Portainer (optional)
    - Traefik
    - Prometheus
    - Grafana



# Goals of the Vagrant Repo:

* Provision a full platfomr with Traefik Stack with Prometheus metrics enabled , grafana and Jenkins

![WorkFlow Diagram](./img/workflow.png)

Verify all the services have been provisioned. The Replica count for each service should be.

Be very patient!!!!

**Note this can take a couple minutes**

# you need to add the following domains in your host file

## Login to traefik and Visualize Dashboard

    http://docker.localhost:8080/  -> traefik dashboard

## Login to Grafana and Visualize Metrics

    http://grafana.localhost (add 127.0.0.1 to /etc/hosts)

Username: admin
Password: superseguro

## Login to Prometheus

    http://prometheus.localhost  (add 127.0.0.1 to /etc/hosts)

## Login to Protainer

    http://localhost:9000 

## Login to Jenkisn

    http://jenkisn.localhost (add 127.0.0.1 to /etc/hosts)

## Login to APP

    http://apisample.localhost (add 127.0.0.1 to /etc/hosts)

![WorkFlow Diagram](./img/deploy.png)

# Blue Green deploy or Canary changing only 2 labels

you can change and scale the application by modifying the stack , modify "replicas" in appli-green.yml or appli-blue.yml and update stack whit Jenkisn pipeline 

yoy change routers only update label in stack , you can get a blue green environment or canary depending on the weights of the routes

example:

    docker service update --label-add "traefik.http.routers.colors-green.priority=0" green_colors-green
    docker service update --label-add "traefik.http.routers.colors-blue.priority=100" blue_colors-blue

    docker service update --label-add "traefik.http.routers.colors-green.priority=100" green_colors-green
    docker service update --label-add "traefik.http.routers.colors-blue.priority=0" blue_colors-blue

# Repository list

Vagrant: deploy platform, this repository triggers the action:
    https://github.com/stirner/vagrant.git

Cicd: traefik , grafana, Prometheus and deploy with Jenkins:
    https://github.com/stirner/cicd.git

ApiSample: the code, Builds and Jenkins Pipelines: 
    https://github.com/stirner/apiSample

# Deploy Stack -> Vagrant -> VIDEO 

[![Deploy Vagrant](https://img.youtube.com/vi/SYDjJjGHqWQ/mq3.jpg)](https://www.youtube.com/watch?v=SYDjJjGHqWQ)

# Deploy App -> Jenkins -> VIDEO

[![Deploy Vagrant](https://img.youtube.com/vi/BQbzubuex9E/mq3.jpg)](https://www.youtube.com/watch?v=BQbzubuex9E)


# TO BE DONE

**solve datasource fix in grafana

**add integration Jenkisn - Sonarcube 

**launch Stress Test whit Jmeter 




