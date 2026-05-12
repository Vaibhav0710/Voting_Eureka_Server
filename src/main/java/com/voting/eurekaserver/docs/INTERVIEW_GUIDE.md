# Interview Guide: Eureka Server (Service Discovery)

### Q1: What is the role of Eureka in our Voting System?
**Answer:** Eureka acts as the **Service Registry**. It maintains a real-time list of all active instances of our microservices. When `user-service` or `candidate-service` starts, it registers its network location (IP and Port) with Eureka.

### Q2: Why are `register-with-eureka` and `fetch-registry` set to `false` in the server's `application.yml`?
**Answer:** These settings are used for Eureka Servers. Since this instance *is* the registry, it doesn't need to register with another server or fetch a registry from another node (common in standalone development setups).

### Q3: Describe the "Self-Preservation" mode in Eureka.
**Answer:** Eureka enters self-preservation mode if it stops receiving heartbeats from a large percentage of services (often due to network issues rather than service failure). In this mode, it stops expiring service instances to prevent the gateway from losing all routing information.

### Q4: How does the Gateway interact with Eureka?
**Answer:** The Gateway is a **Eureka Client**. It periodically fetches the registry from the Eureka Server and uses it to resolve logical service names (like `lb://user-service`) into actual network addresses using a Load Balancer.

### Q5: What is the heartbeat mechanism?
**Answer:** Every service registered with Eureka sends a "heartbeat" (usually every 30 seconds). If Eureka doesn't receive a heartbeat for a specific period (e.g., 90 seconds), it assumes the service is down and removes it from the registry.

### Q6: How do you handle Eureka High Availability?
**Answer:** In a production environment, we would run multiple Eureka instances and have them register with each other (Peer Awareness). Services would be configured with a comma-separated list of all Eureka URLs.

### Q7: What is Service Metadata in Eureka?
**Answer:** Metadata is a set of key-value pairs that a service can send to Eureka during registration (e.g., `version: 1.2.0`, `zone: us-east-1`). The Gateway can use this metadata to implement **Version-based Routing** or **Zone-aware Load Balancing**.

### Q8: How does Eureka differ from Zookeeper or Consul?
**Answer:** Eureka follows the **AP (Availability and Partition tolerance)** principle in CAP. It prioritizes keeping the registry available even if it's slightly outdated. Zookeeper/Consul are **CP (Consistency and Partition tolerance)**; they prioritize accuracy and might block if nodes can't agree, which can bring down a microservices system if the registry becomes a bottleneck.

### Q9: What is the Eureka "Eviction" process?
**Answer:** Eviction is the background process where Eureka scans the registry for instances that haven't sent a heartbeat within the `lease-expiration-duration` (default 90s). If found, they are removed. However, if **Self-Preservation** is active, eviction is paused.

### Q10: Why is the Eureka Dashboard useful?
**Answer:** It provides a visual real-time health check of the entire system. We can see:
1. Which instances are "UP" or "DOWN."
2. The system's "Self-Preservation" status.
3. General health metrics of the server (Memory, Threads).
