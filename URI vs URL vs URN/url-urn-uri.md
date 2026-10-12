# Understanding URI vs URL vs URN

## Introduction

When working with web development, REST APIs, or networking, you'll often hear the terms **URI**, **URL**, and **URN**. They are related but not identical.

A simple way to remember them is:

- **URI** = Identity
- **URL** = Identity + Location
- **URN** = Identity + Name (No Location)

---

# Relationship

```
            URI
           /   \
        URL    URN
```

- Every **URL** is a **URI**.
- Every **URN** is a **URI**.
- But not every URI is a URL or URN.

---

# 1. URI (Uniform Resource Identifier)

A **URI** is a string that uniquely identifies a resource.

It does **not** necessarily tell you where the resource is.

Examples:

```text
https://example.com
ftp://example.com/file.zip
mailto:admin@example.com
urn:isbn:9780134685991
```

Think of URI as the **general concept of identifying something**.

---

# 2. URL (Uniform Resource Locator)

A **URL** identifies a resource **and** tells you **where it is** and **how to access it**.

Example:

```text
https://api.example.com/users/15
```

Breakdown:

```
https://api.example.com/users/15
│      │               │
│      │               └── Path
│      │
│      └────────────────── Domain
│
└───────────────────────── Protocol
```

Meaning:

- Protocol: HTTPS
- Domain: api.example.com
- Resource Path: /users/15

A URL provides both the identity and the location of the resource.

---

# 3. URN (Uniform Resource Name)

A **URN** uniquely identifies a resource using a permanent name.

Unlike a URL, it **does not tell you where the resource is located.**

Example:

```text
urn:isbn:9780134685991
```

This identifies a particular book by its ISBN.

It does **not** specify whether the book is on:

- Amazon
- Google Books
- A university library
- A PDF server

It only identifies the book itself.

---

# URN Structure

General format:

```text
urn:<Namespace Identifier>:<Namespace Specific String>
```

Example:

```text
urn:isbn:9780134685991
```

Breakdown:

```
urn:isbn:9780134685991
│   │           │
│   │           └── Namespace Specific String (NSS)
│   │
│   └────────────── Namespace Identifier (NID)
│
└────────────────── URN Scheme
```

---

## Part 1: `urn`

```
urn:
```

This is called the **scheme**.

It tells the computer:

> This is a Uniform Resource Name.

Similar schemes:

```
https:
ftp:
mailto:
file:
urn:
```

---

## Part 2: `isbn`

```
urn:isbn:...
```

This is the **Namespace Identifier (NID)**.

It specifies which naming system is being used.

Examples:

| Namespace | Meaning |
|-----------|----------|
| isbn | Books |
| uuid | UUID identifiers |
| ietf | RFC documents |
| oid | Object Identifiers |

---

## Part 3: `9780134685991`

This is the **Namespace Specific String (NSS).**

Its format depends on the namespace.

For ISBN, it is simply the book's ISBN number.

```
urn:isbn:9780134685991
```

Meaning:

> The book identified by ISBN `9780134685991`.

Nothing more.

---

# Another URN Example

```
urn:uuid:550e8400-e29b-41d4-a716-446655440000
```

Breakdown:

```
urn
│
├── uuid
│     │
│     └── Namespace
│
└── 550e8400-e29b-41d4-a716-446655440000
      │
      └── UUID value
```

This identifies one unique object.

It does **not** tell you where that object is stored.

---

# URL vs URN

## URL

```
https://example.com/books/9780134685991
```

Meaning:

- Resource exists on example.com
- Accessible via HTTPS
- Located at `/books/9780134685991`

---

## URN

```
urn:isbn:9780134685991
```

Meaning:

- The resource is the book with this ISBN.
- No location information.
- No access method.

---

# Real-Life Analogy

Imagine a person named John.

## URN

```
Passport Number:
AB1234567
```

This uniquely identifies John anywhere.

---

## URL

```
Home Address:
221B Baker Street
```

This tells you where John currently lives.

If John moves:

- Passport number remains the same.
- Address changes.

That's exactly how URNs and URLs differ.

---

# Common URN Examples

## Book

```
urn:isbn:9780134685991
```

---

## UUID

```
urn:uuid:550e8400-e29b-41d4-a716-446655440000
```

---

## RFC Document

```
urn:ietf:rfc:3986
```

Identifies RFC 3986 regardless of where it is hosted.

---

# Where Are URNs Used?

URNs are commonly used in:

- ISBN (Books)
- UUID identifiers
- RFC documents
- XML namespaces
- Digital libraries
- Archive systems
- Telecommunications

---

# Do We Use URNs in Django or REST APIs?

Almost never.

Most backend development uses URLs.

Example:

```
GET https://api.example.com/users/25
```

or

```
GET https://api.example.com/orders/150
```

Because clients need to know **where** to send requests.

URNs only identify resources; they don't provide a way to access them.

---

# Quick Comparison

| Feature | URI | URL | URN |
|----------|-----|-----|-----|
| Full Form | Uniform Resource Identifier | Uniform Resource Locator | Uniform Resource Name |
| Identifies Resource | ✅ | ✅ | ✅ |
| Gives Location | ❌ (Not necessarily) | ✅ | ❌ |
| Gives Access Method | ❌ | ✅ | ❌ |
| Permanent Identifier | Sometimes | No | Yes |
| Common in Web Development | ✅ | ✅ | Rare |

---

# Easy Way to Remember

```
URI
= Identity

URL
= Identity + Location

URN
= Identity + Name
```

---

# Final Example

### URI

```
urn:isbn:9780134685991
```

Identifies a book.

---

### URL

```
https://books.example.com/isbn/9780134685991
```

Shows where that book can be accessed.

---

### URN

```
urn:isbn:9780134685991
```

The identifier remains the same even if the book moves to another website.

---

# Summary

- A **URI** is the general concept of identifying a resource.
- A **URL** identifies a resource **and tells you where and how to access it**.
- A **URN** identifies a resource by a **permanent name**, independent of its location.

In everyday backend development (Django, FastAPI, Spring Boot, Node.js, etc.), you'll use **URLs** almost exclusively. Understanding **URNs** is mainly useful for standards, documentation, and technical interviews.