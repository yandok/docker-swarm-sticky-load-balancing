[&larr;](../README.md)

### Docker Swarm - 01 - Managing Nodes

* initialize cluster with 3 masters and 1 workers in playground

  * initialize `node1` as docker swarm manager-node
  
    * select `node1` on the left panel. 
    * execute `docker swarm init --advertise-addr $(hostname -i)`
    
  * initialize `node2` and `node3` as docker swarm worker-nodes
  
    * select `node2` / `node3` on the left panel
    * execute the command generated in the output of the init-command on the manager-node
    * `docker swarm join --token <TOKEN> <IP-of-manager>:2377`  

  * verify node setup
  
    * select `node1` on the left panel
    * execute `docker node ls`
      
[&larr;](../README.md)