# **🚀 Week 2 Internship Roadmap – React \+ Next.js**

---

### **Day 1 – React Fundamentals**

🎯 Goal: Understand React basics, JSX, props, state, events, lists, and clean code practices.

| Topic | Description | Resource | Task |
| ----- | ----- | ----- | ----- |
| React Basics | What is React, components, JSX, rendering | [React Docs – Quick Start](https://react.dev/learn) | Build a **ProfileCard component** showing name, role, and image |
| Props & Children | Passing data between components | [React Docs – Passing Props](https://react.dev/learn/passing-props-to-a-component) | Create a **Card component** with title/content passed as props |
| State (useState) | Local state management | [React Docs – useState](https://react.dev/reference/react/useState) | Build a **counter** with increment/decrement |
| Event Handling | Handling clicks, forms, keyboard | [React Docs – Events](https://react.dev/learn/responding-to-events) | Add a button to **toggle dark/light text** |
| Lists & Keys | Rendering dynamic lists | [React Docs – Rendering Lists](https://react.dev/learn/rendering-lists) | Build a **dynamic todo list** using `map` |
| SOLID Principles in React | Writing clean, scalable React code | [SOLID Principles in React (YouTube)](https://www.youtube.com/watch?v=Ix6JoarGYiA&ab_channel=moderndev) | Refactor your Card & Todo components to follow **SOLID** practices |

✅ **Deliverables (Day 1):**

* ProfileCard component

* Counter with state & events

* Dynamic Todo list with keys

* Refactored components applying **SOLID principles**

---

### **Day 2 – React Hooks & Forms**

🎯 Goal: Work with hooks, controlled forms, lifting state, conditional rendering, and reusable components.

| Topic | Description | Resource | Task |
| ----- | ----- | ----- | ----- |
| useEffect | Side effects: fetch, subscriptions, cleanup | [React Docs – useEffect](https://react.dev/reference/react/useEffect) | Fetch **dummy posts** (JSONPlaceholder) and render |
| Forms (Controlled) | Controlled vs uncontrolled inputs | [React Docs – Forms](https://react.dev/learn/sharing-state-between-components#controlled-components) | Build a **signup form with validation** |
| Lifting State | Sharing state across components | [React Docs – State Management](https://react.dev/learn/sharing-state-between-components) | Create a parent component with multiple inputs updating one object |
| Conditional Rendering | Show/hide elements based on state/props | [React Docs – Conditional Rendering](https://react.dev/learn/conditional-rendering) | Show "Logged in" or "Guest" message |
| Reusable Components | Component composition & variants | [React Patterns](https://reactpatterns.com/) | Build a **Button component** with multiple variants (primary, secondary, outline) |

✅ **Deliverables (Day 2):**

* Posts fetched & displayed from API

* Signup form with **validation**

* Parent component with lifted state

* Conditional rendering example

* Reusable **Button component**

---

### **Day 3 – Next.js Fundamentals**

🎯 Goal: Understand Next.js project setup, routing, static assets, and layouts.

| Topic | Description | Resource | Task |
| ----- | ----- | ----- | ----- |
| Next.js Setup | Create Next app, folder structure | [Next.js Docs – Getting Started](https://nextjs.org/docs/getting-started) | Initialize a **Next.js project** |
| File based Routing | Pages & nested routes | [Next.js Docs – Routing](https://nextjs.org/docs/app/building-your-application/routing) | Create routes: `/`, `/about`, `/contact` |
| Linking & Navigation | Client side navigation | [Next.js Docs – Link](https://nextjs.org/docs/api-reference/next/link) | Add a **navbar with navigation** |
| Static Assets | Public folder usage | [Next.js Docs – Static Assets](https://nextjs.org/docs/app/building-your-application/optimizing/static-assets) | Add a **profile image** on `/about` page |
| Layouts | Shared components (navbar/footer) | [Next.js Layouts](https://nextjs.org/docs/app/building-your-application/routing/pages-and-layouts) | Create a **layout** with header \+ footer |

✅ **Deliverables (Day 3):**

* Next.js project initialized

* Routes: Home, About, Contact

* Navbar with **Link navigation**

* Static image on About page

* Reusable **Layout component**

---

### **Day 4 – Data Fetching & API Integration**

🎯 Goal: Explore Next.js data fetching (CSR, SSR, SSG) and API routes.

| Topic | Description | Resource | Task |
| ----- | ----- | ----- | ----- |
| Fetching in useEffect | Client side fetching | [React Fetch Guide](https://react.dev/reference/react/useEffect#fetching-data-with-effects) | Fetch posts dynamically on `/posts` page |
| getServerSideProps | Server side rendering | [Next.js SSR](https://nextjs.org/docs/pages/building-your-application/data-fetching/get-server-side-props) | Fetch posts **on server** before render |
| getStaticProps | Static site generation | [Next.js SSG](https://nextjs.org/docs/pages/building-your-application/data-fetching/get-static-props) | Generate blog posts **at build time** |
| Dynamic Routes | Dynamic pages with `[id].js` | [Next.js Dynamic Routes](https://nextjs.org/docs/pages/building-your-application/routing/dynamic-routes) | Create `/posts/[id]` page for individual posts |
| API Routes | Build simple backend APIs | [Next.js API Routes](https://nextjs.org/docs/pages/building-your-application/routing/api-routes) | Create `/api/users` endpoint returning JSON |

✅ **Deliverables (Day 4):**

* `/posts` page with **client side fetch**

* Blog posts rendered with **SSR**

* Blog posts rendered with **SSG**

* `/posts/[id]` dynamic route page

* `/api/users` API endpoint

---

### **Day 5 – Mini Project (React \+ Next.js)**

🎯 Goal: Build a small production ready Next.js project with React fundamentals, Tailwind, and APIs.

| Project Idea | Description | Requirements |
| ----- | ----- | ----- |
| **Blog Dashboard** | A simple blog app with posts & details |   Pages: Home, About, Blog list, Blog details   Use **getStaticProps \+ getStaticPaths** for posts   Blog detail page at `/posts/[id]`   Controlled form for **user feedback**   **Reusable Card & Button** components   Tailwind styling (dark mode optional)   Deploy on **Vercel** |

Resources:

* [Next.js Tutorial Blog Example](https://nextjs.org/learn/basics/create-nextjs-app)

* [Tailwind UI Patterns](https://tailwindui.com/)

✅ **Deliverables (Day 5):**

* Completed **Blog Dashboard project**

* Blog list & dynamic blog details

* Feedback form with validation

* Tailwind styling \+ reusable components

* Deployed on **Vercel**

---

By the end of **Week 2**, interns will:

* Build React components with **props, state, hooks**

* Work with **forms, events, reusable patterns**

* Learn **Next.js routing, SSR, SSG, API routes**

* Deploy a **production ready blog project**

