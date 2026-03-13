---
AWS-CloudFront
---
---
# Complete CloudFront Production Architecture Diagram
---

## 1. Overview

In real-world cloud architectures, **Amazon CloudFront** sits at the **edge of the infrastructure** and acts as the global entry point for users.

It integrates with multiple AWS services to provide:

* Global content delivery
* Security protection
* High availability
* Scalability
* Low latency performance

Typical production architectures include:

* DNS routing
* Web Application Firewall (WAF)
* CDN caching layer
* Load balancing
* Application servers
* Databases
* Object storage

---

# 2. High-Level CloudFront Production Architecture

```text
                    Internet Users
                          │
                          ▼
                     DNS (Route 53)
                          │
                          ▼
                AWS Web Application Firewall
                          │
                          ▼
                 CloudFront Distribution
                          │
        ┌─────────────────┼─────────────────┐
        │                 │                 │
        ▼                 ▼                 ▼
   Edge Location     Edge Location     Edge Location
        │                 │                 │
        ▼                 ▼                 ▼
         Regional Edge Cache (Optional Layer)
                          │
                          ▼
                   Origin Layer
        ┌─────────────────┼─────────────────┐
        │                 │                 │
        ▼                 ▼                 ▼
     S3 Bucket      Application LB       API Gateway
   (Static Files)        │                   │
                         ▼                   ▼
                    EC2 Instances         Lambda
                         │
                         ▼
                     Database
                     (Amazon RDS)
```

---

# 3. Architecture Components Explained

## 3.1 Users

Users access the application from different geographic locations.

Example:

```text
Users → Website / API / Video Content
```

Requests are routed through the nearest **CloudFront edge location**.

---

# 3.2 DNS Layer (Route 53)

The DNS service resolves the domain name and directs users to the CloudFront distribution.

Example:

```text
www.example.com
```

DNS resolution:

```text
User → Route 53 → CloudFront Distribution
```

Benefits:

* Global DNS routing
* Low latency
* High availability

---

# 3.3 AWS WAF (Security Layer)

AWS WAF filters malicious traffic before it reaches the CloudFront distribution.

It protects against:

* SQL Injection
* Cross-Site Scripting (XSS)
* Bot traffic
* DDoS attacks

Example workflow:

```text
User Request
     │
     ▼
AWS WAF Security Check
     │
     ▼
CloudFront
```

---

# 3.4 CloudFront Distribution (CDN Layer)

CloudFront acts as the **global content delivery layer**.

Functions:

* Caching content
* Accelerating website delivery
* Protecting origin servers
* Reducing latency

Example request flow:

```text
User → CloudFront → Edge Cache
```

If cached:

```text
Content delivered instantly
```

If not cached:

```text
CloudFront → Origin Server
```

---

# 3.5 Edge Locations

Edge locations are data centers located worldwide.

Functions:

* Store cached content
* Deliver content to users quickly

Example:

```text
User (India) → Mumbai Edge Location
User (Europe) → Frankfurt Edge Location
```

---

# 3.6 Regional Edge Cache

Regional edge caches sit between edge locations and origin servers.

Purpose:

* Store less frequently accessed content
* Reduce requests to origin servers

Example flow:

```text
Edge Location
      │
      ▼
Regional Edge Cache
      │
      ▼
Origin Server
```

---

# 3.7 Origin Layer

The origin layer contains the backend services that generate or store content.

CloudFront retrieves data from origins when the cache misses.

Typical origins include:

* S3 buckets
* Application Load Balancers
* API Gateway

---

# 3.8 Amazon S3 (Static Content)

S3 stores static assets such as:

* Images
* HTML files
* CSS
* JavaScript
* Videos

Architecture example:

```text
CloudFront → S3 Bucket
```

Benefits:

* Highly scalable storage
* Low cost
* Ideal for static websites

---

# 3.9 Application Load Balancer

ALB distributes traffic across multiple EC2 instances.

Architecture:

```text
CloudFront → ALB → EC2 Instances
```

Benefits:

* High availability
* Automatic load balancing
* Scalable infrastructure

---

# 3.10 EC2 Instances (Application Servers)

EC2 instances host the application backend.

Example:

```text
Web Server
Application Server
Microservices
```

These servers process dynamic requests.

---

# 3.11 API Gateway and Lambda

Serverless APIs can be served through API Gateway.

Architecture:

```text
CloudFront → API Gateway → Lambda
```

Use cases:

* Mobile applications
* Serverless APIs
* SaaS platforms

---

# 3.12 Database Layer

Application servers connect to databases such as:

```text
Amazon RDS
Amazon Aurora
DynamoDB
```

Example architecture:

```text
EC2 → RDS Database
```

This layer stores:

* User data
* Transactions
* Application state

---

# 4. Real Production Request Flow

Example user request:

```text
https://www.example.com/index.html
```

Complete flow:

```text
User
 │
 ▼
Route 53 DNS
 │
 ▼
AWS WAF
 │
 ▼
CloudFront Edge Location
 │
 ▼
Cache Check
 │
 ├── Cache Hit → Serve Content
 │
 └── Cache Miss
        │
        ▼
     Origin Server
        │
        ▼
Content Returned
        │
        ▼
Cached at Edge Location
        │
        ▼
Delivered to User
```

---

# 5. Benefits of This Architecture

### Global Performance

Content delivered from nearest edge location.

---

### High Availability

Multiple edge locations ensure reliability.

---

### Scalability

CloudFront automatically scales to handle millions of requests.

---

### Security

Integration with:

* AWS WAF
* AWS Shield
* HTTPS encryption

---

### Cost Optimization

Caching reduces origin server load and bandwidth costs.

---

# 6. Example Enterprise Architecture

Large production systems often look like:

```text
Users Worldwide
      │
      ▼
Route 53 DNS
      │
      ▼
AWS WAF
      │
      ▼
CloudFront CDN
      │
 ┌────┼───────────────┐
 │    │               │
 ▼    ▼               ▼
S3   ALB            API Gateway
 │    │               │
 ▼    ▼               ▼
Static EC2           Lambda
Content Servers
 │
 ▼
Database (RDS / DynamoDB)
```

---

# 7. Where This Architecture Is Used

This type of architecture is used by:

* Streaming platforms
* E-commerce websites
* SaaS platforms
* Global web applications
* Media delivery systems

---
---
# 1. Introduction to Amazon CloudFront
---
## 1.1 What is Amazon CloudFront

**Amazon CloudFront** is a **Content Delivery Network (CDN)** service provided by AWS that securely delivers data, videos, applications, and APIs to users with **low latency and high transfer speeds**.

CloudFront achieves this by using a **global network of edge locations** that cache copies of content closer to end users.

Instead of sending every request to the origin server, CloudFront serves cached content from the **nearest edge location**, improving performance and reducing server load.

---

## 1.2 Why Amazon CloudFront is Required

Modern web applications serve users from different regions around the world. If content is delivered from a single server location, users who are far away from that server will experience:

* High latency
* Slow website loading
* Increased network congestion
* Poor user experience

CloudFront solves this problem by distributing content across multiple global edge locations.

When a user requests content, the request is routed to the **closest edge location**, ensuring faster delivery.

---

## 1.3 Key Benefits of CloudFront

### 1. Faster Content Delivery

CloudFront caches content at edge locations near users, reducing the distance data must travel.

### 2. Low Latency

Content is delivered through the **AWS global network infrastructure**, providing faster response times.

### 3. Improved Security

CloudFront integrates with several AWS security services such as:

* AWS Web Application Firewall (WAF)
* AWS Shield for DDoS protection
* SSL/TLS encryption
* Signed URLs and signed cookies

### 4. High Scalability

CloudFront automatically scales to handle **millions of requests per second** without manual intervention.

### 5. Cost Optimization

By caching content at edge locations, CloudFront reduces the number of requests sent to the origin server, lowering bandwidth and infrastructure costs.

---

## 1.4 How CloudFront Works (Basic Idea)

Without CDN:

```
User → Origin Server → Response
```

With CloudFront:

```
User → Edge Location (Cache)

If cache hit:
    Content served directly

If cache miss:
    Request forwarded to origin server
    Response cached at edge location
```

---

## 1.5 Types of Content Delivered by CloudFront

CloudFront can deliver both **static and dynamic content**.

### Static Content

Static files that do not change frequently.

Examples:

* Images
* HTML files
* CSS
* JavaScript

Common origin:

* Amazon S3

---

### Dynamic Content

Content generated in real time.

Examples:

* Web applications
* REST APIs
* Authentication services

Common origins:

* EC2 instances
* Application Load Balancer
* API Gateway

---

### Media Streaming

CloudFront can also deliver media content efficiently.

Examples:

* Video streaming
* Live streaming
* Audio content

---

## 1.6 Example Request Flow

```
User (India)
     │
     ▼
Nearest Edge Location
     │
     ▼
Cache Check
     │
 ┌───┴────┐
 │        │
Cache Hit Cache Miss
 │        │
 ▼        ▼
Content   Fetch from Origin (S3 / EC2 / ALB)
Served
```

---

## 1.7 Real-World Example

When a user opens a website such as:

```
https://example.com/image.png
```

The request flow typically looks like:

```
User
 │
 ▼
Route 53 DNS
 │
 ▼
CloudFront Distribution
 │
 ▼
Origin Server
 ├── Amazon S3
 ├── Application Load Balancer
 └── API Gateway
```

---

## 1.8 Real Companies Using CDN

Large companies rely on CDN services like CloudFront to deliver content globally.

Examples include:

* Netflix
* Amazon
* Spotify
* Airbnb
* Adobe

These companies use CDN technology to ensure their applications remain **fast, reliable, and scalable** worldwide.

---
---
# 2. Content Delivery Network (CDN) Explained
---

## 2.1 What is a Content Delivery Network (CDN)

A **Content Delivery Network (CDN)** is a distributed network of servers located in multiple geographic locations that work together to deliver web content to users quickly and efficiently.

Instead of serving content from a single central server, a CDN caches copies of content on servers located closer to users. When a user requests content, it is delivered from the **nearest server**, reducing latency and improving performance.

CDNs are widely used for delivering:

* Websites
* Images
* Videos
* JavaScript files
* CSS files
* APIs
* Streaming media

In AWS, the CDN service is **Amazon CloudFront**.

---

## 2.2 Why CDN is Important

Without a CDN, all users must access content from a **single origin server**.

If the server is located far from the user, several problems can occur:

* High latency
* Slow page load times
* Network congestion
* Increased load on the origin server
* Poor user experience

A CDN solves these issues by **placing cached copies of content closer to users**.

---

## 2.3 Traditional Web Hosting vs CDN

### Traditional Web Hosting

In traditional hosting, all requests go directly to the origin server.

```
User → Internet → Origin Server → Response
```

Problems:

* High latency for distant users
* Server overload
* Slow content delivery

---

### With CDN

In a CDN architecture, content is cached at edge servers.

```
User → Nearest Edge Server → Response
                    │
                    └── If cache miss → Origin Server
```

Benefits:

* Faster delivery
* Reduced latency
* Lower server load

---

## 2.4 How CDN Works

The CDN process typically works in the following steps:

### Step 1 – User Request

A user requests a file such as a webpage or image.

Example:

```
https://example.com/logo.png
```

---

### Step 2 – DNS Resolution

The DNS system routes the request to the **nearest CDN edge location**.

---

### Step 3 – Cache Check

The CDN server checks whether the requested content is already stored in its cache.

```
Edge Server
   │
   ▼
Cache Check
```

---

### Step 4 – Cache Hit

If the content exists in the cache:

```
Edge Server → User
```

The file is delivered immediately.

---

### Step 5 – Cache Miss

If the content is not cached:

```
Edge Server → Origin Server
```

The CDN retrieves the content from the origin server.

---

### Step 6 – Content Caching

After retrieving the content, the CDN stores it in the cache for future requests.

```
Origin Server → Edge Server → Cached
```

---

### Step 7 – Content Delivery

The cached content is delivered to the user.

Future users requesting the same content will receive it directly from the CDN cache.

---

## 2.5 Components of a CDN

A CDN architecture typically includes the following components.

### 1. Origin Server

The **origin server** is the primary location where the original content is stored.

Examples:

* Web server
* Storage server
* Application server

In AWS, common origins include:

* Amazon S3
* EC2 instances
* Application Load Balancer
* API Gateway

---

### 2. Edge Servers

Edge servers are CDN servers located close to users.

They store cached copies of content and deliver them to users.

Functions of edge servers:

* Cache content
* Serve requests quickly
* Reduce origin server load

---

### 3. Cache

Cache is the temporary storage used by CDN servers to store frequently accessed content.

Advantages of caching:

* Faster response time
* Reduced bandwidth usage
* Lower origin server load

---

### 4. DNS Routing

DNS directs users to the **closest CDN edge location** based on their geographic location.

---

## 2.6 CDN Caching Mechanism

The caching mechanism determines how long content stays in the cache.

Important caching concepts:

### TTL (Time to Live)

TTL defines how long content remains cached before it must be refreshed from the origin server.

Example:

```
TTL = 1 hour
```

After one hour, the CDN fetches the updated content from the origin server.

---

### Cache Hit

A **cache hit** occurs when the requested content is found in the CDN cache.

```
User → CDN Cache → Content Delivered
```

This provides the fastest response.

---

### Cache Miss

A **cache miss** occurs when the content is not available in the cache.

```
User → CDN → Origin Server
```

The CDN retrieves the content from the origin and caches it.

---

## 2.7 CDN Performance Benefits

Using a CDN provides several performance improvements.

### Reduced Latency

Content is delivered from nearby servers, reducing network travel distance.

---

### Faster Page Load Times

Static assets like images and scripts are delivered quickly.

---

### Reduced Bandwidth Usage

Because cached content is served by edge servers, fewer requests reach the origin server.

---

### High Availability

If one server fails, other CDN nodes can serve the content.

---

## 2.8 Real-World CDN Use Cases

CDNs are used in many real-world applications.

### Video Streaming Platforms

Examples:

* Netflix
* YouTube
* Amazon Prime Video

CDNs distribute video content globally.

---

### E-Commerce Websites

Examples:

* Amazon
* Flipkart
* Shopify stores

CDNs improve product page loading speed.

---

### News Websites

Examples:

* BBC
* CNN
* TechCrunch

CDNs help handle large traffic spikes.

---

### SaaS Applications

Examples:

* Slack
* Zoom
* Dropbox

CDNs improve application performance worldwide.

---

## 2.9 CDN Example Architecture

```
Users Worldwide
      │
      ▼
DNS System
      │
      ▼
CDN Network
 ├── Edge Server (Asia)
 ├── Edge Server (Europe)
 └── Edge Server (USA)
      │
      ▼
Origin Server
```

---

## 2.10 CDN vs Cloud Hosting

| Feature     | CDN                     | Cloud Hosting       |
| ----------- | ----------------------- | ------------------- |
| Purpose     | Content delivery        | Application hosting |
| Location    | Multiple global servers | Single region       |
| Performance | Very fast delivery      | Depends on region   |
| Use case    | Static content          | Applications        |

---
---
# 3. How Amazon CloudFront Works (Step-by-Step Request Flow)
---

## 3.1 Overview

Amazon CloudFront works by delivering content from **edge locations** that are geographically closer to users.
When a user requests a file (such as an image, webpage, or video), CloudFront routes the request through its global network and serves the content from the **nearest edge location**.

If the content is not already cached, CloudFront retrieves it from the **origin server**, stores it in the cache, and delivers it to the user.

---

## 3.2 Basic CloudFront Request Flow

```text
User Request
     │
     ▼
DNS Resolution
     │
     ▼
Nearest CloudFront Edge Location
     │
     ▼
Cache Check
     │
 ┌───┴─────┐
 │         │
Cache Hit  Cache Miss
 │         │
 ▼         ▼
Serve      Request Sent to Origin
Content
           │
           ▼
       Origin Server
           │
           ▼
Content Returned and Cached
           │
           ▼
Response Sent to User
```

---

## 3.3 Step-by-Step CloudFront Workflow

### Step 1 – User Requests Content

A user enters a URL in the browser.

Example:

```text
https://example.com/index.html
```

The browser sends a request to the domain name.

---

### Step 2 – DNS Resolution

The DNS system resolves the domain name and directs the request to the **CloudFront distribution**.

DNS services like **Amazon Route 53** often manage this process.

```text
User → DNS → CloudFront Distribution
```

---

### Step 3 – Request Routed to Nearest Edge Location

CloudFront determines the **closest edge location** to the user based on network latency and geographic location.

```text
User → Closest Edge Location
```

Example:

* User in India → Mumbai edge location
* User in Europe → Frankfurt edge location

---

### Step 4 – Cache Lookup

The edge location checks whether the requested content is already stored in its cache.

```text
Edge Location
      │
      ▼
Cache Lookup
```

---

### Step 5 – Cache Hit

If the requested content is already cached:

```text
Edge Location → User
```

The edge server immediately delivers the content to the user.

Advantages:

* Faster response time
* Reduced load on origin server

---

### Step 6 – Cache Miss

If the content is not present in the cache:

```text
Edge Location → Origin Server
```

CloudFront forwards the request to the origin server.

---

## 3.4 Origin Servers in CloudFront

The origin server is where the **original content is stored**.

Common origins include:

* Amazon S3
* EC2 instances
* Application Load Balancer
* API Gateway
* On-premise web servers

Example architecture:

```text
User
 │
 ▼
CloudFront Edge Location
 │
 ▼
Origin Server
 ├── Amazon S3
 ├── EC2 Web Server
 └── Application Load Balancer
```

---

## 3.5 Content Retrieval from Origin

When a cache miss occurs, CloudFront sends a request to the origin server.

```text
Edge Location → Origin Server → Content Returned
```

The origin server sends the requested file back to the edge location.

---

## 3.6 Content Caching

After receiving the content from the origin server, CloudFront stores it in the edge location cache.

```text
Origin Server → Edge Location → Cached Content
```

This ensures that future requests for the same content are served directly from the edge location.

---

## 3.7 Response Delivery

Once the content is cached, CloudFront delivers it to the user.

```text
Edge Location → User
```

The user receives the content quickly because it is served from the nearest server.

---

## 3.8 Subsequent Requests

When another user requests the same file:

```text
New User → Edge Location → Cached Content
```

The content is delivered immediately without contacting the origin server.

---

## 3.9 CloudFront Cache Expiration

Cached content is stored for a specific period known as **TTL (Time to Live)**.

Example:

```text
TTL = 24 hours
```

After TTL expires:

* CloudFront checks the origin server for updated content.

---

## 3.10 Complete CloudFront Architecture Flow

```text
User
 │
 ▼
DNS (Route 53)
 │
 ▼
CloudFront Distribution
 │
 ▼
Edge Location
 │
 ▼
Cache Check
 │
 ├── Cache Hit → Serve Content
 │
 └── Cache Miss
        │
        ▼
   Origin Server
   ├── S3 Bucket
   ├── EC2 Instance
   └── Load Balancer
        │
        ▼
Content Returned
        │
        ▼
Cached at Edge Location
        │
        ▼
Response Sent to User
```

---

## 3.11 Key Features in the CloudFront Request Lifecycle

### Edge Locations

These are geographically distributed servers that cache and deliver content.

---

### Cache Behavior

Cache behavior determines how CloudFront processes requests based on:

* URL path patterns
* HTTP methods
* headers
* cookies
* query strings

---

### Origin Communication

CloudFront communicates with the origin server only when necessary, such as during cache misses or cache refresh.

---

## 3.12 Advantages of the CloudFront Workflow

Using CloudFront improves application performance in several ways:

* Reduced latency
* Faster page load times
* Reduced origin server load
* Global content delivery
* Improved scalability

---
---
# 4. CloudFront Global Infrastructure
---

## 4.1 Overview

The global infrastructure of **Amazon CloudFront** is designed to deliver content to users with **low latency and high availability**.

CloudFront uses a worldwide network of servers that are strategically placed in different geographic regions. These servers cache content closer to users and deliver it quickly.

The main components of the CloudFront global infrastructure include:

* Edge Locations
* Regional Edge Caches
* Origin Servers
* AWS Global Network

These components work together to optimize content delivery and reduce latency.

---

## 4.2 Edge Locations

**Edge locations** are data centers where CloudFront caches copies of content.
They are the primary points where users interact with the CloudFront network.

When a user requests content, CloudFront routes the request to the **nearest edge location**.

### Key characteristics of Edge Locations

* Located in cities worldwide
* Cache frequently accessed content
* Deliver content to users with minimal latency
* Reduce load on origin servers

### Example

If a user in India requests a webpage:

```text
User (India)
     │
     ▼
Nearest Edge Location (Mumbai / Delhi / Singapore)
     │
     ▼
Content Delivered
```

Because the content is delivered from a nearby location, response time is significantly reduced.

---

## 4.3 Regional Edge Caches

Regional Edge Caches are a second layer of caching between edge locations and origin servers.

They help improve cache efficiency by storing larger and less frequently accessed objects.

### Benefits of Regional Edge Caches

* Reduce requests to origin servers
* Increase cache hit ratio
* Improve performance for less frequently accessed content

### Request Flow with Regional Edge Cache

```text
User
 │
 ▼
Edge Location
 │
 ▼
Regional Edge Cache
 │
 ▼
Origin Server
```

If content is not available in the edge location, CloudFront checks the **regional edge cache** before contacting the origin server.

---

## 4.4 Origin Servers

The **origin server** is the location where the original content is stored.

CloudFront retrieves content from the origin server when the requested object is not available in the cache.

Common origin servers used with CloudFront include:

* Amazon S3
* Amazon EC2
* Application Load Balancer
* API Gateway
* On-premise servers

### Example Architecture

```text
Users
 │
 ▼
CloudFront Edge Location
 │
 ▼
Origin Server
 ├── Amazon S3 (Static files)
 ├── EC2 (Web application)
 └── Load Balancer
```

---

## 4.5 AWS Global Network

CloudFront uses the **AWS global network infrastructure** to deliver content.

This network consists of high-speed connections between AWS regions and edge locations.

Advantages of the AWS global network:

* Reduced network congestion
* Faster data transfer
* More reliable connectivity
* Lower latency

Instead of traveling through multiple public internet routes, data is transferred through the optimized AWS network.

---

## 4.6 Edge Location vs Regional Edge Cache

| Feature          | Edge Location               | Regional Edge Cache              |
| ---------------- | --------------------------- | -------------------------------- |
| Location         | Closest to users            | Between edge and origin          |
| Purpose          | Deliver cached content      | Improve caching efficiency       |
| Size             | Smaller cache               | Larger cache                     |
| Access frequency | Frequently accessed content | Less frequently accessed content |

---

## 4.7 Example Global Delivery Architecture

```text
Users Worldwide
      │
      ▼
DNS (Route 53)
      │
      ▼
CloudFront Network
      │
 ┌────┼─────────────┐
 │    │             │
 ▼    ▼             ▼
Edge  Edge         Edge
Location Location  Location
 │
 ▼
Regional Edge Cache
 │
 ▼
Origin Server
 ├── S3
 ├── EC2
 └── Load Balancer
```

---

## 4.8 Advantages of CloudFront Global Infrastructure

### Low Latency

Content is delivered from locations closer to users.

### High Availability

Multiple edge locations ensure continuous service even if one location fails.

### Scalability

CloudFront can handle large volumes of traffic without manual scaling.

### Reduced Origin Load

Edge caching reduces the number of requests sent to the origin server.

---

## 4.9 Global Coverage

CloudFront has hundreds of edge locations distributed worldwide, including:

* North America
* Europe
* Asia
* South America
* Africa
* Australia

This global presence ensures users receive content quickly regardless of their location.

---
---
# 5. CloudFront Core Components
---

## 5.1 Overview

Amazon CloudFront is built using several core components that work together to deliver content efficiently across the global network.

The main components of CloudFront include:

* Distribution
* Origins
* Cache Behavior
* Cache Keys
* TTL (Time To Live)
* Edge Locations

Understanding these components is essential for designing and configuring CloudFront distributions.

---

# 5.2 CloudFront Distribution

A **CloudFront Distribution** is the main configuration unit in CloudFront that defines how content is delivered to users.

When you create a distribution, you configure:

* The origin server
* Cache behavior
* Security settings
* SSL certificates
* Domain names
* Content delivery settings

Once a distribution is created, CloudFront provides a unique domain name.

Example:

```
d123abcd.cloudfront.net
```

You can also attach a custom domain such as:

```
cdn.example.com
```

### Distribution Request Flow

```
User
 │
 ▼
CloudFront Distribution
 │
 ▼
Edge Location
 │
 ▼
Origin Server
```

---

# 5.3 Origin

An **Origin** is the location where the original content is stored.

When CloudFront cannot find requested content in the cache, it retrieves the content from the origin server.

Common origin types include:

### Amazon S3

Used for hosting static content.

Examples:

* Images
* HTML files
* CSS
* JavaScript

Example architecture:

```
User → CloudFront → S3 Bucket
```

---

### EC2 Instance

Used for hosting web applications or APIs.

Example:

```
User → CloudFront → EC2 Web Server
```

---

### Application Load Balancer

Used for scalable web applications.

Example:

```
User → CloudFront → ALB → EC2 Instances
```

---

### API Gateway

Used for serverless APIs.

Example:

```
User → CloudFront → API Gateway → Lambda
```

---

# 5.4 Cache Behavior

Cache behavior defines how CloudFront handles requests for different types of content.

It allows you to control request processing based on **path patterns**.

Example configuration:

| Path Pattern | Origin       |
| ------------ | ------------ |
| `/images/*`  | S3 bucket    |
| `/api/*`     | API Gateway  |
| `/videos/*`  | Media server |

### Example Routing

```
User Request → /images/logo.png
                 │
                 ▼
           Routed to S3 Origin
```

```
User Request → /api/user
                 │
                 ▼
           Routed to API Gateway
```

Cache behaviors also control:

* HTTP methods
* Cookies
* Query strings
* Header forwarding
* Cache policies

---

# 5.5 Cache Keys

A **Cache Key** determines how CloudFront identifies cached objects.

CloudFront uses cache keys to decide whether it can serve cached content or must retrieve it from the origin server.

A cache key can include:

* URL path
* HTTP headers
* Cookies
* Query strings

### Example

Request 1:

```
example.com/product?id=10
```

Request 2:

```
example.com/product?id=20
```

If query strings are included in the cache key:

```
Two separate cache entries will be created
```

If query strings are ignored:

```
Both requests use the same cached content
```

---

# 5.6 TTL (Time To Live)

TTL defines how long CloudFront keeps content in the cache before checking with the origin server for updates.

TTL values include:

* Minimum TTL
* Default TTL
* Maximum TTL

### Example

```
Default TTL = 1 hour
```

This means content stays cached for 1 hour before CloudFront checks the origin server again.

---

### TTL Workflow

```
User Request
     │
     ▼
Edge Location Cache
     │
     ▼
TTL Check
     │
 ┌───┴────┐
 │        │
Valid     Expired
 │        │
 ▼        ▼
Serve     Fetch Updated Content
Cache     From Origin
```

---

# 5.7 Edge Locations

Edge locations are the global data centers where CloudFront caches content.

Functions of edge locations:

* Store cached content
* Deliver content to users
* Reduce latency
* Reduce origin server load

Example flow:

```
User
 │
 ▼
Nearest Edge Location
 │
 ▼
Cached Content Delivered
```

---

# 5.8 Combined CloudFront Architecture

All core components work together as follows:

```
User
 │
 ▼
DNS (Route 53)
 │
 ▼
CloudFront Distribution
 │
 ▼
Edge Location
 │
 ▼
Cache Behavior
 │
 ▼
Origin Server
 ├── S3
 ├── EC2
 └── API Gateway
```

---

# 5.9 Importance of CloudFront Components

Understanding these components helps in:

* Designing scalable architectures
* Optimizing caching strategies
* Improving website performance
* Reducing infrastructure cost
* Enhancing security

---
---
# 6. CloudFront Distribution Types
---

## 6.1 Overview

A **CloudFront Distribution** defines how CloudFront delivers content to users.
When you create a distribution, you configure the **origin, caching behavior, security settings, and content delivery rules**.

Historically, CloudFront supported two distribution types:

* Web Distribution
* RTMP Distribution (Legacy)

Today, most implementations use **Web Distribution**, which supports both **static and dynamic content delivery**.

---

# 6.2 Web Distribution

A **Web Distribution** is used to deliver content over **HTTP and HTTPS protocols**.

This is the most commonly used distribution type in CloudFront and supports:

* Static content
* Dynamic content
* APIs
* Video streaming
* Web applications

---

## 6.2.1 Static Content Delivery

Static content does not change frequently and can be cached easily.

Examples of static content:

* HTML pages
* Images
* CSS files
* JavaScript files
* PDF documents

Typical architecture:

```text
User
 │
 ▼
CloudFront
 │
 ▼
Amazon S3 (Static Website)
```

Advantages:

* Faster page loading
* Reduced server load
* Improved global performance

---

## 6.2.2 Dynamic Content Delivery

Dynamic content is generated by the server in real time.

Examples:

* User dashboards
* Login pages
* API responses
* Personalized content

Architecture example:

```text
User
 │
 ▼
CloudFront
 │
 ▼
Application Load Balancer
 │
 ▼
EC2 Instances
```

CloudFront can still improve performance for dynamic content by:

* Optimizing network paths
* Using persistent connections
* Reducing latency

---

## 6.2.3 API Delivery

CloudFront is commonly used to accelerate APIs.

Example architecture:

```text
User
 │
 ▼
CloudFront
 │
 ▼
API Gateway
 │
 ▼
AWS Lambda
```

Benefits:

* Faster API response
* Global API distribution
* Improved scalability

---

## 6.2.4 Media Streaming

CloudFront can deliver streaming media such as:

* Video
* Audio
* Live streaming

Streaming protocols supported include:

* HLS (HTTP Live Streaming)
* MPEG-DASH

Example architecture:

```text
User
 │
 ▼
CloudFront
 │
 ▼
Media Server / S3
```

This allows efficient delivery of media files worldwide.

---

# 6.3 RTMP Distribution (Legacy)

RTMP (Real-Time Messaging Protocol) distributions were previously used for **streaming media content** through Adobe Flash.

Typical architecture:

```text
User
 │
 ▼
Flash Media Player
 │
 ▼
CloudFront RTMP Distribution
 │
 ▼
Origin Media Server
```

However, RTMP distributions are now **deprecated** because Flash technology is no longer widely supported.

Modern streaming uses **HTTP-based streaming protocols** such as:

* HLS
* DASH

---

# 6.4 Modern CloudFront Distribution Model

Today, almost all CloudFront implementations use **Web Distributions** for every type of content.

Example modern architecture:

```text
Users
 │
 ▼
CloudFront Distribution
 │
 ├── Static Content → S3
 │
 ├── Web Application → ALB → EC2
 │
 └── API Requests → API Gateway → Lambda
```

This architecture allows CloudFront to handle:

* Static assets
* Dynamic web applications
* APIs
* Streaming content

---

# 6.5 Benefits of Using CloudFront Distributions

### Global Performance

Content is delivered from the closest edge location.

---

### High Availability

CloudFront automatically routes traffic through multiple edge locations.

---

### Security

CloudFront distributions support:

* HTTPS encryption
* AWS WAF integration
* DDoS protection using AWS Shield
* Signed URLs and cookies

---

### Scalability

CloudFront can scale automatically to handle millions of user requests.

---

# 6.6 Distribution Domain Names

When a distribution is created, CloudFront provides a default domain name.

Example:

```text
d123abcd.cloudfront.net
```

You can also configure a **custom domain name**.

Example:

```text
cdn.example.com
```

This is done using:

* DNS configuration
* SSL certificates
* AWS Certificate Manager (ACM)

---

# 6.7 Example CloudFront Distribution Architecture

```text
User
 │
 ▼
DNS (Route 53)
 │
 ▼
CloudFront Distribution
 │
 ├── /images/* → S3 Bucket
 │
 ├── /app/* → Application Load Balancer
 │
 └── /api/* → API Gateway
```

This allows CloudFront to route requests to different backend services.

---

# 6.8 When to Use CloudFront Distribution

You should use CloudFront when:

* Delivering content globally
* Hosting static websites
* Accelerating APIs
* Streaming media content
* Protecting applications with AWS WAF

---
---
# 7. Origins in Amazon CloudFront
---

## 7.1 Overview

In **Amazon CloudFront**, an **Origin** is the location where the original version of the content is stored.

When CloudFront receives a request from a user, it first checks whether the content exists in the **edge location cache**.
If the content is not available in the cache (**cache miss**), CloudFront retrieves the content from the **origin server**.

The origin can be an AWS service or a custom web server.

---

# 7.2 How Origins Work in CloudFront

Basic workflow:

```text
User Request
     │
     ▼
CloudFront Edge Location
     │
     ▼
Cache Check
     │
 ┌───┴─────┐
 │         │
Cache Hit  Cache Miss
 │         │
 ▼         ▼
Serve      Request Sent to Origin
Content
           │
           ▼
       Origin Server
           │
           ▼
Response Cached at Edge Location
           │
           ▼
Response Sent to User
```

---

# 7.3 Types of Origins Supported in CloudFront

CloudFront supports multiple origin types.

### 1. Amazon S3 Origin

### 2. EC2 Instance Origin

### 3. Application Load Balancer Origin

### 4. API Gateway Origin

### 5. Custom Origin (External Server)

---

# 7.4 Amazon S3 Origin

Amazon S3 is one of the most common origins used with CloudFront.

It is ideal for delivering **static content** such as:

* Images
* HTML files
* CSS files
* JavaScript
* Downloadable files

Example architecture:

```text
User
 │
 ▼
CloudFront
 │
 ▼
S3 Bucket
```

Advantages:

* Highly scalable storage
* Low cost
* Easy integration with CloudFront
* Ideal for static websites

---

# 7.5 EC2 Instance Origin

CloudFront can use an **EC2 instance** as the origin server.

This is commonly used when hosting dynamic web applications.

Example architecture:

```text
User
 │
 ▼
CloudFront
 │
 ▼
EC2 Web Server
```

Use cases:

* Web applications
* Backend services
* Custom server applications

---

# 7.6 Application Load Balancer Origin

In large-scale architectures, CloudFront is often connected to an **Application Load Balancer (ALB)**.

The ALB distributes traffic to multiple EC2 instances.

Example architecture:

```text
User
 │
 ▼
CloudFront
 │
 ▼
Application Load Balancer
 │
 ▼
EC2 Instances
```

Advantages:

* High availability
* Automatic load balancing
* Scalability

---

# 7.7 API Gateway Origin

CloudFront can also deliver **API requests** by using **API Gateway** as the origin.

Example architecture:

```text
User
 │
 ▼
CloudFront
 │
 ▼
API Gateway
 │
 ▼
Lambda Function
```

Benefits:

* Faster API responses
* Global API delivery
* Improved performance for serverless applications

---

# 7.8 Custom Origins

A **custom origin** is any web server that is not an AWS service.

Examples:

* On-premise web server
* Third-party hosting provider
* External HTTP server

Example architecture:

```text
User
 │
 ▼
CloudFront
 │
 ▼
Custom Web Server
```

CloudFront communicates with custom origins using:

* HTTP
* HTTPS

---

# 7.9 Origin Groups (Failover Origins)

CloudFront supports **origin groups**, which provide failover between multiple origins.

If the primary origin fails, CloudFront automatically switches to the **secondary origin**.

Example architecture:

```text
User
 │
 ▼
CloudFront
 │
 ▼
Primary Origin (S3)
 │
 └── If Failure
       │
       ▼
Secondary Origin (Backup Server)
```

Advantages:

* High availability
* Disaster recovery
* Improved reliability

---

# 7.10 Origin Settings

When configuring an origin in CloudFront, several settings can be defined.

### Origin Domain Name

Specifies the domain name of the origin server.

Example:

```text
mybucket.s3.amazonaws.com
```

---

### Origin Protocol Policy

Defines how CloudFront communicates with the origin.

Options include:

* HTTP only
* HTTPS only
* Match viewer

---

### Origin Path

Defines a specific directory in the origin where content is stored.

Example:

```text
/images
```

CloudFront will fetch content from that path.

---

### Origin Timeout Settings

Defines how long CloudFront waits for the origin to respond.

Settings include:

* Connection timeout
* Response timeout

---

# 7.11 Example CloudFront Origin Architecture

```text
Users
 │
 ▼
CloudFront Distribution
 │
 ├── Static Content → S3 Bucket
 │
 ├── Web Application → ALB → EC2 Instances
 │
 └── API Requests → API Gateway → Lambda
```

This architecture is commonly used in **modern cloud applications**.

---

# 7.12 Best Practices for Origins

### Use S3 for Static Content

S3 is the best option for hosting static files.

---

### Use Load Balancers for Dynamic Applications

Application Load Balancer helps distribute traffic across multiple servers.

---

### Enable HTTPS

Always use HTTPS communication between CloudFront and the origin server.

---

### Configure Origin Failover

Use origin groups to ensure high availability.

---

# 7.13 Advantages of Using Origins with CloudFront

* Improved performance
* Reduced origin server load
* Global content delivery
* Better scalability
* Higher availability

---
---
# 8. CloudFront Cache
---

## 8.1 Overview

Caching is one of the most important features of **Amazon CloudFront**.
CloudFront stores copies of content in **edge locations** so that future user requests can be served quickly without contacting the origin server.

This process reduces:

* Latency
* Network traffic
* Load on the origin server

Caching significantly improves **website performance and scalability**.

---

# 8.2 What is CloudFront Caching

**Caching** is the process of storing frequently accessed content temporarily at edge locations.

When a user requests content:

1. CloudFront checks the edge cache.
2. If content is found → it is delivered immediately.
3. If not found → CloudFront retrieves it from the origin server.

Example:

```text
User
 │
 ▼
Edge Location
 │
 ▼
Cache Check
```

---

# 8.3 Cache Hit

A **Cache Hit** occurs when the requested content is already stored in the edge location cache.

Example flow:

```text
User Request
     │
     ▼
Edge Location Cache
     │
     ▼
Content Found
     │
     ▼
Content Delivered to User
```

Advantages:

* Faster response time
* Reduced origin server load
* Lower bandwidth usage

---

# 8.4 Cache Miss

A **Cache Miss** occurs when the requested content is not present in the cache.

Example flow:

```text
User Request
     │
     ▼
Edge Location
     │
     ▼
Content Not Found
     │
     ▼
Request Sent to Origin
     │
     ▼
Origin Server Response
     │
     ▼
Content Cached at Edge Location
     │
     ▼
Delivered to User
```

Future requests will result in a **cache hit**.

---

# 8.5 Cache Expiration (TTL)

TTL (Time To Live) defines how long content remains in the cache before CloudFront checks for updates.

Types of TTL:

### Minimum TTL

The shortest time CloudFront keeps content in cache.

---

### Default TTL

The default caching duration when no cache-control headers are present.

Example:

```text
Default TTL = 3600 seconds (1 hour)
```

---

### Maximum TTL

The longest time content can stay in the cache.

---

# 8.6 Cache Control Headers

Origin servers can control caching behavior using HTTP headers.

Common cache headers include:

### Cache-Control

Example:

```text
Cache-Control: max-age=3600
```

This tells CloudFront to cache the object for **1 hour**.

---

### Expires Header

Defines the expiration date of cached content.

Example:

```text
Expires: Wed, 10 Jun 2026 10:00:00 GMT
```

---

# 8.7 Cache Key

A **Cache Key** determines how CloudFront identifies unique cached objects.

The cache key can include:

* URL path
* Query strings
* HTTP headers
* Cookies

Example request:

```text
example.com/product?id=101
```

If query strings are included in cache keys:

```text
example.com/product?id=102
```

These will be stored as **separate cache entries**.

---

# 8.8 Cache Policies

Cache policies define how CloudFront caches content.

Cache policies control:

* Headers included in cache keys
* Cookies included in cache keys
* Query strings included in cache keys
* TTL settings

CloudFront provides:

### Managed Cache Policies

Predefined policies provided by AWS.

Example:

* CachingOptimized
* CachingDisabled

---

### Custom Cache Policies

Users can create custom caching rules depending on application requirements.

---

# 8.9 Cache Invalidation

Sometimes cached content must be removed before the TTL expires.

This process is called **cache invalidation**.

Example:

```text
/images/logo.png
```

If the image is updated, you can invalidate the cached version.

Invalidation request example:

```text
/images/*
```

This removes all cached objects under the `/images` directory.

---

# 8.10 Cache Behavior Example

Example architecture:

```text
User
 │
 ▼
CloudFront Edge Location
 │
 ▼
Cache Lookup
 │
 ├── Cache Hit → Content Delivered
 │
 └── Cache Miss
        │
        ▼
   Origin Server
        │
        ▼
Content Cached at Edge Location
        │
        ▼
Delivered to User
```

---

# 8.11 Benefits of CloudFront Caching

### Faster Content Delivery

Content is served directly from nearby edge locations.

---

### Reduced Origin Load

Fewer requests are sent to the origin server.

---

### Cost Reduction

Caching reduces bandwidth and compute costs.

---

### Better Scalability

Edge caching allows applications to handle large traffic spikes.

---

# 8.12 Cache Best Practices

### Cache Static Content

Cache static assets like images, CSS, and JavaScript for longer durations.

---

### Use Cache-Control Headers

Control caching behavior using HTTP headers.

---

### Optimize Cache Keys

Avoid unnecessary headers or cookies in cache keys to increase cache efficiency.

---

### Use Invalidation Carefully

Invalidation requests may incur additional cost.

---

# 8.13 Example CloudFront Caching Architecture

```text
Users
 │
 ▼
CloudFront Edge Locations
 │
 ▼
Cache Storage
 │
 ▼
Origin Server
 ├── Amazon S3
 ├── EC2
 └── Load Balancer
```

---

# 8.14 Cache Performance Metrics

Important caching metrics include:

* Cache Hit Ratio
* Origin Request Rate
* Latency
* Data Transfer

These metrics are monitored using **CloudWatch**.

---
---
# 9. CloudFront Behaviors
---

## 9.1 Overview

In **Amazon CloudFront**, a **Behavior (Cache Behavior)** defines how CloudFront handles requests for specific types of content.

Cache behaviors allow CloudFront to route requests to different **origin servers** based on **URL path patterns**.

This helps manage different types of content such as:

* Images
* Web applications
* APIs
* Videos

Each CloudFront distribution contains:

* **Default behavior** (mandatory)
* **Additional behaviors** (optional)

---

# 9.2 Default Cache Behavior

Every CloudFront distribution must have a **default cache behavior**.

The default behavior handles all requests that do not match any other path pattern.

Example:

```text
Default Behavior
Path Pattern: *
```

Request example:

```text
https://example.com/home
```

Since it does not match any specific rule, it is handled by the **default behavior**.

---

# 9.3 Path Pattern Routing

CloudFront uses **path patterns** to determine how requests are routed to origin servers.

Example configuration:

| Path Pattern | Origin                 |
| ------------ | ---------------------- |
| `/images/*`  | S3 Bucket              |
| `/videos/*`  | Media Server           |
| `/api/*`     | API Gateway            |
| `*`          | Web Application Server |

---

### Example Routing

Request:

```text
https://example.com/images/logo.png
```

Routing:

```text
User → CloudFront → S3 Origin
```

---

Request:

```text
https://example.com/api/user
```

Routing:

```text
User → CloudFront → API Gateway
```

---

# 9.4 HTTP Methods

CloudFront behaviors can define which HTTP methods are allowed.

Common HTTP methods include:

* GET
* HEAD
* OPTIONS
* POST
* PUT
* PATCH
* DELETE

Example configuration:

```text
Allowed HTTP Methods:
GET, HEAD, OPTIONS
```

These methods are typically used for **static content delivery**.

For APIs, additional methods may be enabled.

Example:

```text
GET, POST, PUT, DELETE
```

---

# 9.5 Header Forwarding

Headers are part of HTTP requests and may affect how content is delivered.

CloudFront behaviors can control which headers are forwarded to the origin server.

Examples of headers:

* Authorization
* User-Agent
* Host
* Accept-Language

Example configuration:

```text
Forward Headers:
Authorization
User-Agent
```

Forwarding headers allows the origin server to process requests differently based on header values.

---

# 9.6 Cookie Forwarding

Cookies are used to store user-specific information.

Examples:

* Session IDs
* Login tokens
* User preferences

CloudFront behaviors allow three cookie forwarding options.

### 1. None

No cookies are forwarded to the origin.

Example:

```text
Cookie Forwarding: None
```

Best for static websites.

---

### 2. Whitelist

Only specific cookies are forwarded.

Example:

```text
Forward Cookie: session_id
```

---

### 3. All Cookies

All cookies are forwarded to the origin server.

Example:

```text
Cookie Forwarding: All
```

This is commonly used for dynamic applications.

---

# 9.7 Query String Forwarding

Query strings are parameters added to URLs.

Example:

```text
https://example.com/products?id=100
```

Query string:

```text
id=100
```

CloudFront behaviors can control whether query strings are forwarded to the origin server.

Options include:

### None

Query strings are ignored.

Example:

```text
example.com/products?id=100
example.com/products?id=200
```

Both requests use the same cached object.

---

### Forward All

All query strings are forwarded to the origin server.

Example:

```text
example.com/products?id=100
example.com/products?id=200
```

These requests are treated as different cache entries.

---

### Whitelist Query Strings

Only specific query strings are forwarded.

Example:

```text
Allowed Query Strings: id
```

---

# 9.8 Behavior Priority

When multiple behaviors match a request, CloudFront selects the **most specific path pattern**.

Example configuration:

| Path Pattern         | Priority |
| -------------------- | -------- |
| `/images/*`          | High     |
| `/images/products/*` | Higher   |

Example request:

```text
/images/products/item1.jpg
```

Routing:

```text
CloudFront → /images/products/* behavior
```

Because it is more specific.

---

# 9.9 Behavior Architecture Example

```text
User Request
      │
      ▼
CloudFront Distribution
      │
      ▼
Behavior Rules
 ├── /images/* → S3 Bucket
 ├── /videos/* → Media Server
 ├── /api/* → API Gateway
 └── * → Web Application Server
```

This architecture helps deliver different types of content efficiently.

---

# 9.10 Best Practices for Cache Behaviors

### Use Specific Path Patterns

Define precise routing rules to optimize caching and performance.

---

### Limit Header and Cookie Forwarding

Forwarding unnecessary headers or cookies reduces cache efficiency.

---

### Optimize Query String Handling

Forward only required query strings to improve cache performance.

---

### Separate Static and Dynamic Content

Use different behaviors for static files and dynamic applications.

---

# 9.11 Advantages of Using CloudFront Behaviors

* Flexible request routing
* Better caching strategies
* Improved performance
* Reduced origin server load
* Efficient content delivery

---
---
# 10. CloudFront Security Features
---

## 10.1 Overview

Security is a critical aspect of **Amazon CloudFront**.
CloudFront provides multiple security mechanisms to protect applications, content, and users from threats such as:

* Unauthorized access
* Data interception
* DDoS attacks
* Web application attacks

CloudFront integrates with several AWS security services to provide **secure content delivery**.

Main security features include:

* HTTPS and SSL/TLS encryption
* Origin Access Control (OAC)
* Origin Access Identity (OAI)
* Signed URLs and Signed Cookies
* AWS WAF integration
* AWS Shield protection
* Field-level encryption

---

# 10.2 HTTPS Support

CloudFront supports secure content delivery using **HTTPS (Hypertext Transfer Protocol Secure)**.

HTTPS encrypts communication between:

* User → CloudFront
* CloudFront → Origin server

Example request:

```text
https://example.com/index.html
```

Benefits:

* Secure data transmission
* Protection against man-in-the-middle attacks
* Improved user trust

CloudFront supports modern TLS protocols such as:

* TLS 1.2
* TLS 1.3

---

# 10.3 SSL/TLS Certificates

To enable HTTPS, CloudFront requires an **SSL/TLS certificate**.

Certificates verify the identity of a domain and enable encrypted communication.

Two types of certificates can be used:

### Default CloudFront Certificate

CloudFront automatically provides a default certificate for its domain.

Example:

```text
d123abcd.cloudfront.net
```

---

### Custom SSL Certificate

You can attach a custom domain such as:

```text
cdn.example.com
```

To do this, you must use **AWS Certificate Manager (ACM)** to create or import a certificate.

Steps:

1. Request certificate in ACM
2. Validate domain ownership
3. Attach certificate to CloudFront distribution

---

# 10.4 Origin Access Identity (OAI)

**Origin Access Identity (OAI)** is used to restrict direct access to an S3 bucket.

Without OAI:

```text
User → S3 Bucket (Direct Access Possible)
```

With OAI:

```text
User → CloudFront → S3 Bucket
```

This ensures that content stored in the S3 bucket can only be accessed through CloudFront.

Benefits:

* Prevents direct access to S3
* Improves security of static content

---

# 10.5 Origin Access Control (OAC)

**Origin Access Control (OAC)** is a newer and more secure method than OAI.

OAC allows CloudFront to securely access the origin using **signed requests**.

Advantages of OAC:

* Better security
* Supports modern authentication methods
* Recommended by AWS for new deployments

Example workflow:

```text
User
 │
 ▼
CloudFront
 │
 ▼
Origin Access Control
 │
 ▼
S3 Bucket
```

---

# 10.6 Signed URLs

Signed URLs provide **temporary access to private content**.

They are commonly used when only authorized users should access specific files.

Example use cases:

* Paid video streaming
* Private downloads
* Subscription content

Example signed URL:

```text
https://example.com/video.mp4?Expires=123456789&Signature=xyz
```

Features:

* Expiration time
* Secure signature
* Access restrictions

---

# 10.7 Signed Cookies

Signed cookies allow access to multiple restricted files without generating multiple signed URLs.

Example use cases:

* Premium content websites
* Subscription video platforms

Example workflow:

```text
User Login
 │
 ▼
Application Generates Signed Cookie
 │
 ▼
User Browser Stores Cookie
 │
 ▼
CloudFront Validates Cookie
 │
 ▼
Access Granted
```

Benefits:

* Efficient access control
* Useful for multiple files

---

# 10.8 AWS WAF Integration

CloudFront integrates with **AWS Web Application Firewall (WAF)**.

AWS WAF protects web applications from common attacks.

Examples of attacks blocked by WAF:

* SQL Injection
* Cross-Site Scripting (XSS)
* Bot attacks
* IP-based attacks

Example architecture:

```text
User
 │
 ▼
AWS WAF
 │
 ▼
CloudFront
 │
 ▼
Origin Server
```

---

# 10.9 AWS Shield Protection

CloudFront automatically integrates with **AWS Shield** for DDoS protection.

Two versions of AWS Shield:

### AWS Shield Standard

Automatically enabled for all CloudFront distributions.

Protection against:

* Network layer attacks
* Transport layer attacks

---

### AWS Shield Advanced

Provides additional protection and monitoring for enterprise applications.

Features:

* Advanced DDoS detection
* Cost protection
* Detailed attack reports

---

# 10.10 Field-Level Encryption

Field-level encryption protects sensitive user data in HTTP requests.

Example sensitive data:

* Credit card numbers
* Personal identification numbers
* Sensitive user information

Example workflow:

```text
User Input
 │
 ▼
Encrypted at CloudFront
 │
 ▼
Origin Server Receives Encrypted Data
```

Only authorized applications can decrypt this information.

---

# 10.11 Geo Restriction (Geo Blocking)

CloudFront allows restricting content access based on geographic location.

Example:

Allow access only from:

* United States
* Canada
* Europe

Example configuration:

```text
Allowed Countries:
US
CA
DE
FR
```

Users from other countries will be blocked.

---

# 10.12 Example Secure CloudFront Architecture

```text
Users
 │
 ▼
AWS WAF
 │
 ▼
CloudFront Distribution
 │
 ▼
Origin Access Control
 │
 ▼
S3 / ALB / EC2
```

Security layers:

1. WAF protection
2. HTTPS encryption
3. Access control
4. Origin security

---

# 10.13 Best Practices for CloudFront Security

### Always Enable HTTPS

Use secure communication between users and CloudFront.

---

### Restrict Origin Access

Use **OAC or OAI** to prevent direct access to S3 buckets.

---

### Use AWS WAF

Protect applications from common web attacks.

---

### Enable DDoS Protection

Use AWS Shield for automatic DDoS mitigation.

---

### Protect Private Content

Use signed URLs or signed cookies.

---

# 10.14 Benefits of CloudFront Security

* Secure content delivery
* Protection from web attacks
* Secure origin access
* Global DDoS protection
* Data encryption

---
---
# 11. CloudFront Pricing Model
---

## 11.1 Overview

The pricing of **Amazon CloudFront** is based on a **pay-as-you-go model**.
You only pay for the resources you use when delivering content through the CloudFront network.

CloudFront pricing mainly depends on:

* Data transfer out to the internet
* Number of HTTP/HTTPS requests
* Invalidation requests
* Optional features such as real-time logs or dedicated IP SSL

Understanding CloudFront pricing helps optimize infrastructure costs for large-scale applications.

---

# 11.2 Main CloudFront Pricing Components

CloudFront pricing is divided into several categories:

1. Data Transfer Out
2. HTTP/HTTPS Requests
3. Cache Invalidation
4. Real-Time Logs
5. Dedicated IP SSL Certificates

---

# 11.3 Data Transfer Out

Data transfer out refers to the amount of data delivered from CloudFront edge locations to users.

The cost depends on:

* The amount of data transferred
* The geographic region where the data is delivered

Example:

```text
User downloads image.jpg (2 MB)
```

CloudFront charges for the **2 MB of data transferred**.

---

### Example Pricing Structure (Approximate)

| Data Transfer Region | Cost (per GB) |
| -------------------- | ------------- |
| North America        | Lower cost    |
| Europe               | Moderate cost |
| Asia                 | Higher cost   |
| South America        | Highest cost  |

Prices decrease as data transfer volume increases.

---

# 11.4 HTTP and HTTPS Request Pricing

CloudFront charges for the number of **requests processed by edge locations**.

Two main request types:

* HTTP requests
* HTTPS requests

Example request:

```text
https://example.com/logo.png
```

Each time a user requests a file, CloudFront counts it as **one request**.

---

### Example Request Pricing

| Request Type  | Cost                 |
| ------------- | -------------------- |
| HTTP Request  | Lower cost           |
| HTTPS Request | Slightly higher cost |

HTTPS requests cost more because they require **SSL/TLS encryption processing**.

---

# 11.5 Cache Invalidation Pricing

Cache invalidation allows you to remove cached files from CloudFront edge locations.

Example invalidation request:

```text
/images/logo.png
```

CloudFront will remove the cached version of this file from all edge locations.

---

### Free Invalidation Limit

CloudFront provides:

```text
First 1000 invalidation paths per month → Free
```

After this limit, additional invalidation requests incur charges.

Example:

```text
/images/*
```

Counts as **one invalidation path**.

---

# 11.6 Real-Time Logs Pricing

CloudFront provides **real-time logging** that streams request data to monitoring systems.

Logs can be sent to:

* Amazon Kinesis Data Streams
* Analytics tools

Real-time logs are charged based on:

* Number of log lines delivered
* Data processing

These logs help analyze traffic patterns and performance.

---

# 11.7 Dedicated IP SSL Pricing

CloudFront supports two SSL options:

### Shared SSL Certificate

Uses shared IP addresses across CloudFront distributions.

Example:

```text
d123abcd.cloudfront.net
```

Cost:

```text
Included in CloudFront pricing
```

---

### Dedicated IP SSL Certificate

Used for legacy clients that require dedicated IP addresses.

Example:

```text
cdn.example.com
```

This option incurs an **additional monthly cost**.

---

# 11.8 CloudFront Free Tier

AWS offers a **free tier** for CloudFront usage.

Free tier benefits include:

```text
1 TB Data Transfer Out
10,000,000 HTTP/HTTPS Requests
2,000,000 CloudFront Functions Invocations
```

Free tier is available for **12 months after account creation**.

---

# 11.9 Example Pricing Scenario

Example application:

* Website traffic: 100,000 users
* Average file size: 1 MB
* Total data delivered: 100 GB

Estimated charges include:

* Data transfer cost
* Request processing cost

Caching reduces costs because fewer requests reach the origin server.

---

# 11.10 Cost Optimization Strategies

### Enable Caching

Store frequently accessed content in edge locations to reduce origin requests.

---

### Compress Content

Use compression techniques such as:

* Gzip
* Brotli

This reduces the size of transferred data.

---

### Use Cache-Control Headers

Define caching rules so content stays longer in the cache.

---

### Minimize Cache Invalidations

Avoid unnecessary invalidation requests to reduce costs.

---

### Use Appropriate TTL Settings

Proper TTL values reduce origin requests and improve caching efficiency.

---

# 11.11 Example Cost-Efficient Architecture

```text
Users
 │
 ▼
CloudFront Edge Locations
 │
 ▼
Cached Content
 │
 ▼
Origin Server
 ├── Amazon S3
 ├── Application Load Balancer
 └── API Gateway
```

In this architecture:

* Most requests are served from the cache
* Origin servers receive fewer requests
* Infrastructure costs are reduced

---

# 11.12 Monitoring CloudFront Costs

CloudFront costs can be monitored using AWS services such as:

* AWS Cost Explorer
* AWS Billing Dashboard
* Amazon CloudWatch

These tools help track usage and optimize spending.

---

# 11.13 Key Benefits of CloudFront Pricing Model

* Pay only for what you use
* No upfront costs
* Automatic scaling
* Cost-effective global delivery

---
---
# 12. CloudFront Cache Policies
---

## 12.1 Overview

**Cache Policies** in **Amazon CloudFront** define how CloudFront caches content and determines what information is included in the **cache key**.

A cache policy controls:

* How long objects stay in the cache (TTL settings)
* Which headers are included in caching
* Which cookies are included in caching
* Which query strings are included in caching

Cache policies help optimize:

* Performance
* Cache efficiency
* Origin server load

---

# 12.2 What is a Cache Policy

A **Cache Policy** is a set of rules that tells CloudFront:

* How to cache content
* How to generate cache keys
* How long to store objects in cache

Example workflow:

```text
User Request
     │
     ▼
CloudFront Cache Policy Applied
     │
     ▼
Cache Key Generated
     │
     ▼
Cache Lookup
     │
 ┌───┴────┐
 │        │
Hit      Miss
 │        │
 ▼        ▼
Serve     Request Origin
Cache
```

---

# 12.3 Components of Cache Policy

A cache policy mainly includes the following components:

1. TTL Settings
2. Header Caching
3. Cookie Caching
4. Query String Caching

These components define how CloudFront handles caching behavior.

---

# 12.4 TTL Settings in Cache Policy

TTL determines how long content remains in the cache.

Three TTL values can be defined.

### Minimum TTL

The minimum amount of time CloudFront keeps objects in cache.

Example:

```text
Minimum TTL = 0 seconds
```

---

### Default TTL

The default time CloudFront caches objects when no caching headers are provided.

Example:

```text
Default TTL = 3600 seconds (1 hour)
```

---

### Maximum TTL

The maximum duration CloudFront can cache objects.

Example:

```text
Maximum TTL = 86400 seconds (24 hours)
```

---

# 12.5 Header-Based Caching

Headers can influence the response returned by the origin server.

CloudFront can include selected headers in the cache key.

Example headers:

* Authorization
* User-Agent
* Accept-Language

Example:

```text
Header Included in Cache Key: User-Agent
```

This means requests from different devices may create separate cache entries.

Example:

```text
User-Agent: Mobile
User-Agent: Desktop
```

Two separate cached responses will be stored.

---

# 12.6 Cookie-Based Caching

Cookies contain user-specific information.

CloudFront can include cookies in the cache key.

Cookie options include:

### None

No cookies included in cache key.

Example:

```text
Cookie Setting: None
```

Best for static websites.

---

### Whitelist Cookies

Only selected cookies are included.

Example:

```text
Allowed Cookie: session_id
```

---

### All Cookies

All cookies are included in the cache key.

Example:

```text
Cookie Setting: All
```

Used for personalized applications.

---

# 12.7 Query String Caching

Query strings are parameters included in URLs.

Example:

```text
https://example.com/product?id=100
```

Query string:

```text
id=100
```

CloudFront cache policy can define how query strings are handled.

---

### No Query Strings

Query strings are ignored.

Example:

```text
product?id=100
product?id=200
```

Both requests return the same cached object.

---

### All Query Strings

Every unique query string creates a new cache entry.

Example:

```text
product?id=100
product?id=200
```

Two different cached objects.

---

### Specific Query Strings

Only selected query strings are included.

Example:

```text
Allowed Query String: id
```

---

# 12.8 Managed Cache Policies

CloudFront provides **AWS-managed cache policies**.

These policies are optimized for common use cases.

Examples include:

### CachingOptimized

Used for static content.

Characteristics:

* No cookies
* No headers
* No query strings

---

### CachingDisabled

Disables caching completely.

Used for dynamic applications.

---

### CachingOptimizedForUncompressedObjects

Used when compression is not enabled.

---

# 12.9 Custom Cache Policies

Users can create **custom cache policies** for specific application requirements.

Custom policies allow control over:

* TTL values
* Header inclusion
* Cookie inclusion
* Query string handling

Example custom policy:

```text
Default TTL = 2 hours
Include Query String = id
Forward Header = Authorization
```

---

# 12.10 Cache Policy Example

Example architecture:

```text
User Request
      │
      ▼
CloudFront Distribution
      │
      ▼
Cache Policy Applied
      │
      ▼
Cache Key Generated
      │
      ▼
Cache Lookup
      │
 ┌────┴─────┐
 │          │
Hit        Miss
 │          │
 ▼          ▼
Serve      Request Origin
Cached
Content
```

---

# 12.11 Best Practices for Cache Policies

### Avoid Unnecessary Headers

Forwarding unnecessary headers reduces cache efficiency.

---

### Limit Cookies

Include only required cookies to improve caching performance.

---

### Use Query Strings Carefully

Forward only necessary query strings.

---

### Increase TTL for Static Content

Static files should have longer cache durations.

---

# 12.12 Advantages of Cache Policies

* Better caching efficiency
* Reduced origin server load
* Faster content delivery
* Improved scalability
* Better cost optimization

---

# 12.13 Example CloudFront Cache Policy Architecture

```text
Users
 │
 ▼
CloudFront Edge Location
 │
 ▼
Cache Policy Applied
 │
 ▼
Cache Storage
 │
 ▼
Origin Server
```

This architecture ensures optimized content caching.

---
---
# 13. Origin Request Policies
---

## 13.1 Overview

An **Origin Request Policy** in **Amazon CloudFront** controls **what information CloudFront sends to the origin server** when a request is forwarded.

When CloudFront receives a user request, it may forward certain parts of the request to the origin server such as:

* HTTP headers
* Cookies
* Query strings

Origin request policies determine **which of these values are included in the request sent to the origin**.

This is important for applications that require specific request information to generate dynamic responses.

---

# 13.2 How Origin Request Policies Work

Basic workflow:

```text
User Request
     │
     ▼
CloudFront Edge Location
     │
     ▼
Cache Check
     │
 ┌───┴────┐
 │        │
Hit      Miss
 │        │
 ▼        ▼
Serve     Apply Origin Request Policy
Cache     │
          ▼
       Forward Request to Origin
```

When a **cache miss occurs**, CloudFront uses the **origin request policy** to decide what request details to forward.

---

# 13.3 Components of Origin Request Policy

An origin request policy can include the following request information:

1. HTTP Headers
2. Cookies
3. Query Strings

These components control what data is sent to the origin server.

---

# 13.4 Header Forwarding

HTTP headers contain metadata about the request.

Examples include:

* Authorization
* User-Agent
* Host
* Accept-Language
* Referer

Some applications rely on headers to generate responses.

Example:

```text
Authorization: Bearer token123
```

If the **Authorization header** is forwarded, the origin server can validate user authentication.

Example configuration:

```text
Forward Header: Authorization
```

---

# 13.5 Cookie Forwarding

Cookies store user-specific data such as session information.

Example cookie:

```text
session_id=abc123
```

CloudFront can forward cookies to the origin server.

Options include:

### None

No cookies are forwarded.

Example:

```text
Cookie Forwarding: None
```

Best used for static content.

---

### Whitelist Cookies

Only selected cookies are forwarded.

Example:

```text
Forward Cookie: session_id
```

---

### All Cookies

All cookies are forwarded to the origin server.

Example:

```text
Cookie Forwarding: All
```

Used for applications requiring full session management.

---

# 13.6 Query String Forwarding

Query strings are parameters included in URLs.

Example:

```text
https://example.com/product?id=10
```

Query string:

```text
id=10
```

CloudFront can forward query strings to the origin server.

Options include:

### None

Query strings are not forwarded.

Example:

```text
product?id=10
product?id=20
```

Both requests are treated the same.

---

### All Query Strings

All query strings are forwarded to the origin server.

Example:

```text
product?id=10
product?id=20
```

These requests are handled separately.

---

### Specific Query Strings

Only selected query parameters are forwarded.

Example:

```text
Forward Query String: id
```

---

# 13.7 Managed Origin Request Policies

CloudFront provides several **AWS-managed origin request policies**.

Examples include:

### AllViewer

Forwards all headers, cookies, and query strings.

Use case:

* Dynamic web applications

---

### AllViewerExceptHostHeader

Forwards everything except the Host header.

Use case:

* API Gateway integration

---

### CORS-S3Origin

Used for S3 origins that require CORS headers.

---

### CORS-CustomOrigin

Used when CORS headers must be forwarded to custom origins.

---

# 13.8 Custom Origin Request Policies

Users can create custom policies to forward only required request parameters.

Example configuration:

```text
Forward Headers:
Authorization
User-Agent

Forward Cookies:
session_id

Forward Query Strings:
id
```

This ensures that only necessary data is forwarded to the origin server.

---

# 13.9 Difference Between Cache Policy and Origin Request Policy

| Feature  | Cache Policy                                | Origin Request Policy                      |
| -------- | ------------------------------------------- | ------------------------------------------ |
| Purpose  | Controls caching behavior                   | Controls what is sent to origin            |
| Used For | Cache key generation                        | Origin request configuration               |
| Includes | Headers, cookies, query strings for caching | Headers, cookies, query strings for origin |
| Impact   | Cache efficiency                            | Origin server processing                   |

---

# 13.10 Example Architecture Using Origin Request Policy

```text
User
 │
 ▼
CloudFront Edge Location
 │
 ▼
Cache Policy Applied
 │
 ▼
Origin Request Policy Applied
 │
 ▼
Origin Server
 ├── S3
 ├── EC2
 └── Load Balancer
```

---

# 13.11 Best Practices for Origin Request Policies

### Forward Only Required Headers

Avoid forwarding unnecessary headers to reduce complexity.

---

### Limit Cookie Forwarding

Forward only required cookies to maintain caching efficiency.

---

### Use Query Strings Carefully

Forward only necessary query parameters.

---

### Combine with Cache Policies

Use origin request policies together with cache policies for optimized performance.

---

# 13.12 Advantages of Origin Request Policies

* Better request control
* Improved performance
* Reduced origin server load
* More efficient caching
* Secure request forwarding

---

# 13.13 Example Request Flow with Origin Request Policy

```text
User Request
      │
      ▼
CloudFront Distribution
      │
      ▼
Cache Lookup
      │
 ┌────┴────┐
 │         │
Hit       Miss
 │         │
 ▼         ▼
Serve     Apply Origin Request Policy
Content   │
          ▼
       Forward Request
          │
          ▼
       Origin Server
```

---
---
# 14. Response Headers Policies
---

## 14.1 Overview

A **Response Headers Policy** in **Amazon CloudFront** controls the HTTP headers that CloudFront adds to responses before sending them to users.

These headers help manage:

* Security settings
* Cross-origin resource sharing (CORS)
* Browser behavior
* Custom response information

Response headers policies allow administrators to enforce consistent security and browser configuration without modifying the origin server.

---

# 14.2 How Response Headers Policies Work

When CloudFront receives a response from the origin server, it can add or modify headers before delivering the response to the user.

Basic workflow:

```text
User Request
     │
     ▼
CloudFront Edge Location
     │
     ▼
Origin Server Response
     │
     ▼
Apply Response Headers Policy
     │
     ▼
Modified Response Sent to User
```

This ensures that every response contains the required security and configuration headers.

---

# 14.3 Types of Response Headers

Response headers policies generally manage the following types of headers:

1. Security Headers
2. CORS Headers
3. Custom Headers
4. Remove Headers

These headers control how browsers handle requests and responses.

---

# 14.4 Security Headers

Security headers protect web applications from common attacks and enforce secure browser behavior.

Important security headers include:

### Strict-Transport-Security (HSTS)

Forces browsers to use HTTPS connections.

Example:

```text
Strict-Transport-Security: max-age=31536000
```

This instructs browsers to use HTTPS for the next **1 year**.

---

### Content-Security-Policy (CSP)

Prevents malicious scripts from running on web pages.

Example:

```text
Content-Security-Policy: default-src 'self'
```

Only content from the same domain is allowed.

---

### X-Content-Type-Options

Prevents browsers from guessing content types.

Example:

```text
X-Content-Type-Options: nosniff
```

---

### X-Frame-Options

Prevents clickjacking attacks.

Example:

```text
X-Frame-Options: DENY
```

This prevents the page from being loaded inside an iframe.

---

### Referrer-Policy

Controls how much referrer information is shared.

Example:

```text
Referrer-Policy: strict-origin
```

---

# 14.5 CORS Headers

CORS (Cross-Origin Resource Sharing) allows resources to be accessed from different domains.

This is commonly used for:

* APIs
* Web applications
* JavaScript requests

Important CORS headers include:

### Access-Control-Allow-Origin

Defines which domains can access the resource.

Example:

```text
Access-Control-Allow-Origin: *
```

This allows all domains.

---

### Access-Control-Allow-Methods

Defines allowed HTTP methods.

Example:

```text
Access-Control-Allow-Methods: GET, POST, PUT
```

---

### Access-Control-Allow-Headers

Defines allowed request headers.

Example:

```text
Access-Control-Allow-Headers: Authorization
```

---

### Access-Control-Max-Age

Defines how long browsers cache CORS responses.

Example:

```text
Access-Control-Max-Age: 3600
```

---

# 14.6 Custom Response Headers

CloudFront allows adding custom headers to responses.

Example:

```text
X-Company-Name: ExampleCorp
```

Custom headers are often used for:

* Application identification
* Debugging
* Analytics

---

# 14.7 Removing Response Headers

CloudFront can remove specific headers before delivering responses.

Example:

Headers removed:

```text
Server
X-Powered-By
```

This helps hide backend server details and improve security.

---

# 14.8 Managed Response Headers Policies

CloudFront provides several **AWS-managed response headers policies**.

Examples include:

### SimpleCORS

Adds basic CORS headers.

---

### CORS-With-Preflight

Supports CORS preflight requests.

---

### SecurityHeadersPolicy

Adds common security headers such as:

* HSTS
* X-Frame-Options
* X-Content-Type-Options

---

# 14.9 Custom Response Headers Policies

Users can create custom policies to control response headers.

Example configuration:

```text
Security Headers:
Strict-Transport-Security
X-Frame-Options
X-Content-Type-Options

CORS Headers:
Access-Control-Allow-Origin: *

Custom Header:
X-App-Version: 1.0
```

This configuration ensures secure and consistent responses.

---

# 14.10 Example Architecture

```text
User
 │
 ▼
CloudFront Edge Location
 │
 ▼
Origin Server
 │
 ▼
Response Headers Policy Applied
 │
 ▼
Secure Response Delivered
```

---

# 14.11 Benefits of Response Headers Policies

* Improved application security
* Consistent header configuration
* Reduced origin server complexity
* Protection against common web attacks
* Better browser compatibility

---

# 14.12 Best Practices

### Enable Security Headers

Always configure security headers to protect applications.

---

### Configure CORS Carefully

Allow only trusted domains instead of using `*` whenever possible.

---

### Remove Sensitive Headers

Remove headers that expose backend information.

---

### Use Managed Policies

Use AWS-managed policies when possible for simplicity and security.

---

# 14.13 Example Response Header Flow

```text
User Request
      │
      ▼
CloudFront
      │
      ▼
Origin Server
      │
      ▼
Apply Response Headers Policy
      │
      ▼
Add Security + CORS Headers
      │
      ▼
Response Sent to User
```

---
---
# 15. CloudFront Functions
---

## 15.1 Overview

**CloudFront Functions** are lightweight JavaScript functions that run at **CloudFront edge locations**.

They allow developers to modify **HTTP requests and responses** before CloudFront processes them or sends them back to users.

CloudFront Functions are designed for:

* Very fast execution
* High scalability
* Low latency

They execute directly at the **edge of the AWS network**, meaning the logic runs closer to users.

---

# 15.2 Edge Computing Concept

Edge computing means running code **closer to the user**, instead of running it in centralized servers.

Traditional architecture:

```text
User → Internet → Server → Response
```

With edge computing:

```text
User → Edge Location (Function executed) → Response
```

This reduces latency and improves application performance.

---

# 15.3 How CloudFront Functions Work

CloudFront Functions run during specific request stages.

Workflow:

```text
User Request
     │
     ▼
CloudFront Edge Location
     │
     ▼
CloudFront Function Executed
     │
     ▼
Request Processed
     │
     ▼
Content Delivered
```

These functions execute **before CloudFront sends the request to the origin** or **before the response is returned to the user**.

---

# 15.4 Function Execution Points

CloudFront Functions run at two stages:

### Viewer Request

Executed when CloudFront receives a request from the user.

Example:

```text
User → CloudFront → Function → Process Request
```

Use cases:

* URL rewriting
* Authentication checks
* Request validation

---

### Viewer Response

Executed before CloudFront sends the response back to the user.

Example:

```text
Origin → CloudFront → Function → Response Sent to User
```

Use cases:

* Add security headers
* Modify response headers

---

# 15.5 Common Use Cases

CloudFront Functions are used for many edge-level operations.

### URL Rewriting

Example:

```text
/user → /user/index.html
```

Used for static websites.

---

### Redirect Requests

Example:

```text
http://example.com → https://example.com
```

Force HTTPS connections.

---

### Authentication Checks

Verify tokens or session data before forwarding requests.

Example:

```text
Authorization Header Validation
```

---

### Header Manipulation

Add or modify HTTP headers.

Example:

```text
Add Header:
X-App-Version: 1.0
```

---

### Bot Filtering

Identify and block unwanted bot traffic.

---

# 15.6 Example CloudFront Function

Example JavaScript function:

```javascript
function handler(event) {
    var request = event.request;

    if (request.uri === "/") {
        request.uri = "/index.html";
    }

    return request;
}
```

Function behavior:

* If user requests `/`
* CloudFront redirects to `/index.html`

---

# 15.7 CloudFront Functions vs Lambda@Edge

CloudFront Functions and Lambda@Edge both run at the edge, but they serve different purposes.

| Feature         | CloudFront Functions | Lambda@Edge       |
| --------------- | -------------------- | ----------------- |
| Execution Speed | Very fast            | Moderate          |
| Runtime         | JavaScript only      | Multiple runtimes |
| Complexity      | Simple logic         | Complex logic     |
| Latency         | Extremely low        | Slightly higher   |
| Cost            | Lower cost           | Higher cost       |

CloudFront Functions are best for **simple request transformations**.

Lambda@Edge is used for **advanced application logic**.

---

# 15.8 Function Execution Architecture

Example architecture:

```text
User
 │
 ▼
CloudFront Edge Location
 │
 ▼
CloudFront Function
 │
 ▼
Cache Check
 │
 ▼
Origin Server
```

The function runs **before CloudFront checks the cache**.

---

# 15.9 Performance Benefits

CloudFront Functions provide several advantages:

### Ultra-Low Latency

Functions execute within microseconds.

---

### High Scalability

CloudFront can run functions across **all edge locations globally**.

---

### Cost Efficiency

CloudFront Functions cost less than Lambda@Edge.

---

### Faster Request Processing

Requests can be modified before reaching the origin.

---

# 15.10 Example Real-World Use Case

Example: Redirect non-www traffic.

```text
example.com → www.example.com
```

Workflow:

```text
User Request
      │
      ▼
CloudFront Function
      │
      ▼
Redirect to www.example.com
      │
      ▼
Response Sent to User
```

---

# 15.11 Limitations of CloudFront Functions

CloudFront Functions have some limitations:

* JavaScript runtime only
* Limited execution time
* No access to external services
* Cannot access request body

These limitations make them suitable only for **lightweight operations**.

---

# 15.12 Best Practices

### Keep Functions Lightweight

Avoid complex logic.

---

### Use for Request Transformations

Ideal for URL rewriting, redirects, and header modifications.

---

### Combine with CloudFront Caching

Functions can optimize caching behavior.

---

# 15.13 Example CloudFront Functions Workflow

```text
User Request
      │
      ▼
CloudFront Edge Location
      │
      ▼
CloudFront Function Executed
      │
      ▼
Request Modified
      │
      ▼
Cache Check
      │
      ▼
Origin Server
```

---

# 15.14 Advantages of CloudFront Functions

* Faster edge processing
* Reduced latency
* Improved request handling
* Lower operational cost
* Global scalability

---
---
# 16. Lambda@Edge
---

## 16.1 Overview

**Lambda@Edge** allows you to run serverless functions at **CloudFront edge locations** using **AWS Lambda**.

It enables developers to run custom code closer to users to:

* Modify requests
* Modify responses
* Implement authentication
* Personalize content

Lambda@Edge integrates directly with **CloudFront distributions**, allowing logic to run during different stages of the request lifecycle.

---

# 16.2 Edge Computing with Lambda@Edge

Traditional web architecture:

```text
User → Internet → Origin Server → Response
```

With Lambda@Edge:

```text
User → CloudFront Edge → Lambda@Edge → Origin → Response
```

Lambda@Edge runs code at the **edge location**, reducing latency and improving response time.

---

# 16.3 How Lambda@Edge Works

When a user sends a request to CloudFront, Lambda@Edge functions can be triggered during specific request or response events.

Workflow:

```text
User Request
     │
     ▼
CloudFront Edge Location
     │
     ▼
Lambda@Edge Function
     │
     ▼
Origin Server
     │
     ▼
Response Returned
```

The Lambda function can modify the request or response before continuing.

---

# 16.4 Lambda@Edge Event Triggers

Lambda@Edge supports **four event triggers** in the CloudFront request lifecycle.

1. Viewer Request
2. Viewer Response
3. Origin Request
4. Origin Response

Each event allows different types of request processing.

---

# 16.5 Viewer Request Event

The **Viewer Request** event occurs when CloudFront receives a request from a user.

Example workflow:

```text
User → CloudFront → Lambda@Edge (Viewer Request)
```

Common use cases:

* Authentication checks
* URL rewriting
* Redirecting requests
* Request validation

Example scenario:

```text
User Request → Lambda@Edge → Validate Token
```

---

# 16.6 Viewer Response Event

The **Viewer Response** event occurs before CloudFront sends the response back to the user.

Example workflow:

```text
Origin Response → Lambda@Edge → User
```

Common use cases:

* Add security headers
* Modify response headers
* Response customization

Example:

```text
Add Header: X-App-Version: 1.0
```

---

# 16.7 Origin Request Event

The **Origin Request** event occurs when CloudFront forwards a request to the origin server.

Example workflow:

```text
CloudFront → Lambda@Edge → Origin Server
```

Use cases:

* Dynamic origin selection
* Request modification
* Load balancing logic

Example:

```text
Route request to different origin servers
```

---

# 16.8 Origin Response Event

The **Origin Response** event occurs when the origin server returns a response to CloudFront.

Example workflow:

```text
Origin Server → Lambda@Edge → CloudFront → User
```

Use cases:

* Modify response data
* Add headers
* Implement caching logic

---

# 16.9 Lambda@Edge Example Function

Example Node.js Lambda function:

```javascript
exports.handler = async (event) => {
    const request = event.Records[0].cf.request;

    if (request.uri === "/") {
        request.uri = "/index.html";
    }

    return request;
};
```

Function behavior:

* If user requests `/`
* CloudFront returns `/index.html`

---

# 16.10 Lambda@Edge Architecture

Example architecture:

```text
User
 │
 ▼
CloudFront Distribution
 │
 ▼
Lambda@Edge Function
 │
 ▼
Origin Server
 ├── Amazon S3
 ├── EC2
 └── API Gateway
```

Lambda@Edge executes before or after CloudFront interacts with the origin.

---

# 16.11 Common Lambda@Edge Use Cases

### User Authentication

Verify login tokens before allowing access.

Example:

```text
Check Authorization Header
```

---

### A/B Testing

Serve different content versions to different users.

Example:

```text
User Group A → Version A
User Group B → Version B
```

---

### URL Redirection

Redirect users to different pages.

Example:

```text
old-page.html → new-page.html
```

---

### Dynamic Content Personalization

Modify responses based on:

* User location
* Device type
* Language

---

# 16.12 Lambda@Edge vs CloudFront Functions

| Feature        | CloudFront Functions     | Lambda@Edge                 |
| -------------- | ------------------------ | --------------------------- |
| Complexity     | Simple logic             | Complex logic               |
| Runtime        | JavaScript               | Node.js / Python            |
| Execution time | Very short               | Longer execution            |
| Latency        | Extremely low            | Slightly higher             |
| Use case       | Header/URL modifications | Advanced request processing |

CloudFront Functions are better for **lightweight tasks**, while Lambda@Edge supports **advanced processing**.

---

# 16.13 Limitations of Lambda@Edge

Lambda@Edge has some limitations:

* Deployment must occur in **us-east-1 region**
* Cold start latency may occur
* Execution time limits apply
* Higher cost compared to CloudFront Functions

---

# 16.14 Best Practices

### Use Lambda@Edge for Complex Logic

Implement authentication, routing, and dynamic content processing.

---

### Avoid Heavy Processing

Keep functions efficient to reduce latency.

---

### Combine with CloudFront Caching

Caching improves performance and reduces origin requests.

---

### Monitor Using CloudWatch

Monitor logs and performance metrics.

---

# 16.15 Example Lambda@Edge Request Lifecycle

```text
User Request
      │
      ▼
Viewer Request Event
      │
      ▼
CloudFront Cache Check
      │
      ▼
Origin Request Event
      │
      ▼
Origin Server
      │
      ▼
Origin Response Event
      │
      ▼
Viewer Response Event
      │
      ▼
Response Delivered to User
```

---

# 16.16 Benefits of Lambda@Edge

* Execute logic at global edge locations
* Improve application performance
* Reduce latency
* Enable advanced request processing
* Integrate with CloudFront infrastructure

---
---
# 17. CloudFront Logging and Monitoring
---

## 17.1 Overview

**Logging and Monitoring** in **Amazon CloudFront** help administrators track requests, analyze traffic patterns, and troubleshoot issues.

CloudFront provides multiple monitoring and logging mechanisms that allow visibility into how content is delivered and how users interact with applications.

Main monitoring and logging features include:

* Standard Logging (Access Logs)
* Real-Time Logging
* CloudWatch Metrics
* CloudWatch Alarms
* AWS Monitoring Tools

These tools help maintain **performance, security, and reliability**.

---

# 17.2 Standard Logging (Access Logs)

Standard logging records detailed information about every request processed by CloudFront.

Logs are typically stored in an **Amazon S3 bucket**.

Example workflow:

```text
User Request
     │
     ▼
CloudFront Edge Location
     │
     ▼
Request Processed
     │
     ▼
Access Log Generated
     │
     ▼
Stored in S3 Bucket
```

These logs help analyze traffic and diagnose issues.

---

## 17.2.1 Information Stored in Access Logs

Each log entry may contain the following information:

* Request date and time
* Client IP address
* HTTP method (GET, POST, etc.)
* Requested object path
* HTTP response status code
* Referrer information
* User-Agent details
* Bytes transferred
* Edge location used

Example log entry:

```text
2026-03-10 12:30:45 LAX1 GET example.com /image.jpg 200 Mozilla/5.0
```

---

# 17.3 Real-Time Logging

Real-time logging allows near-instant analysis of CloudFront requests.

Instead of storing logs in S3 with delays, real-time logs are streamed to **Amazon Kinesis Data Streams**.

Example architecture:

```text
User Request
      │
      ▼
CloudFront Edge Location
      │
      ▼
Real-Time Logs Generated
      │
      ▼
Kinesis Data Streams
      │
      ▼
Analytics Tools
```

Real-time logs allow monitoring within **seconds of request processing**.

---

## 17.3.1 Use Cases of Real-Time Logging

Real-time logs are useful for:

* Security monitoring
* Traffic analysis
* Real-time dashboards
* Fraud detection
* Performance monitoring

---

# 17.4 CloudWatch Metrics

CloudFront automatically sends operational metrics to **Amazon CloudWatch**.

These metrics help monitor performance and usage.

Common CloudFront metrics include:

* Requests
* Bytes Downloaded
* Bytes Uploaded
* Cache Hit Rate
* Error Rate

Example architecture:

```text
CloudFront
     │
     ▼
CloudWatch Metrics
     │
     ▼
Monitoring Dashboard
```

---

# 17.5 Important CloudFront Metrics

### Request Count

Total number of requests processed by CloudFront.

Example:

```text
Requests = 1,000,000
```

---

### Cache Hit Ratio

Percentage of requests served from cache.

Example:

```text
Cache Hit Ratio = 85%
```

Higher values indicate better caching efficiency.

---

### Error Rate

Percentage of failed requests.

Example:

```text
Error Rate = 2%
```

Errors include:

* 4xx client errors
* 5xx server errors

---

### Data Transfer Metrics

Shows how much data is delivered through CloudFront.

Examples:

* Bytes downloaded
* Bytes uploaded

---

# 17.6 CloudWatch Alarms

CloudWatch alarms can trigger notifications when metrics exceed defined thresholds.

Example alarm:

```text
If Error Rate > 5%
Send Alert
```

Alarm workflow:

```text
CloudWatch Metric
      │
      ▼
Threshold Exceeded
      │
      ▼
CloudWatch Alarm Triggered
      │
      ▼
SNS Notification Sent
```

This helps detect problems quickly.

---

# 17.7 Integration with AWS Monitoring Tools

CloudFront integrates with multiple AWS monitoring services.

### Amazon CloudWatch

Used for metrics and alarms.

---

### AWS CloudTrail

Tracks API activity and configuration changes.

Example:

```text
CreateDistribution
UpdateDistribution
DeleteDistribution
```

CloudTrail helps with auditing and compliance.

---

### AWS X-Ray

Used for tracing distributed applications and debugging.

---

# 17.8 Example Logging Architecture

```text
Users
 │
 ▼
CloudFront Edge Locations
 │
 ├── Access Logs → S3 Bucket
 │
 └── Real-Time Logs → Kinesis Streams
      │
      ▼
Analytics Systems
```

This architecture provides both **historical and real-time monitoring**.

---

# 17.9 Troubleshooting Using Logs

CloudFront logs help diagnose issues such as:

### High Error Rates

Example:

```text
HTTP 502
HTTP 503
HTTP 504
```

These errors may indicate origin server issues.

---

### Cache Problems

Low cache hit ratio may indicate inefficient caching policies.

---

### Traffic Analysis

Logs help identify:

* Most requested content
* User locations
* Peak traffic times

---

# 17.10 Best Practices for Monitoring

### Enable Access Logs

Always enable standard logging for production environments.

---

### Use Real-Time Logs for Critical Applications

Real-time logs help detect issues quickly.

---

### Monitor Cache Hit Ratio

Optimizing cache policies improves performance.

---

### Configure CloudWatch Alarms

Alerts help detect performance issues early.

---

# 17.11 Example Monitoring Workflow

```text
User Request
      │
      ▼
CloudFront Edge Location
      │
      ▼
Metrics Generated
      │
      ▼
CloudWatch Monitoring
      │
      ▼
Alarm Triggered (if needed)
      │
      ▼
SNS Notification
```

---

# 17.12 Benefits of CloudFront Logging and Monitoring

* Improved system visibility
* Faster troubleshooting
* Better traffic analysis
* Enhanced performance optimization
* Stronger security monitoring

---
---
# 18. CloudFront Invalidation
---

## 18.1 Overview

**CloudFront Invalidation** is the process of removing cached objects from **CloudFront edge locations** before their **TTL (Time To Live)** expires.

Normally, cached content stays in the edge cache until its TTL ends. However, if the content is updated on the origin server, users may still receive the **old cached version**.

Invalidation forces CloudFront to **delete the cached copy** so that the next user request fetches the **updated content from the origin server**.

---

# 18.2 Why Cache Invalidation is Needed

Cache invalidation is required when the origin content changes but the cached version is still being served.

Example scenario:

```text
User requests logo.png
CloudFront caches logo.png for 24 hours
```

If the logo is updated on the origin server:

```text
Users still receive the old logo until TTL expires
```

Using invalidation ensures users receive the **latest version immediately**.

---

# 18.3 How CloudFront Invalidation Works

Basic workflow:

```text
Content Updated on Origin
        │
        ▼
Create Invalidation Request
        │
        ▼
CloudFront Removes Cached Object
        │
        ▼
Next User Request
        │
        ▼
Fetch Updated Content from Origin
```

This ensures that the latest content is delivered.

---

# 18.4 Invalidation Process

Step-by-step process:

### Step 1 – Update Content

Content is updated in the origin server.

Example:

```text
/images/logo.png
```

---

### Step 2 – Create Invalidation Request

An invalidation request is submitted to CloudFront.

Example:

```text
/images/logo.png
```

---

### Step 3 – CloudFront Removes Cached Files

CloudFront removes cached versions of the file from **all edge locations**.

---

### Step 4 – Next Request Fetches Updated Content

When users request the file again:

```text
User → CloudFront → Origin Server
```

CloudFront retrieves the **updated content**.

---

# 18.5 Types of Invalidation Requests

CloudFront supports two main types of invalidation.

---

## 18.5.1 Single File Invalidation

Used when only one file needs to be updated.

Example:

```text
/images/logo.png
```

This removes only the cached copy of **logo.png**.

---

## 18.5.2 Wildcard Invalidation

Wildcard invalidation removes multiple cached objects using a wildcard pattern.

Example:

```text
/images/*
```

This removes all cached files in the **images directory**.

Another example:

```text
/*
```

This removes **all cached objects** in the distribution.

---

# 18.6 Creating Invalidation Requests

Invalidation requests can be created using:

* AWS Management Console
* AWS CLI
* AWS SDK

---

## Example AWS CLI Command

```bash
aws cloudfront create-invalidation \
--distribution-id ABC123XYZ \
--paths "/images/logo.png"
```

Example wildcard invalidation:

```bash
aws cloudfront create-invalidation \
--distribution-id ABC123XYZ \
--paths "/images/*"
```

---

# 18.7 Invalidation Status

When an invalidation request is submitted, CloudFront processes it asynchronously.

Invalidation status includes:

* **In Progress**
* **Completed**

Example workflow:

```text
Invalidation Request Created
        │
        ▼
CloudFront Processing
        │
        ▼
Invalidation Completed
```

Once completed, the cached content is removed from edge locations.

---

# 18.8 Invalidation Pricing

CloudFront provides a free invalidation limit.

Free tier:

```text
First 1000 invalidation paths per month → Free
```

After the free limit:

Additional invalidation paths incur charges.

Example:

```text
/images/*
```

Counts as **one invalidation path**.

---

# 18.9 Alternative to Invalidation (Versioning)

Instead of invalidating cached files, many applications use **file versioning**.

Example:

Old file:

```text
logo.png
```

New file:

```text
logo_v2.png
```

Example URL:

```text
https://example.com/images/logo_v2.png
```

Advantages:

* No invalidation needed
* Faster cache updates
* Better performance

---

# 18.10 Example Invalidation Architecture

```text
User
 │
 ▼
CloudFront Edge Location
 │
 ▼
Cached Content
 │
 ▼
Invalidation Request
 │
 ▼
Cache Cleared
 │
 ▼
Origin Server
```

After invalidation, CloudFront retrieves fresh content from the origin.

---

# 18.11 Best Practices for Cache Invalidation

### Use File Versioning

Versioned files avoid unnecessary invalidation requests.

---

### Avoid Invalidating Entire Cache

Invalidating all objects can increase origin server load.

Example to avoid:

```text
/*
```

---

### Invalidate Specific Paths

Invalidate only required files.

Example:

```text
/css/style.css
```

---

### Automate Invalidation

Use CI/CD pipelines to trigger invalidation after deployments.

---

# 18.12 Common Use Cases

Cache invalidation is commonly used when:

* Updating website assets
* Fixing broken files
* Deploying new application versions
* Updating images or CSS files

---

# 18.13 Example Invalidation Workflow

```text
Update File on Origin
        │
        ▼
Create Invalidation Request
        │
        ▼
CloudFront Removes Cached File
        │
        ▼
Next User Request
        │
        ▼
Updated File Delivered
```

---

# 18.14 Benefits of Cache Invalidation

* Ensures users receive updated content
* Prevents stale data delivery
* Maintains application consistency
* Improves user experience

---
---
# 19. CloudFront Geographic Restrictions
---

## 19.1 Overview

**Geographic Restrictions (Geo Restrictions)** in **Amazon CloudFront** allow you to control access to your content based on the **geographic location of users**.

Using Geo Restrictions, you can:

* Allow access only from specific countries
* Block access from certain countries

CloudFront determines the user's location based on the **IP address** of the incoming request.

This feature is commonly used to comply with **licensing agreements, legal regulations, or security policies**.

---

# 19.2 How Geographic Restrictions Work

When a user sends a request to CloudFront, the system identifies the user's country using the IP address.

Workflow:

```text
User Request
     │
     ▼
CloudFront Edge Location
     │
     ▼
Check User Country (IP Address)
     │
 ┌───┴─────────┐
 │             │
Allowed        Blocked
 │             │
 ▼             ▼
Content        Access Denied
Delivered
```

If the user's country is blocked, CloudFront returns an **HTTP 403 Forbidden error**.

---

# 19.3 Types of Geographic Restrictions

CloudFront supports two main types of geographic restrictions.

---

## 19.3.1 Allow List (Whitelist)

In an allow list configuration, only users from specified countries are allowed to access the content.

Example configuration:

```text
Allowed Countries:
US
UK
CA
DE
```

Workflow:

```text
User from US → Access Allowed
User from India → Access Blocked
```

This is useful when content is licensed only in specific countries.

---

## 19.3.2 Block List (Blacklist)

In a block list configuration, users from specific countries are blocked.

Example configuration:

```text
Blocked Countries:
CN
RU
KP
```

Workflow:

```text
User from China → Access Blocked
User from Japan → Access Allowed
```

This approach is often used for security or regulatory reasons.

---

# 19.4 Example Geographic Restriction Architecture

```text
Users Worldwide
      │
      ▼
CloudFront Edge Location
      │
      ▼
Geo Restriction Check
      │
 ┌────┴─────┐
 │          │
Allowed     Blocked
 │          │
 ▼          ▼
Content     HTTP 403
Delivered   Access Denied
```

---

# 19.5 Use Cases of Geographic Restrictions

Geo restrictions are widely used in several scenarios.

---

## Content Licensing

Streaming platforms may restrict access to certain regions due to licensing agreements.

Example:

```text
Movie available only in US and Canada
```

---

## Regulatory Compliance

Some applications must block access from specific countries due to legal regulations.

Example:

```text
Financial services restricted in certain regions
```

---

## Security Protection

Organizations may block traffic from regions with high levels of malicious activity.

Example:

```text
Block traffic from high-risk countries
```

---

# 19.6 Configuring Geographic Restrictions

Geo restrictions can be configured when creating or updating a CloudFront distribution.

Configuration options include:

* Restriction type (Allow or Block)
* List of countries

Example configuration:

```text
Restriction Type: Allow List
Countries:
US
UK
CA
```

---

# 19.7 Custom Error Responses

When a request is blocked by geographic restrictions, CloudFront returns:

```text
HTTP 403 Forbidden
```

You can configure a **custom error page** for blocked users.

Example:

```text
Access to this content is not available in your region.
```

This improves the user experience.

---

# 19.8 Limitations of Geographic Restrictions

Geo restrictions have some limitations:

* Country-level filtering only (not city-level)
* IP-based detection may not always be accurate
* Users using VPNs may bypass restrictions

Despite these limitations, geo restrictions remain effective for most use cases.

---

# 19.9 Advanced Geographic Restrictions

For more advanced geographic filtering, organizations often use:

* AWS WAF Geo Match rules
* Third-party geolocation services

Example architecture:

```text
User
 │
 ▼
AWS WAF (Geo Filtering)
 │
 ▼
CloudFront
 │
 ▼
Origin Server
```

This approach provides more flexible location-based access control.

---

# 19.10 Best Practices

### Use Allow Lists for Licensed Content

Allow only countries where content distribution is permitted.

---

### Combine with AWS WAF

Use AWS WAF for advanced geographic filtering.

---

### Provide Custom Error Pages

Display user-friendly messages when access is blocked.

---

### Monitor Traffic Patterns

Use CloudFront logs and CloudWatch to analyze blocked traffic.

---

# 19.11 Example Request Flow with Geo Restriction

```text
User Request
      │
      ▼
CloudFront Edge Location
      │
      ▼
Identify User Country
      │
 ┌────┴─────┐
 │          │
Allowed     Blocked
 │          │
 ▼          ▼
Serve       Return
Content     HTTP 403
```

---

# 19.12 Benefits of Geographic Restrictions

* Control regional access to content
* Protect licensed media distribution
* Improve security policies
* Ensure regulatory compliance

---
---
# 20. CloudFront Integration with AWS Services
---

## 20.1 Overview

**Amazon CloudFront** integrates seamlessly with many **AWS services** to build scalable, secure, and high-performance architectures.

By integrating CloudFront with other AWS services, organizations can:

* Improve content delivery speed
* Reduce server load
* Enhance security
* Build highly scalable applications

Common AWS services integrated with CloudFront include:

* Amazon S3
* Amazon EC2
* Application Load Balancer (ALB)
* Amazon API Gateway
* AWS Lambda and Lambda@Edge
* AWS WAF
* AWS Shield
* Amazon Route 53

These integrations help create **modern cloud architectures**.

---

# 20.2 CloudFront Integration with Amazon S3

Amazon S3 is one of the most common origins used with CloudFront.

S3 stores static content such as:

* Images
* HTML files
* CSS
* JavaScript
* Videos

Architecture example:

```text
User
 │
 ▼
CloudFront
 │
 ▼
Amazon S3 Bucket
```

Benefits:

* Faster static website delivery
* Reduced latency
* Improved caching performance

Common use case:

```text
Static Website Hosting
```

---

# 20.3 CloudFront Integration with Amazon EC2

CloudFront can deliver content from applications hosted on **Amazon EC2 instances**.

Architecture example:

```text
User
 │
 ▼
CloudFront
 │
 ▼
EC2 Web Server
```

Benefits:

* Reduced load on EC2 servers
* Faster content delivery
* Improved scalability

Common use case:

* Web applications
* Backend services

---

# 20.4 CloudFront Integration with Application Load Balancer

In large-scale architectures, CloudFront is often connected to an **Application Load Balancer (ALB)**.

The ALB distributes incoming traffic to multiple EC2 instances.

Architecture example:

```text
User
 │
 ▼
CloudFront
 │
 ▼
Application Load Balancer
 │
 ▼
EC2 Instances
```

Benefits:

* Load balancing across multiple servers
* High availability
* Automatic scaling

Common use case:

```text
High-traffic web applications
```

---

# 20.5 CloudFront Integration with API Gateway

CloudFront can accelerate APIs built with **Amazon API Gateway**.

Architecture example:

```text
User
 │
 ▼
CloudFront
 │
 ▼
API Gateway
 │
 ▼
AWS Lambda
```

Benefits:

* Faster API responses
* Global API delivery
* Reduced latency

Common use case:

```text
Serverless APIs
```

---

# 20.6 CloudFront Integration with AWS Lambda

CloudFront integrates with **AWS Lambda** through **Lambda@Edge**.

Lambda functions can run at edge locations to modify requests and responses.

Architecture example:

```text
User
 │
 ▼
CloudFront
 │
 ▼
Lambda@Edge
 │
 ▼
Origin Server
```

Common use cases:

* Authentication
* Request validation
* URL rewriting
* Response modification

---

# 20.7 CloudFront Integration with AWS WAF

**AWS Web Application Firewall (WAF)** protects applications from malicious traffic.

Architecture example:

```text
User
 │
 ▼
AWS WAF
 │
 ▼
CloudFront
 │
 ▼
Origin Server
```

AWS WAF protects against:

* SQL injection
* Cross-site scripting (XSS)
* Bot attacks
* IP-based threats

---

# 20.8 CloudFront Integration with AWS Shield

CloudFront integrates with **AWS Shield** for **DDoS protection**.

Architecture example:

```text
User
 │
 ▼
AWS Shield
 │
 ▼
CloudFront
 │
 ▼
Origin Server
```

Types of AWS Shield:

* AWS Shield Standard
* AWS Shield Advanced

Benefits:

* Automatic DDoS mitigation
* Improved application availability

---

# 20.9 CloudFront Integration with Amazon Route 53

Amazon Route 53 is used for **DNS management**.

Route 53 directs users to CloudFront distributions.

Architecture example:

```text
User
 │
 ▼
Route 53 DNS
 │
 ▼
CloudFront Distribution
 │
 ▼
Origin Server
```

Benefits:

* Intelligent traffic routing
* High availability
* DNS-based load balancing

---

# 20.10 Example Full AWS Architecture

A typical production architecture may look like this:

```text
Users
 │
 ▼
Route 53 DNS
 │
 ▼
AWS WAF
 │
 ▼
CloudFront Distribution
 │
 ▼
Application Load Balancer
 │
 ▼
EC2 Instances
 │
 ▼
Database (RDS)
```

Static content may be served from:

```text
CloudFront → S3 Bucket
```

APIs may be served from:

```text
CloudFront → API Gateway → Lambda
```

---

# 20.11 Benefits of CloudFront Integration

Integrating CloudFront with AWS services provides several advantages.

### Improved Performance

Content is delivered from global edge locations.

---

### High Availability

Integration with load balancers ensures application reliability.

---

### Enhanced Security

Security services such as WAF and Shield protect applications.

---

### Cost Optimization

Caching reduces the number of requests reaching origin servers.

---

### Scalability

Applications can handle large traffic volumes.

---

# 20.12 Best Practices

### Use S3 for Static Content

Static files should be served through S3 with CloudFront caching.

---

### Use ALB for Dynamic Applications

ALB distributes traffic to EC2 instances.

---

### Protect Applications with AWS WAF

Block malicious traffic at the edge.

---

### Enable HTTPS

Always secure communication using SSL/TLS.

---

### Monitor with CloudWatch

Track CloudFront performance and traffic metrics.

---

# 20.13 Example Integrated Workflow

```text
User Request
      │
      ▼
Route 53 DNS
      │
      ▼
CloudFront Edge Location
      │
      ▼
AWS WAF Security Check
      │
      ▼
Origin Server
 ├── S3 Bucket
 ├── ALB → EC2
 └── API Gateway → Lambda
```

---

# 20.14 Key Advantages

* Faster global content delivery
* Secure application architecture
* High scalability
* Seamless AWS integration

---
---
# 21. CloudFront Real-World Use Cases
---

## 21.1 Overview

**Amazon CloudFront** is widely used in real-world production environments to deliver content quickly and securely across the globe.

Organizations use CloudFront for:

* Video streaming platforms
* Static website hosting
* API acceleration
* E-commerce websites
* Software download distribution
* Gaming platforms

These use cases demonstrate how CloudFront improves **performance, scalability, and user experience**.

---

# 21.2 Video Streaming Platforms

One of the most common uses of CloudFront is **video streaming**.

Streaming platforms need to deliver large video files to millions of users worldwide with minimal buffering.

### Example Architecture

```text
Users
 │
 ▼
CloudFront Edge Locations
 │
 ▼
Media Storage (S3)
 │
 ▼
Video Streaming Delivered
```

CloudFront caches video segments at edge locations, allowing users to stream content from nearby servers.

### Real Example

Streaming services such as:

* Netflix-like platforms
* Online education platforms
* Live streaming websites

use CDN technology to distribute media globally.

### Benefits

* Reduced video buffering
* Faster playback start time
* Global scalability

---

# 21.3 Static Website Hosting

CloudFront is commonly used to deliver **static websites hosted on Amazon S3**.

Static websites include files such as:

* HTML
* CSS
* JavaScript
* Images

### Architecture Example

```text
User
 │
 ▼
CloudFront
 │
 ▼
Amazon S3 Static Website
```

### Use Cases

* Personal websites
* Company landing pages
* Documentation portals
* Portfolio websites

### Benefits

* Faster global page loading
* Reduced server load
* High availability

---

# 21.4 API Acceleration

CloudFront can accelerate APIs by caching responses and routing requests through the AWS global network.

### Architecture Example

```text
User
 │
 ▼
CloudFront
 │
 ▼
API Gateway
 │
 ▼
Lambda Function
```

### Use Cases

* Mobile applications
* SaaS platforms
* Serverless APIs

### Benefits

* Faster API response time
* Reduced backend load
* Improved global performance

---

# 21.5 E-Commerce Platforms

E-commerce websites often serve millions of users globally.

CloudFront helps deliver:

* Product images
* CSS and JavaScript files
* API responses

### Architecture Example

```text
Users
 │
 ▼
CloudFront
 │
 ▼
Application Load Balancer
 │
 ▼
EC2 Web Servers
 │
 ▼
Database
```

### Real Examples

Large e-commerce platforms such as:

* Amazon-style stores
* Online retail platforms

use CDNs to improve performance during high traffic events.

### Benefits

* Faster page loading
* Better user experience
* Handling traffic spikes during sales

---

# 21.6 Software Distribution

Many companies use CloudFront to distribute **software packages, updates, and downloads**.

Examples include:

* Operating system updates
* Mobile app downloads
* Game updates
* Software installers

### Architecture Example

```text
Users
 │
 ▼
CloudFront
 │
 ▼
S3 Storage
 │
 ▼
Software Download
```

### Benefits

* Faster global downloads
* Reduced bandwidth costs
* Reliable distribution network

---

# 21.7 Gaming Platforms

Gaming platforms often deliver large files such as:

* Game updates
* Downloadable content (DLC)
* Patch files

### Architecture Example

```text
Players
 │
 ▼
CloudFront
 │
 ▼
Game Content Storage (S3)
```

### Benefits

* Faster game updates
* Reduced download time
* Global availability

---

# 21.8 News and Media Websites

News websites experience traffic spikes when major events occur.

CloudFront helps deliver content quickly during these spikes.

### Architecture Example

```text
Users
 │
 ▼
CloudFront
 │
 ▼
Web Servers
 │
 ▼
Content Management System
```

### Benefits

* Handle sudden traffic surges
* Faster article loading
* Improved reader experience

---

# 21.9 Online Learning Platforms

Educational platforms use CloudFront to deliver:

* Course videos
* Learning materials
* PDFs and documents

### Architecture Example

```text
Students
 │
 ▼
CloudFront
 │
 ▼
S3 Course Content
```

### Benefits

* Faster video streaming
* Improved accessibility worldwide

---

# 21.10 SaaS Applications

Many SaaS platforms use CloudFront to accelerate web applications.

Examples include:

* CRM platforms
* Collaboration tools
* Cloud dashboards

### Architecture Example

```text
Users
 │
 ▼
CloudFront
 │
 ▼
Application Load Balancer
 │
 ▼
EC2 / Containers
```

### Benefits

* Improved application performance
* Reduced latency
* Better user experience

---

# 21.11 Global Content Delivery Architecture

Example production architecture:

```text
Users Worldwide
 │
 ▼
Route 53 DNS
 │
 ▼
CloudFront Distribution
 │
 ▼
AWS WAF
 │
 ▼
Application Load Balancer
 │
 ▼
EC2 Instances
 │
 ▼
Database
```

Static content delivery:

```text
CloudFront → Amazon S3
```

API delivery:

```text
CloudFront → API Gateway → Lambda
```

---

# 21.12 Advantages of Using CloudFront in Real Applications

### Global Performance

Content is delivered from the nearest edge location.

---

### Scalability

CloudFront handles millions of requests automatically.

---

### Cost Efficiency

Caching reduces infrastructure and bandwidth costs.

---

### Security

Integration with AWS security services protects applications.

---

# 21.13 Summary

CloudFront is used in many real-world applications including:

* Video streaming platforms
* Static websites
* APIs and mobile applications
* E-commerce platforms
* Software distribution systems

These use cases demonstrate the **power and flexibility of CloudFront in modern cloud architectures**.

---
---
# 22. CloudFront Hands-on Practical Guide
---

## 22.1 Overview

This section provides a **step-by-step practical implementation** of **Amazon CloudFront** using a static website hosted on **Amazon S3**.

In this lab you will learn how to:

1. Create an S3 bucket for a static website
2. Upload website files
3. Create a CloudFront distribution
4. Configure the origin server
5. Enable HTTPS
6. Test content delivery through CloudFront

This is one of the **most common real-world DevOps implementations**.

---

# 22.2 Architecture for the Practical

```text
User
 │
 ▼
CloudFront Distribution
 │
 ▼
Amazon S3 Bucket
 │
 ▼
Static Website Files
```

Users access the website through **CloudFront**, which caches content at edge locations.

---

# 22.3 Step 1 – Create an S3 Bucket

1. Login to AWS Management Console
2. Open **S3 Service**
3. Click **Create Bucket**

Configuration example:

```text
Bucket Name: my-cloudfront-demo-site
Region: us-east-1
```

---

## Disable Public Access Block

To allow website access:

1. Go to **Block Public Access Settings**
2. Disable the following options:

```text
Block all public access
```

---

# 22.4 Step 2 – Upload Website Files

Upload your static website files such as:

```text
index.html
style.css
logo.png
```

Steps:

1. Open your S3 bucket
2. Click **Upload**
3. Select files
4. Upload

Example file structure:

```text
my-cloudfront-demo-site
 ├── index.html
 ├── css/
 │     └── style.css
 └── images/
       └── logo.png
```

---

# 22.5 Step 3 – Enable Static Website Hosting

1. Open **Bucket Properties**
2. Scroll to **Static Website Hosting**
3. Enable hosting

Configuration example:

```text
Index Document: index.html
Error Document: error.html
```

After enabling, S3 generates a website endpoint.

Example:

```text
http://my-cloudfront-demo-site.s3-website-us-east-1.amazonaws.com
```

---

# 22.6 Step 4 – Create CloudFront Distribution

1. Open **CloudFront Service**
2. Click **Create Distribution**

---

## Origin Configuration

Select the S3 bucket as the origin.

Example:

```text
Origin Domain:
my-cloudfront-demo-site.s3.amazonaws.com
```

---

## Default Cache Behavior

Example configuration:

```text
Viewer Protocol Policy: Redirect HTTP to HTTPS
Allowed HTTP Methods: GET, HEAD
Cache Policy: CachingOptimized
```

---

## Distribution Settings

Example configuration:

```text
Alternate Domain Name (CNAME): cdn.example.com
Default Root Object: index.html
```

---

# 22.7 Step 5 – Enable HTTPS

To enable HTTPS for a custom domain:

1. Open **AWS Certificate Manager (ACM)**
2. Request a new certificate

Example domain:

```text
cdn.example.com
```

After validation:

1. Attach the certificate to CloudFront distribution
2. Enable HTTPS

---

# 22.8 Step 6 – Deploy CloudFront Distribution

After configuration:

1. Click **Create Distribution**
2. CloudFront deployment starts

Deployment time:

```text
5 – 15 minutes
```

Once completed, CloudFront provides a domain name.

Example:

```text
d123abcd.cloudfront.net
```

---

# 22.9 Step 7 – Test the CloudFront Website

Open a browser and test the distribution domain.

Example:

```text
https://d123abcd.cloudfront.net
```

The content should load from **CloudFront edge locations**.

---

# 22.10 Verify Caching

Test caching using multiple requests.

Example workflow:

```text
User Request
      │
      ▼
CloudFront Edge Location
      │
      ▼
Cache Hit
      │
      ▼
Content Delivered Quickly
```

You can verify caching using browser developer tools.

---

# 22.11 Optional Step – Configure Custom Domain

If using a custom domain:

Example:

```text
cdn.example.com
```

Steps:

1. Open **Route 53**
2. Create a **CNAME record**

Example DNS record:

```text
cdn.example.com → d123abcd.cloudfront.net
```

Now users can access the website using the custom domain.

---

# 22.12 Optional Step – Configure Cache Invalidation

If you update files in S3:

Example:

```text
index.html updated
```

Create an invalidation request.

Example:

```text
/index.html
```

This clears the cached version from edge locations.

---

# 22.13 Example Production Architecture

```text
Users Worldwide
 │
 ▼
Route 53 DNS
 │
 ▼
CloudFront Distribution
 │
 ▼
S3 Static Website
```

For dynamic applications:

```text
CloudFront
 │
 ▼
Application Load Balancer
 │
 ▼
EC2 Instances
```

---

# 22.14 Common Issues in the Lab

### Access Denied Error

Cause:

```text
S3 bucket permissions not configured correctly
```

Solution:

```text
Allow public access or use OAC/OAI
```

---

### 403 Forbidden Error

Cause:

```text
Incorrect origin configuration
```

Solution:

```text
Verify origin domain and permissions
```

---

### Content Not Updating

Cause:

```text
Cached content in CloudFront
```

Solution:

```text
Create cache invalidation
```

---

# 22.15 Benefits of Using CloudFront in This Lab

* Faster website loading
* Reduced latency
* Global CDN distribution
* Improved scalability
* Secure HTTPS delivery

---

# 22.16 Summary

In this practical lab you learned how to:

* Create an S3 static website
* Configure CloudFront distribution
* Enable HTTPS
* Deliver content through edge locations

This is a **common production architecture used for modern web applications**.

---
---
# 23. CloudFront vs Other CDN Services

## 23.1 Overview

A **Content Delivery Network (CDN)** improves application performance by delivering content from servers closer to users.

Many CDN providers exist in the market. The most widely used include:

* **Amazon CloudFront**
* **Cloudflare**
* **Akamai**
* **Fastly**

Each CDN offers different features, pricing models, and infrastructure.

Understanding these differences helps organizations choose the best CDN for their needs.

---

# 23.2 What is a CDN

A CDN distributes content through a global network of servers.

Basic architecture:

```text
User
 │
 ▼
Nearest CDN Edge Server
 │
 ▼
Cached Content
 │
 ▼
Origin Server
```

This reduces latency and improves application performance.

---

# 23.3 CloudFront vs Cloudflare

| Feature      | CloudFront                | Cloudflare                 |
| ------------ | ------------------------- | -------------------------- |
| Provider     | AWS                       | Independent CDN provider   |
| Integration  | Deep AWS integration      | Multi-cloud support        |
| Edge Network | Large global network      | Very large global network  |
| Security     | AWS WAF, Shield           | Built-in security services |
| Setup        | AWS console configuration | Simple dashboard setup     |
| Pricing      | Pay-as-you-go             | Free and paid plans        |

### When to Use CloudFront

* Applications hosted in AWS
* Tight AWS integration needed
* Enterprise cloud environments

### When to Use Cloudflare

* Multi-cloud environments
* Smaller websites
* Free CDN solutions

---

# 23.4 CloudFront vs Akamai

Akamai is one of the oldest CDN providers and is widely used by large enterprises.

| Feature        | CloudFront         | Akamai                 |
| -------------- | ------------------ | ---------------------- |
| Infrastructure | AWS global network | Massive global network |
| Integration    | AWS services       | Independent platform   |
| Pricing        | Pay-as-you-go      | Enterprise pricing     |
| Deployment     | Self-service       | Enterprise setup       |
| Scalability    | High               | Extremely high         |

### When to Use CloudFront

* AWS-based applications
* Startup and mid-size applications

### When to Use Akamai

* Large global enterprises
* Media companies
* Global streaming services

---

# 23.5 CloudFront vs Fastly

Fastly is a modern CDN designed for high-performance edge computing.

| Feature                 | CloudFront    | Fastly                   |
| ----------------------- | ------------- | ------------------------ |
| Edge Computing          | Lambda@Edge   | Advanced edge computing  |
| Performance             | Very fast     | Extremely fast           |
| Real-time configuration | Limited       | Very flexible            |
| Integration             | AWS ecosystem | Multi-cloud environments |
| Pricing                 | Pay-as-you-go | Usage-based pricing      |

### When to Use CloudFront

* AWS-hosted applications
* Standard CDN workloads

### When to Use Fastly

* Advanced edge computing needs
* Real-time application control

---

# 23.6 CDN Architecture Comparison

### CloudFront Architecture

```text
Users
 │
 ▼
CloudFront Edge Locations
 │
 ▼
Regional Edge Cache
 │
 ▼
Origin Server
```

---

### Cloudflare Architecture

```text
Users
 │
 ▼
Cloudflare Edge Network
 │
 ▼
Security Layer
 │
 ▼
Origin Server
```

---

### Akamai Architecture

```text
Users
 │
 ▼
Akamai Edge Servers
 │
 ▼
Caching Layer
 │
 ▼
Origin Server
```

---

# 23.7 Performance Comparison

| CDN Provider | Performance    | Global Coverage      |
| ------------ | -------------- | -------------------- |
| CloudFront   | Very high      | Large global network |
| Cloudflare   | Very high      | Very large network   |
| Akamai       | Extremely high | Largest network      |
| Fastly       | Extremely high | Large network        |

All major CDNs deliver excellent performance, but their strengths vary depending on architecture and integration.

---

# 23.8 Security Comparison

| Security Feature         | CloudFront | Cloudflare          | Akamai                |
| ------------------------ | ---------- | ------------------- | --------------------- |
| DDoS Protection          | AWS Shield | Built-in protection | Enterprise protection |
| Web Application Firewall | AWS WAF    | Cloudflare WAF      | Akamai WAF            |
| TLS Encryption           | Supported  | Supported           | Supported             |
| Bot Protection           | Available  | Advanced            | Advanced              |

---

# 23.9 Pricing Comparison

| CDN Provider | Pricing Model       |
| ------------ | ------------------- |
| CloudFront   | Pay-as-you-go       |
| Cloudflare   | Free + paid plans   |
| Akamai       | Enterprise pricing  |
| Fastly       | Usage-based pricing |

CloudFront pricing is flexible and integrates with AWS billing.

---

# 23.10 When to Choose CloudFront

CloudFront is best suited for:

* Applications hosted on AWS
* Serverless architectures
* Static website hosting on S3
* API acceleration using API Gateway
* High scalability workloads

Example architecture:

```text
Users
 │
 ▼
Route 53
 │
 ▼
CloudFront
 │
 ▼
S3 / ALB / API Gateway
```

---

# 23.11 Advantages of CloudFront

* Deep integration with AWS services
* Global edge location network
* Built-in DDoS protection
* High scalability
* Flexible pricing model

---

# 23.12 Limitations of CloudFront

* Less flexible than some third-party CDNs
* Advanced configuration can be complex
* Some features require additional AWS services

---

# 23.13 Summary

Each CDN provider serves different use cases.

* **CloudFront** → Best for AWS-based architectures
* **Cloudflare** → Best for multi-cloud and small websites
* **Akamai** → Best for large global enterprises
* **Fastly** → Best for advanced edge computing

Choosing the right CDN depends on:

* Application architecture
* Performance requirements
* Budget
* Cloud platform

---
---
# 24. CloudFront Interview Questions (50 Questions with Answers)
---

## 24.1 Basic CloudFront Interview Questions

### 1. What is Amazon CloudFront?

Amazon CloudFront is a **Content Delivery Network (CDN)** service provided by AWS that delivers content such as websites, APIs, videos, and images with **low latency and high transfer speeds** using a global network of edge locations.

---

### 2. What is a CDN?

A **Content Delivery Network (CDN)** is a distributed network of servers that cache and deliver content closer to users to reduce latency and improve performance.

---

### 3. What are Edge Locations in CloudFront?

Edge locations are **data centers located worldwide** where CloudFront caches content to deliver it faster to users.

---

### 4. What is a CloudFront Distribution?

A **CloudFront Distribution** is the configuration that defines how content is delivered to users through CloudFront.

---

### 5. What is an Origin in CloudFront?

An **Origin** is the location where the original content is stored. CloudFront fetches content from the origin when it is not available in the cache.

Examples:

* Amazon S3
* EC2 instances
* Application Load Balancer
* API Gateway

---

### 6. What is Cache Hit?

A **Cache Hit** occurs when the requested content is already stored in the CloudFront edge location and can be delivered directly.

---

### 7. What is Cache Miss?

A **Cache Miss** occurs when content is not available in the edge cache and must be fetched from the origin server.

---

### 8. What is TTL in CloudFront?

**TTL (Time To Live)** defines how long an object remains in the CloudFront cache before it expires.

---

### 9. What is CloudFront used for?

CloudFront is used for:

* Website acceleration
* Video streaming
* API acceleration
* Software distribution
* Global content delivery

---

### 10. What types of content can CloudFront deliver?

CloudFront can deliver:

* Static content (images, CSS, JavaScript)
* Dynamic content (APIs, web applications)
* Streaming media

---

# 24.2 Intermediate CloudFront Interview Questions

### 11. What is a Cache Behavior?

Cache behavior defines how CloudFront handles requests based on URL path patterns.

Example:

```
/images/* → S3
/api/* → API Gateway
```

---

### 12. What is Cache Invalidation?

Cache invalidation removes cached content from edge locations before TTL expires.

---

### 13. What is an Origin Access Identity (OAI)?

OAI allows CloudFront to securely access an S3 bucket while preventing direct access to the bucket.

---

### 14. What is Origin Access Control (OAC)?

OAC is a newer mechanism that allows CloudFront to securely access origins using signed requests.

---

### 15. What is Geo Restriction?

Geo restriction limits access to content based on user geographic location.

---

### 16. What is Lambda@Edge?

Lambda@Edge allows running **AWS Lambda functions at CloudFront edge locations** to modify requests and responses.

---

### 17. What are CloudFront Functions?

CloudFront Functions are lightweight JavaScript functions used to modify requests and responses at edge locations.

---

### 18. What is the difference between Lambda@Edge and CloudFront Functions?

| Feature         | CloudFront Functions | Lambda@Edge      |
| --------------- | -------------------- | ---------------- |
| Execution speed | Very fast            | Slightly slower  |
| Complexity      | Simple logic         | Complex logic    |
| Runtime         | JavaScript           | Node.js / Python |

---

### 19. What is a Signed URL?

A **Signed URL** provides temporary access to private CloudFront content.

---

### 20. What are Signed Cookies?

Signed cookies allow access to multiple restricted files without generating separate signed URLs.

---

# 24.3 Advanced CloudFront Interview Questions

### 21. What is a Cache Policy?

A cache policy defines caching behavior including TTL settings and cache key configuration.

---

### 22. What is an Origin Request Policy?

An origin request policy controls which headers, cookies, and query strings are forwarded to the origin server.

---

### 23. What is a Response Headers Policy?

A response headers policy adds or modifies HTTP headers in responses sent to users.

---

### 24. What is CloudFront Logging?

CloudFront logging records request information and stores it in **Amazon S3** for analysis.

---

### 25. What is Real-Time Logging?

Real-time logging streams request logs to **Amazon Kinesis Data Streams** for immediate analysis.

---

### 26. What is AWS Shield?

AWS Shield provides **DDoS protection** for CloudFront applications.

---

### 27. What is AWS WAF?

AWS WAF protects web applications from attacks such as:

* SQL injection
* Cross-site scripting

---

### 28. What is CloudFront Regional Edge Cache?

Regional edge caches store less frequently accessed content between edge locations and origin servers.

---

### 29. What is a Viewer Request Event?

A viewer request event occurs when CloudFront receives a request from a user.

---

### 30. What is an Origin Request Event?

An origin request event occurs when CloudFront forwards a request to the origin server.

---

# 24.4 Scenario-Based Interview Questions

### 31. How would you accelerate a static website globally?

Use:

```
S3 → CloudFront → Users
```

---

### 32. How do you secure an S3 bucket behind CloudFront?

Use **Origin Access Control (OAC)** or **Origin Access Identity (OAI)**.

---

### 33. How do you restrict access to CloudFront content?

Use:

* Signed URLs
* Signed Cookies
* AWS WAF

---

### 34. How can you update cached content immediately?

Use **CloudFront cache invalidation**.

---

### 35. How do you block users from specific countries?

Use **CloudFront Geo Restrictions**.

---

### 36. How do you improve cache hit ratio?

* Optimize cache policies
* Increase TTL values
* Reduce cookie forwarding

---

### 37. How do you monitor CloudFront performance?

Use:

* CloudWatch metrics
* Access logs
* Real-time logs

---

### 38. How do you enable HTTPS in CloudFront?

Attach an SSL certificate using **AWS Certificate Manager (ACM)**.

---

### 39. How do you route traffic to different origins?

Use **Cache Behaviors with path patterns**.

Example:

```
/images/* → S3
/api/* → API Gateway
```

---

### 40. How do you handle traffic spikes with CloudFront?

CloudFront automatically scales using its global edge network.

---

# 24.5 Expert-Level Interview Questions

### 41. What is the difference between CloudFront and an Application Load Balancer?

| Feature          | CloudFront | ALB            |
| ---------------- | ---------- | -------------- |
| Purpose          | CDN        | Load balancing |
| Content delivery | Global     | Regional       |
| Caching          | Yes        | No             |

---

### 42. What is the difference between CloudFront and S3 static website hosting?

S3 hosts static content, while CloudFront accelerates delivery using global edge locations.

---

### 43. How does CloudFront reduce origin server load?

By caching frequently requested content at edge locations.

---

### 44. What are CloudFront edge locations?

Global data centers that store cached content and deliver it to users.

---

### 45. How does CloudFront determine the nearest edge location?

CloudFront uses DNS routing and network latency measurements.

---

### 46. What happens when TTL expires?

CloudFront checks the origin server for updated content.

---

### 47. What is origin failover?

CloudFront can switch to a secondary origin if the primary origin fails.

---

### 48. What are common CloudFront errors?

Examples:

```
403 Forbidden
404 Not Found
502 Bad Gateway
503 Service Unavailable
504 Gateway Timeout
```

---

### 49. What services integrate with CloudFront?

Common integrations include:

* Amazon S3
* EC2
* Application Load Balancer
* API Gateway
* AWS Lambda
* AWS WAF
* AWS Shield

---

### 50. What are the advantages of using CloudFront?

Advantages include:

* Global content delivery
* Reduced latency
* High scalability
* Improved security
* Integration with AWS services

---
