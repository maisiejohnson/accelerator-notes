# Network Devices

## Load Balancers

- Load balancers help to prevent computer systems, websites and webapps from performing suboptimally when dealing with a large influx of requests.
- To reduce the load on a single server, the system is scaled horizontally and we add extra servers, hosting a replica of our app, in parallel. A **load balancer** is used to direct network traffic and distribute the load over all of the servers.
- Load balancers
- When using a load balancer to horizontally scale a system, it is important that the load balancer does not become a single point of failure. With just one load balancer, if the load balancer fails then the whole system goes down - this is clearly not a reliable model. To offset this issue load balancers are often used in high availability pairs. However, in cases where session persistence data is required (that is, throughout a session the same client needs to communicate with same back-end server and the session data needs to be stored), e.g., in e-commerce, it is important that the both load balancers in the pair have close to real time information about the state of the session. This means that the 2 load balancers need to share the same memory, such that if the load balancer that a given clients requests have been routed by fails, the other load balancer can pick up where the other one left off and route the clients requests to the same back-end server. Thus, high-availability pair of load balancers make a given system overall more reliable, but this does come at the cost of extra hardware and complexity.

#### Load Balancing Algorithms

Load balancing algorithms are the programmatic logic used by load balancers to decide how requests should be distributed over a software system's resources.

##### Static Load Balancing Algorithms

A static load balancing algorithm does not take into account the state of the system when deciding how to distribute tasks/ requests over system resources. Examples include:

- **Round Robin:** network traffic is distributed to a list of servers in rotation. This algorithm works best the servers in the list have roughly equal computing capabilities, e.g., CPU & RAM. This is because this algorithm has no way to favour servers with higher computing capabilities and as a result servers with lower computing capabilities will perform suboptimally relative to those with higher computing capabilities. -**Weighted Round Robin:** The weighted round robin load balancing algorithm allows site administrators to assign weights to each server, based on criteria like computing power and traffic handling capabilities. Higher weights are assigned to servers that can deal with greater loads, and as such network traffic is directed to these servers more frequently that to servers with a lower weighting.
- **IP Hash:** An algorithm is used that generates a unique hash key from the source and destination IP address of the client and server. This key is then used to allocate the client to a particular server. If a client needs to connect to a session that is still active after disconnection, the hash key can be regenerated and the client directed to the same back end server.

#### Dynamic Load Balancing Algorithms

---

## Proxies

---

## Firewalls
