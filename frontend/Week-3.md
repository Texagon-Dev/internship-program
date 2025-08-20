# **Week 3 Internship Roadmap – Advanced Frontend & Web Essentials**

---

### **Day 1 – API Calls & Data Handling**

🎯 Goal: Master fetching data from APIs, handling async/await, errors, and pagination.

| Topic | Description | Resource | Task |
| ----- | ----- | ----- | ----- |
| Fetch & Axios | Fetch API basics, async/await, Axios client, error handling | [MDN Fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) / [Axios Docs](https://axios-http.com/docs/intro) | Fetch posts from `https://jsonplaceholder.typicode.com/posts` and display them in React |
| REST API Basics | GET, POST, PUT, DELETE, status codes | [REST Tutorial](https://restfulapi.net/http-methods/) | Add a form to **create new posts** via API |
| Error Handling | try/catch, loading & error states | [React Error Handling](https://react.dev/reference/react/Component#catching-rendering-errors-with-an-error-boundary) | Show **loading spinner \+ error message** while fetching |
| Pagination & Filtering | Query params, client side filtering | [MDN URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) | Implement pagination (5 posts per page) and add a search filter |

✅ **Deliverables (Day 1):**

* React component fetching posts with **loading & error states**

* Form to **add new post** via API

* **Pagination \+ filtering** feature

---

### **Day 2 – Supabase Basics**

🎯 Goal: Learn how to use Supabase (DB \+ API \+ Realtime).

| Topic | Description | Resource | Task |
| ----- | ----- | ----- | ----- |
| Supabase Setup | Create project, get API keys, connect in Next.js | [Supabase Quickstart](https://supabase.com/docs/guides/getting-started/quickstarts/with-nextjs) | Connect a Next.js app to Supabase |
| Database Tables | Creating tables, querying rows | [Supabase Database Docs](https://supabase.com/docs/guides/database) | Create a `Tasks` table, fetch tasks and display them |
| Row Inserts & Updates | Insert/update via JS client | [Supabase JS Docs](https://supabase.com/docs/reference/javascript/supabase-client) | Add a form to **insert tasks** and update status |
| Realtime | Listen for changes in DB | [Supabase Realtime](https://supabase.com/docs/guides/realtime) | Show tasks updating in real time when added/updated |

✅ **Deliverables (Day 2):**

* Supabase connected **Next.js app**

* Working **Tasks table** with CRUD

* **Realtime updates** on new task inserts

---

### **Day 3 – Authentication \+ Storage**

🎯 Goal: Implement auth with Supabase and handle storage securely.

| Topic | Description | Resource | Task |
| ----- | ----- | ----- | ----- |
| Supabase Auth | Email/password signup, login, logout | [Supabase Auth](https://supabase.com/docs/guides/auth) | Implement signup/login form with Supabase |
| Protected Routes | Restrict routes to logged in users | [Next.js Middleware](https://nextjs.org/docs/app/building-your-application/routing/middleware) | Protect `/dashboard` route and redirect guests |
| LocalStorage vs SessionStorage vs Cookies | Use cases & differences | [MDN Storage Guide](https://developer.mozilla.org/en-US/docs/Web/API/Web_Storage_API/Using_the_Web_Storage_API) | Store auth token in `localStorage` and persist login |
| Cookies | Basics, JWT storage, preferences | [Cookies vs Storage](https://auth0.com/docs/secure/tokens/token-storage) | Save theme preference in cookies & read in middleware |
| Logout & Session Handling | Clearing tokens, redirect | [Supabase Session](https://supabase.com/docs/reference/javascript/auth-signout) | Add logout button that clears session and storage |

✅ **Deliverables (Day 3):**

* Working **auth system** (signup, login, logout)

* **Protected routes** for logged in users only

* Theme preference stored in **cookies**

---

### **Day 4 – State Management with Zustand**

🎯 Goal: Manage global state effectively in real apps.

| Topic | Description | Resource | Task |
| ----- | ----- | ----- | ----- |
| Zustand Basics | Store, actions, selectors | [Zustand Docs](https://docs.pmnd.rs/zustand/getting-started/introduction) | Build a **counter store** used across components |
| Async State | Fetching data in Zustand | [Zustand Async Example](https://docs.pmnd.rs/zustand/guides/async-actions) | Move **tasks fetching** into Zustand store |
| Persist Middleware | Saving state to storage | [Zustand Persist](https://docs.pmnd.rs/zustand/integrations/persisting-store-data) | Persist auth session in localStorage |
| Multiple Stores | Organizing stores (auth, tasks, UI) | — | Create `useAuthStore`, `useTaskStore`, `useUIStore` |
| Production Patterns | Scalable state management | — | Connect **Supabase tasks** to Zustand global state |

✅ **Deliverables (Day 4):**

* Multiple Zustand stores (`auth`, `tasks`, `UI`)

* Persisted state (auth session)

* **Supabase tasks synced** with Zustand

---

### **Day 5 – Web Essentials \+ Mini Project**

🎯 Goal: Cover essential web concepts and build a full stack mini project.

| Topic | Description | Resource | Task |
| ----- | ----- | ----- | ----- |
| HTTP & Status Codes | Common status codes (200, 201, 400, 401, 403, 404, 500\) | [MDN HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status) | Handle errors properly in API responses |
| CORS | What it is, common issues, fixes | [MDN CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS) | Explain how you’d fix a blocked API request |
| Debouncing & Throttling | Performance optimization | [Debounce/Throttle Guide](https://www.freecodecamp.org/news/javascript-debounce-example/) | Build a **debounced search bar** for tasks |
| Security Basics | XSS, CSRF, input sanitization | [OWASP Top 10](https://owasp.org/www-project-top-ten/) | Sanitize input in a form before storing |
| Mini Project (Capstone) | Combine Supabase \+ Zustand \+ Auth \+ Tailwind | — | Build a **Task Manager App** |

**Project Requirements:**

* Signup/login with Supabase Auth

* Authenticated **dashboard** with tasks

* CRUD tasks (Supabase DB \+ API calls)

* Zustand for **global state** (tasks \+ auth)

* Session persistence with localStorage

* Responsive UI with Tailwind

✅ **Deliverables (Day 5):**

* **Task Manager App** with Auth, CRUD, Zustand

* Search with **debounce**

* Secure form inputs

* **Deployed app** (Netlify/Vercel/Cloudflare)

---

**After Week 3 interns will:**

* Be **production ready frontend engineers**

* Confidently use **Supabase \+ Zustand \+ React**

* Understand **auth, APIs, state management**

* Know key web concepts (CORS, security, storage)

* Have a **capstone Task Manager App** deployed online  
