# Introduction to AWS Load Balancer

## What is a Load Balancer?

A **Load Balancer in AWS** is a service that automatically distributes incoming application traffic across multiple targets such as **Amazon EC2 instances, containers, and IP addresses**.

It acts like a **traffic controller**, ensuring that no single server becomes overloaded. This improves the **availability, scalability, and reliability** of applications.

AWS provides a managed service called **Elastic Load Balancing (ELB)** which automatically distributes incoming traffic and scales according to demand.

Elastic Load Balancing supports three types of load balancers:

- Application Load Balancer (ALB)
- Network Load Balancer (NLB)
- Gateway Load Balancer (GWLB)

---

# Types of Load Balancers in AWS

## 1. Application Load Balancer (ALB)

The **Application Load Balancer** operates at **Layer 7 (Application Layer)** of the OSI model.

It is designed specifically for **HTTP and HTTPS traffic** and is commonly used for **web applications and microservices**.

### Key Features

- Advanced routing based on:
  - URL path
  - Hostname
  - Query string
  - HTTP headers
- Supports **WebSockets**
- Supports **SSL termination**
- Integrates with **AWS Web Application Firewall (WAF)**
- Ideal for **containerized and microservice architectures**

---

## 2. Network Load Balancer (NLB)

The **Network Load Balancer** operates at **Layer 4 (Transport Layer)** of the OSI model.

It is designed to handle **extremely high performance traffic** with **very low latency**.

### Key Features

- Supports **TCP, UDP, and TLS traffic**
- Provides **static IP addresses**
- Preserves the **client's source IP address**
- Capable of handling **millions of requests per second**
- Suitable for **high-performance applications**

---

## 3. Gateway Load Balancer (GWLB)

The **Gateway Load Balancer** operates at **Layer 3 (Network Layer)**.

It is used to **deploy, scale, and manage third-party virtual appliances** such as security solutions.

### Common Use Cases

- Firewalls
- Intrusion Detection Systems (IDS)
- Intrusion Prevention Systems (IPS)
- Network security appliances

---

# Difference Between Application Load Balancer and Network Load Balancer

| Feature | Application Load Balancer (ALB) | Network Load Balancer (NLB) |
|-------|----------------------------------|------------------------------|
| OSI Layer | Layer 7 (Application Layer) | Layer 4 (Transport Layer) |
| Traffic Type | HTTP, HTTPS | TCP, UDP, TLS |
| Routing | Content-based routing (URL, headers, etc.) | Connection-based routing |
| Performance | Optimized for web applications | Extremely high throughput and low latency |
| Source IP Preservation | Not preserved (Load Balancer IP is used) | Preserved |
| Use Case | Web applications, microservices | Gaming, IoT, real-time communication |
| Static IP Support | No | Yes |
| WebSocket Support | Yes | No |

---

# Summary

- **ALB** → Best for **web applications and microservices**
- **NLB** → Best for **high-performance, low-latency applications**
- **GWLB** → Best for **network security appliances**

All three are part of **AWS Elastic Load Balancing**, which helps improve **application availability, scalability, and fault tolerance**.
