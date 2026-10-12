# Types of APIs (Interview Notes)

APIs allow different applications to communicate with each other. Choosing the right API architecture depends on the application's requirements.

---

# 1. REST API (HTTP/HTTPS)

## What is it?

REST (Representational State Transfer) is the most widely used API architecture. It uses HTTP/HTTPS methods to perform operations on resources.

**Common Methods**

- GET → Read
- POST → Create
- PUT/PATCH → Update
- DELETE → Delete

## Example

```http
GET /users/5 HTTP/1.1
Host: api.example.com
```

Response:

```json
{
  "id": 5,
  "name": "John"
}
```

## When to Use

- Web applications
- Mobile applications
- Public APIs
- Standard CRUD operations

## Why Choose REST?

- Simple and easy to understand
- JSON is lightweight and human-readable
- Excellent browser and mobile support
- Huge ecosystem and community
- Easy to test using tools like Postman

**Examples**

- GitHub API
- Stripe API
- OpenWeather API

---

# 2. SOAP API

## What is it?

SOAP (Simple Object Access Protocol) is a protocol that exchanges data using XML and follows strict standards.

## Example

Request:

```xml
<soap:Envelope>
    <soap:Body>
        <GetUser>
            <Id>5</Id>
        </GetUser>
    </soap:Body>
</soap:Envelope>
```

Response:

```xml
<User>
    <Id>5</Id>
    <Name>John</Name>
</User>
```

## When to Use

- Banking systems
- Government services
- Enterprise software
- Systems requiring strict contracts

## Why Choose SOAP?

- Strong security standards (WS-Security)
- Built-in error handling
- Strict contract using WSDL
- High reliability for enterprise integrations

**Examples**

- Banking
- Insurance
- Payment processing
- Legacy enterprise systems

---

# 3. GraphQL

## What is it?

GraphQL is a query language for APIs where the client requests exactly the data it needs.

Instead of multiple endpoints, GraphQL typically exposes a single endpoint.

## Example

Query:

```graphql
{
  user(id: 5) {
    name
    email
  }
}
```

Response:

```json
{
  "data": {
    "user": {
      "name": "John",
      "email": "john@example.com"
    }
  }
}
```

## When to Use

- Complex dashboards
- Mobile applications
- Multiple frontend clients
- Nested or related data

## Why Choose GraphQL?

- Avoids over-fetching and under-fetching
- Single endpoint for all queries
- Reduces the number of API requests
- Frontend has full control over requested fields

**Examples**

- Facebook
- GitHub GraphQL API
- Shopify

---

# 4. gRPC

## What is it?

gRPC (Google Remote Procedure Call) is a high-performance communication framework that uses Protocol Buffers (protobuf) instead of JSON.

## Example

```proto
service UserService {
    rpc GetUser(UserRequest) returns (UserResponse);
}
```

Client:

```text
GetUser(id=5)
```

Response:

```text
id: 5
name: John
```

## When to Use

- Microservices
- Internal backend communication
- Real-time applications
- High-performance distributed systems

## Why Choose gRPC?

- Extremely fast (binary serialization)
- Smaller payload than JSON
- Supports streaming (client, server, bidirectional)
- Strongly typed contracts using `.proto` files
- Ideal for service-to-service communication

**Examples**

- Google Cloud
- Kubernetes
- Netflix-style microservices
- Internal communication between backend services

---

# Quick Comparison

| Feature | REST | SOAP | GraphQL | gRPC |
|----------|------|------|----------|-------|
| Data Format | JSON | XML | JSON | Protocol Buffers |
| Transport | HTTP/HTTPS | HTTP, SMTP, etc. | HTTP/HTTPS | HTTP/2 |
| Speed | Fast | Slow | Fast | Very Fast |
| Learning Curve | Easy | Hard | Medium | Medium |
| Best For | Web & Mobile APIs | Enterprise Systems | Flexible Frontends | Microservices |
| Multiple Endpoints | Yes | Yes | Usually One | Service Methods |

---

# Interview Answer (When the interviewer asks "Which one would you choose and why?")

| Scenario | Choose | Reason |
|----------|--------|--------|
| Public Web API | REST | Simple, widely adopted, easy for clients to consume. |
| Banking / Government | SOAP | Strong security, strict contracts, and reliability. |
| React/Flutter Dashboard | GraphQL | Client fetches only the required data, reducing API calls. |
| Internal Microservices | gRPC | High performance, low latency, efficient binary communication. |

---

# One-Line Memory Trick

- **REST** → Simple JSON APIs for web and mobile.
- **SOAP** → Secure XML APIs for enterprise systems.
- **GraphQL** → Client asks for exactly the data it needs.
- **gRPC** → Fast binary communication between backend services.