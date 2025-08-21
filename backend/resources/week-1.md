# Backend Internship: Week 1 – Express + Prisma

## Week 1 Overview
**Goal:** In this first week, you will learn the fundamentals of building a backend application. The focus will be on understanding HTTP semantics, mastering asynchronous and concurrent programming in JavaScript, and using a modern framework (Express.js) with an ORM (Prisma) and a relational database (PostgreSQL) to build a complete API. By the end of the week, you will have shipped a full CRUD API.

---

## Day 1: JS/TS + HTTP Request Types
### Concepts
Understand the core principles of the web:
- **HTTP Methods:** Learn the purpose and behavior of GET, POST, PUT, PATCH, and DELETE. Understand the concept of **idempotency**.
- **Status Codes:** Recognize common status codes and their meanings (e.g., `200 OK`, `201 Created`, `404 Not Found`, `500 Internal Server Error`).
- **Headers:** Learn about request and response headers and their roles, including `Content-Type` and **authorization headers**.
- **Request Lifecycle:** Follow the journey of an HTTP request from the client to the server and back to the client.

### Task
Create a simple in-memory API for `/api/product` that supports all five HTTP verbs. The product should have an `id` and a `name`.

### Resources
| Topic | Resource Link |
| :--- | :--- |
| HTTP Methods & Status Codes | [MDN Web Docs: HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP) |
| HTTP Headers | [MDN Web Docs: HTTP Headers](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers) |
| Request Lifecycle | [How the Web Works: HTTP and the Browser](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/How_the_Web_works) |


#### Example Code
```js
import express from "express";

const app = express();
app.use(express.json());

let products = [{ id: 1, name: "Book" }];

// GET all
app.get("/api/product", (req, res) => {
  res.json(products);
});

// GET by id
app.get("/api/product/:id", (req, res) => {
  const product = products.find(p => p.id == req.params.id);
  if (!product) return res.status(404).json({ error: "Not Found" });
  res.json(product);
});

// POST
app.post("/api/product", (req, res) => {
  const newProduct = { id: Date.now(), name: req.body.name };
  products.push(newProduct);
  res.status(201).json(newProduct);
});

// PUT (replace)
app.put("/api/product/:id", (req, res) => {
  const idx = products.findIndex(p => p.id == req.params.id);
  if (idx === -1) return res.status(404).json({ error: "Not Found" });
  products[idx] = { id: products[idx].id, name: req.body.name };
  res.json(products[idx]);
});

// PATCH (partial update)
app.patch("/api/product/:id", (req, res) => {
  const product = products.find(p => p.id == req.params.id);
  if (!product) return res.status(404).json({ error: "Not Found" });
  if (req.body.name) product.name = req.body.name;
  res.json(product);
});

// DELETE
app.delete("/api/product/:id", (req, res) => {
  products = products.filter(p => p.id != req.params.id);
  res.status(204).end();
});

app.listen(3000, () => console.log("Server running on http://localhost:3000"));
```
---

## Day 2: Async & Concurrency
### Concepts
Master asynchronous operations in JavaScript:
- **`async`/`await`:** Learn the modern syntax for handling promises.
- **Promise Methods:** Differentiate between `Promise.all()`, `Promise.race()`, `Promise.allSettled()`, and `Promise.any()` and understand when to use each.
- **Concurrency Control:** Implement timeouts with `AbortController` and strategies like backoff and jitter.

### Task
Build an aggregator that hits three different public APIs. Control the parallelism of these requests and log the timing of each one.

### Example Code
```js
import fetch from "node-fetch";

// helper with timeout
async function fetchWithTimeout(url, timeout = 5000) {
  const controller = new AbortController();
  const id = setTimeout(() => controller.abort(), timeout);
  try {
    const res = await fetch(url, { signal: controller.signal });
    return await res.json();
  } finally {
    clearTimeout(id);
  }
}

async function aggregator() {
  const urls = [
    "https://jsonplaceholder.typicode.com/posts/1",
    "https://jsonplaceholder.typicode.com/users/1",
    "https://jsonplaceholder.typicode.com/todos/1",
  ];

  console.time("All Requests");
  const results = await Promise.all(urls.map(u => fetchWithTimeout(u, 3000)));
  console.timeEnd("All Requests");

  console.log(results);
}

// Example usage
aggregator();
```

### Resources
| Topic | Resource Link |
| :--- | :--- |
| `async`/`await` | [MDN Web Docs: async function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function) |
| Promise Methods | [MDN Web Docs: Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) |
| Concurrency & `AbortController` | [MDN Web Docs: AbortController](https://developer.mozilla.org/en-US/docs/Web/API/AbortController) |

---

## Day 3: Express Foundations
### Concepts
Dive into the **Express.js** framework:
- **Middleware Pipeline:** Requests go through middleware functions in sequence.
- **Central Error Handler:** A single place to catch and format errors.
- **Logging:** Use **pino** for request logging and debugging.
- **Input Validation:** Use **Joi** (or alternatives like Zod) to validate request bodies.

### Task
Create an Express application with:
- A `/health` route.
- A central error handler.
- Input validation on a route.

### Example Code
```js
import express from "express";
import pino from "pino-http";
import Joi from "joi";

const app = express();
app.use(express.json());
app.use(pino());

// Health check route
app.get("/health", (req, res) => {
  res.json({ status: "ok" });
});

// Validation schema
const userSchema = Joi.object({
  name: Joi.string().min(3).required(),
  email: Joi.string().email().required(),
});

// Example route with validation
app.post("/users", (req, res, next) => {
  const { error, value } = userSchema.validate(req.body);
  if (error) return next(error); // send to error handler
  res.status(201).json({ message: "User created", user: value });
});

// Middleware example
app.use((req, res, next) => {
  req.log.info(`Request received at ${req.path}`);
  next();
});

// Central error handler
app.use((err, req, res, next) => {
  req.log.error(err);
  res.status(400).json({
    error: true,
    message: err.message,
  });
});

app.listen(3000, () => {
  console.log("Server running on http://localhost:3000");
});
```

### Resources
| Topic | Resource Link |
| :--- | :--- |
| Express Middleware | [Express.js: Using middleware](https://expressjs.com/en/guide/using-middleware.html) |
| Error Handling | [Express.js: Error handling](https://expressjs.com/en/guide/error-handling.html) |
| Pino Logger | [Pino: Getting Started](https://getpino.io/#/docs/getting-started?id=getting-started) |
| Input Validation | [Joi: Getting Started](https://joi.dev/api/?v=17.9.1#getting-started) |

---

## Day 4: PostgreSQL + Prisma
### Concepts
Integrate a database into your application stack:
- **Prisma Schema:** Define models and relations.
- **Migrations:** Safely evolve schema with version control.
- **Relations:** One-to-many, many-to-many.
- **Transactions:** Ensure data consistency across multiple queries.
- **Seed Script:** Populate your DB with sample data.

### Task
Set up a PostgreSQL database and configure Prisma. Create a schema with two models in a one-to-many relationship. Run a migration and seed the database.

---

### Example `schema.prisma`
```prisma
datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

generator client {
  provider = "prisma-client-js"
}

model Author {
  id    Int     @id @default(autoincrement())
  name  String
  books Book[]
}

model Book {
  id       Int    @id @default(autoincrement())
  title    String
  authorId Int
  author   Author @relation(fields: [authorId], references: [id])
}

```

### Resources
| Topic | Resource Link |
| :--- | :--- |
| Prisma Get Started | [Prisma: Getting started with PostgreSQL](https://www.prisma.io/docs/getting-started/quickstart) |
| Prisma Schema | [Prisma Docs: Schema](https://www.prisma.io/docs/concepts/components/prisma-schema) |
| Migrations | [Prisma Docs: Migrations](https://www.prisma.io/docs/concepts/components/prisma-migrate) |
| Relations | [Prisma Docs: Relations](https://www.prisma.io/docs/concepts/components/prisma-schema/relations) |
| PostgreSQL Docs | [PostgreSQL Official Documentation](https://www.postgresql.org/docs/) |
| PostgreSQL Docker Image | [Docker Hub: postgres](https://hub.docker.com/_/postgres) |


---

## Day 5: Long Final Project: Library Manager API (Full CRUD)
### Project Scope
Build a complete Library Manager API that manages books, authors, members, and loans.

#### Models
- `Author`
- `Book`
- `Member`
- `Loan`

#### Business Rules
- A book cannot be loaned if it's not available or if an active loan for that book already exists.
- Returning a book sets the `returnedAt` timestamp and marks the book as `available=true`.
- (Optional) A member cannot have more than five active loans.

#### Endpoints
- **CRUD:** Full CRUD for `Authors`, `Books`, and `Members`.
- **Search:** A `GET /books?q=` endpoint to search for books by title or author name.
- **Loans:**
  - `POST /loans` to create a new loan.
  - `POST /loans/:id/return` to return a book.

#### Seed Script
- Create a seed script that populates the database with:
  - 5 authors
  - 8 books
  - 3 members
  - 1 active loan

#### Auto-tests (Minimum)
- Test CRUD operations for happy paths, 404 Not Found, and 422 Unprocessable Entity.
- Test the loan conflict flow to ensure a 409 Conflict is returned when trying to loan an unavailable book.
- Test the full return flow.
- Test the search functionality for `/books?q=`.
- Test the `/health` route.
- Ensure migrations and the seed script run correctly.

### Resources
| Topic | Resource Link |
| :--- | :--- |
| Building REST APIs | [MDN Web Docs: Designing RESTful APIs](https://developer.mozilla.org/en-US/docs/Glossary/REST) |
| Jest for Testing | [Jest: Getting Started](https://jestjs.io/docs/getting-started) |
| Supertest for API Testing | [Supertest: Getting Started](https://www.npmjs.com/package/supertest) |

---
