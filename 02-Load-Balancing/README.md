[&larr;](../README.md)

### 02 - Load Balancing 

* demonstration of `haproxy`-deployment with and without sticky-sessions 

* create a overlay-network `haproxy-network`

  * `docker network create -d overlay haproxy-network --attachable`

#### 02 - Load Balancing - 01 - Round Robing

* deploy haproxy on `node1`, expose haproxy-listener-port on that node `port 10087` with round-robin load balancing to max. 5 `whoami`-service-tasks (source files in folder `01-roundrobin`)

  * adapt `haproxy.cfg` file, so that the host-url `<host-node1>-10087.direct.labs.play-with-docker.com` is proxied
  * `docker stack deploy -c deploy-infra.yml infra` 

* access the haproxy-stats-page (URL-path `/my-stats`) at `<host-node1>-10087.direct.labs.play-with-docker.com/my-stats`

* deploy the web-stack consisting of 1 `whoami`-service-task

  * `docker stack deploy -c deploy-web.yml web`

* access the haproxy-stats-page (URL-path `/my-stats`) at `<host-node1>-10087.direct.labs.play-with-docker.com/my-stats`

* scale the web-stack to 3 replicas and observe the stats-page

  * `docker service scale web_whoami=3`

* access the whoami server at `<host-node1>-10087.direct.labs.play-with-docker.com` and reload page multiple times

#### 02 - Load Balancing - 02 - Sticky

* deploy haproxy on `node2`, expose haproxy-listener-port on that node `port 10088` with sticky load balancing to max. 5 `whoamisticky`-service-tasks (source files in folder `02-sticky`)

  * adapt `haproxy.cfg` file, so that the host `<host-node2>-10088.direct.labs.play-with-docker.com` is proxied
  * `docker stack deploy -c deploy-infra-sticky.yml infra-sticky`
  
* deploy the web-stack consisting of 1 `whoamisticky`-service-tasks

  * `docker stack deploy -c deploy-web-sticky.yml web-sticky`
  
* scale the web-stack to 4 replicas and observe the stats-page

  * `docker service scale web-sticky_whoamisticky=4` 
  
* access the whoamisticky server and reload page multiple times  

* install `coockie-manager` chrome-extension at `https://chrome.google.com/webstore/detail/cookiemanager-cookie-edit/hdhngoamekjhmnpenphenpaiindoinpo?hl=en`

* remove `SRVID`-coockie and reload again

[&larr;](../README.md)