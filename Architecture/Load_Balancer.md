Load balancing solves a fundamental challenge in computing: how to handle more traffic than a single server can manage on its own.

1. The Core Problem.
As application grows, that single server runs into critical limitations:
 Single Point of Failure (SPOF): If that one server crashes or loses power, your entire application goes offline.
 Capacity Bottleneck: A single machine has finite CPU, memory, and network bandwidth. High traffic leads to slow load times or complete timeouts.
 Maintenance Overhead: You cannot update or upgrade the server without causing downtime for users.

2. The Concept.
A Load Balancer (LB) sits directly between client devices (like phones or browsers) and a collection of backend servers (often called a server pool or server farm).

Instead of clients talking to servers directly, all incoming traffic hits the load balancer first. It performs three key roles:
1. Traffic Routing: Distributes incoming network requests across multiple healthy backend servers.
2. Health Monitoring: Constantly checks if backend servers are responsive. If a server fails, the load balancer automatically redirects traffic away from it.
3. Scalability: Allows you to add or remove backend servers seamlessly without affecting the user experience.

Self-Hosted Software Load Balancers.

NGINX: A versatile open-source web server that also functions as an Application Load Balancer (Layer 7). It excels at routing HTTP requests based on URL paths and managing SSL encryption.

HAProxy: A dedicated, extremely fast load balancer that operates at both Layer 4 (TCP) and Layer 7 (HTTP). It is famous for its high reliability and low memory usage.

Cloud-Managed Load Balancers.

AWS Application Load Balancer (ALB): Operates at Layer 7. It inspects HTTP headers, cookies, and paths—making it ideal for microservices and containerized apps.

AWS Network Load Balancer (NLB): Operates at Layer 4 (TCP/UDP). It can handle millions of requests per second with ultra-low latency without inspecting content.

Cloudflare Global LB: Uses Anycast routing to distribute user traffic across global edge data centers based on geographic location and server health.