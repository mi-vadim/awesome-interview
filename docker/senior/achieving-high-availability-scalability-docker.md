Achieving high availability and scalability with Dockerized applications, especially when focusing on Kubernetes as the orchestration platform, involves leveraging Kubernetes' robust ecosystem, features, and best practices. Here's how you can accomplish this:

### High Availability in Kubernetes

1. **Multi-node Cluster Deployment**: Distribute your Kubernetes nodes across multiple availability zones to protect your applications from zone failures.

2. **Pod Replication**: Use Deployments and StatefulSets to ensure that multiple instances of your pods are running at any given time. Kubernetes automatically replaces failed pods to maintain the desired state.

3. **Liveness and Readiness Probes**: Implement liveness probes to restart containers that become unresponsive and readiness probes to ensure traffic is only sent to pods ready to handle requests.

4. **Persistent Storage**: Utilize Persistent Volumes (PVs) and Persistent Volume Claims (PVCs) with storage solutions that support data replication and automatic failover to ensure data persists beyond pod lifecycles.

5. **Service Discovery and Load Balancing**: Kubernetes Services act as an abstract layer and load balancer for a set of pods, providing a single access point and distributing traffic to maintain availability.

### Scalability in Kubernetes

1. **Horizontal Pod Autoscaler (HPA)**: Automatically scales the number of pod replicas in a deployment or replica set based on observed CPU utilization or custom metrics.

2. **Vertical Pod Autoscaler (VPA)**: Adjusts the CPU and memory reservations of pods in a deployment, ensuring pods have the resources they need without over-provisioning.

3. **Cluster Autoscaler**: Dynamically adjusts the size of your Kubernetes cluster based on the demands of your workloads and the utilization of your nodes.

4. **Manual Scaling**: Provides the ability to manually scale the number of replicas in a deployment for immediate response to changing requirements.

5. **Efficient Resource Allocation**: Define resource requests and limits for your containers to ensure optimal allocation of resources across your nodes, preventing overallocation and ensuring scalability.

### Example Scenario

Consider an e-commerce platform deployed on Kubernetes with a microservices architecture:

- The front-end, back-end, and database services are deployed as separate microservices, each managed by Kubernetes Deployments for high availability.
- Persistent Volume Claims are used for database storage, ensuring data persistence across pod restarts and failures.
- A Kubernetes Service is defined for each microservice, providing stable IP addresses and DNS names for service discovery and internal load balancing.
- Horizontal Pod Autoscaler is configured for the front-end and back-end services to automatically scale the number of replicas based on CPU and memory usage metrics.
- The Cluster Autoscaler is enabled on the Kubernetes cluster to add or remove nodes based on the overall demand and resource utilization, ensuring the cluster can scale up during peak times and scale down during off-peak times.

### Summary

By leveraging Kubernetes' features for deployment, service discovery, scaling, and self-healing, you can achieve a highly available and scalable architecture for Dockerized applications. This approach ensures that applications can handle failures gracefully and scale dynamically in response to varying loads, all without relying on Docker Swarm for orchestration.