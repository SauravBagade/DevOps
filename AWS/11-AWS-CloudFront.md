---
AWS-CloudFront
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
  


This will make your **CloudFront documentation look like official AWS documentation.**
