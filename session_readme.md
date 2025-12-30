# weekly report 

Name: Natan Muleta
Development of a Frontend Blog Website completed over five weekly frontend training sessions.
Date:December 30 , 2025
Advisor: Binyam

the link of Blog website is 


# WEEK 4: React Fundamentals
we learn about the react fundamentals it's include this things

## What is the Frontend?


The frontend is the part of a website or application that users see and interact with directly in their browser.

# SPA vs MPA

## SPA (Single Page Application)
A Single Page Application loads one HTML page and updates content dynamically using JavaScript
How SPA works:

Page loads once

Navigation happens without full page reload

Only the needed content changes

Examples:

React apps

Gmail

Twitter

Dashboard applications

Advantages:

Faster navigation

Better user experience

Feels like a mobile app

## MPA (Multi Page Application)

A Multi Page Application reloads the page every time you navigate.

How MPA works:

Each page is a separate HTML file

Browser reloads on every navigation

Examples:

Traditional websites

Old-style PHP or HTML sites

## Why React?

React is a JavaScript library for building user interfaces.

Why React is popular:

Component-based architecture

Fast rendering with Virtual DOM

Reusable UI components

Strong community support

Easy to scale projects

Why React for this project:

Perfect for SPA

Clean separation of UI parts

Easy to manage state

Beginner-friendly for learning frontend

📌 React helps us think in components, not pages.

## Components, JSX, Props
```
{

Components
A component is a small reusable piece of UI.
Examples:
Navbar
BlogCard
Footer
Button

}

```

## Basic State

State is data that changes over time inside a component.
In React, we use the useState hook

State is used for:

Form inputs

UI interactions

Likes, toggles, filters

Local data changes

## Styling (Tailwind CSS)

Tailwind CSS is a utility-first CSS framework.

Instead of writing CSS files, you use classes directly in JSX.

Why Tailwind?
No custom CSS needed
Faster development
Consistent design
Easy responsive layouts
Small final CSS size
Tailwind keeps styling simple and scalable.

## Folder Structure & Tooling (Vite)
Vite is a modern build tool for frontend projects.
Why Vite?
Very fast startup
Fast hot reload
Simple configuration
Optimized production builds

### Typical Folder Structure
```
{
    src/
│── components/   → Reusable UI components
│── pages/        → Application pages (routes)
│── data/         → Local JSON data files
│── hooks/        → Custom React hooks
│── types/        → TypeScript interfaces
│── assets/       → Images and static files
│── App.tsx       → Main app component
│── main.tsx      → App entry point

}
```
# WEEK 5: React Hooks & Events

## Why Hooks?
Hooks let you use state and lifecycle features in function components.
```
{
Before hooks:
State was only in class components
Code was harder to reuse and understand
With hooks:
Cleaner code
Reusable logic
No classes needed
Easier to learn and maintain
Hooks make function components powerful.
}

```

## useState

useState lets a component store and update data.
```{

Syntax:
const [value, setValue] = useState(initialValue);
Example (Counter):
const [count, setCount] = useState(0);
<button onClick={() => setCount(count + 1)}>
  Count: {count}
</button>
When state changes, the UI updates automatically.

} 
```

## useEffect

useEffect runs side effects in a component.
Side effects include:
Fetching data
Running code after render
Subscribing to events

```
{
useEffect(() => {
  console.log("Component rendered");
}, []);

}
```
The empty array [] means run once on mount.

## Lifecycle Simulation with Hooks

In class components, we had lifecycle methods.
Hooks simulate them using useEffect.

Lifecycle	Hook Equivalent
Component mounts	useEffect(() => {}, [])
Component updates	useEffect(() => {}, [dependency])
Component unmounts	return () => {} cleanup

```
{
useEffect(() => {
  console.log("Mounted");

  return () => {
    console.log("Unmounted");
  };
}, []);

One hook can replace multiple lifecycle methods.
}
```
##  Practical Examples

### Fetching API Data
```
 {

useEffect(() => {
  fetch("/data/blogs.json")
    .then(res => res.json())
    .then(data => setBlogs(data));
}, []);

Used for:
Loading data on page load
Fetching local JSON or APIs
} 
```

### Toggle Example
```
{
const [isOpen, setIsOpen] = useState(false);

<button onClick={() => setIsOpen(!isOpen)}>
  Toggle
</button>
 Used for:
Modals
Dropdowns
Dark mode
}
```
 ### ounter Example

```
{
const [count, setCount] = useState(0);

<button onClick={() => setCount(count + 1)}>+</button>
<button onClick={() => setCount(count - 1)}>-</button>
  Used for:
Likes
Quantities
Scores
}
```

# WEEK 6: Client-Side State Management


## Local State vs Global State

🔹 Local State

Local state belongs to one component only.

```
{
const [isOpen, setIsOpen] = useState(false);

Used for:
Toggles
Form inputs
Modals
Counters

If only one component needs the data → local state is enough
} 
```

## Global State

Global state is shared across multiple components.

Examples:
```
{
 Logged-in user
Theme (dark/light)
Shopping cart
}
```

If many components need the same data → global state

## When Is Global State Needed?

Use global state when:

Data is used in many places

Props are passed too deeply (prop drilling)

State must persist across pages

State represents app-level data

Avoid global state for small UI logic
Use it for shared, important data

## State Management Options

### Context API

Built into React

Good for small to medium apps

Simple setup

Can cause re-renders if misused

Best for:

Theme

Auth user

Language settings

###  Zustand

Lightweight external library

Simple API

Very fast

Less boilerplate

Best for:

Medium to large apps

Clean global state

### Redux

Powerful and scalable

More boilerplate

Industry standard for large apps

Best for:

Large applications

Complex state logic

 For most frontend apps:


Context or Zustand is enough

## Building a Global Provider (Context API Example

**Step 1: Create Context**
`
import { createContext } from "react";

export const ThemeContext = createContext(null);

`
**Step 2: Create Provider**
`
export function ThemeProvider({ children }) {
  const [theme, setTheme] = useState("light");

  return (
    <ThemeContext.Provider value={{ theme, setTheme }}>
      {children}
    </ThemeContext.Provider>
  );
}

`

**Step 3: Wrap App**
`

<ThemeProvider>
  <App />
</ThemeProvider>

`

**Step 4: Use Context**
`
const { theme, setTheme } = useContext(ThemeContext);
`
### This makes the state available everywhere.

## Common Use Cases
```
{
   
Theme (Dark / Light)

Shared across all pages

Changes UI globally

Perfect for Context

  Cart Data

Used in navbar, pages, checkout

Needs global access

Best with Zustand or Context

 User Data

Login status

User profile

Permissions

 Must be global because many components rely on it.
}

```
# WEEK 7: Server-Side State Management

##  Client State vs Server State

 **Client State**

Client state lives entirely in the frontend.

Examples:

Theme (dark / light)

Toggle states

Modal open/close

Form input values

**Managed with:**

useState

Context

Zustand

**server State**

Server state comes from an external source (API, JSON, backend).

Examples:

Blog list

Users

Products

Comments

Server state:

Can change outside your app

Needs refetching

Needs caching

Can fail (errors)

## Fetching Data: Fetch API vs Axios

**Fetch API**

Built into browsers
No installation needed
Manual error handling

`
 fetch("/api/blogs")
  .then(res => res.json())

`
**Axios**
External library

Automatic JSON handling

Better error responses

Supports interceptors

` axios.get("/api/blogs");
  `
### Axios is usually cleaner for real projects.

## TanStack Query / RTK Query

These libraries manage server state automatically.

They handle:

Fetching

Caching

Loading states

Errors

Refetching

Pagination

**TanStack Query (React Query)**

Best for:

REST APIs

Frontend-focused apps
`useQuery({
  queryKey: ["blogs"],
  queryFn: fetchBlogs
});
`

**RTK Query**

Best for:

Redux-based apps

Large applications
`
useGetBlogsQuery();

`
### Both eliminate manual state handling.

## Fetch, Cache, Invalidate

 ### Fetch

Gets fresh data from the server.
 
 **Cache**

Stores fetched data locally to:

Avoid refetching

Improve performance

Cached data is reused automatically.

**Invalidate**

Marks cached data as outdated.

Used when:

Data changes (create, update, delete)

Need fresh data

` queryClient.invalidateQueries(["blogs"]);
`

## Loading, Error, Refetch Handling

**Loading**

Show a loader while data is loading.

`
if (isLoading) return <Spinner />;

`
**Error** 
Handle failed requests gracefully.
`
if (isError) return <ErrorMessage />;

`
**Refetch**

Reload data manually or automatically.

`refetch();
`
Used for:

Refresh buttons

Retry after error

## Pagination
```{
Pagination loads data in parts, not all at once.

Why pagination?

Better performance

Faster loading

Cleaner UI
Pagination Example:

Page 1 → Blogs 1–10

Page 2 → Blogs 11–20

Libraries support:

Page-based pagination

Infinite scrolling
}
```
`
useQuery(["blogs", page], fetchBlogs);
`
# WEEK 8: Routing & Forms

## React Router

React Router handles navigation and routing in a React SPA.

It allows different URLs to show different components without reloading the page.

Example:
`
<Route path="/" element={<Home />} />
<Route path="/blogs" element={<Blogs />} />
`

### Enables multi-page experience in a single-page app.

## Nested Routes

Nested routes allow routes inside other routes.
Used when pages share:
Layout
Navbar
Sidebar
`
<Route path="/dashboard" element={<Layout />}>
  <Route path="profile" element={<Profile /> />
</Route>
`

### Keeps layouts clean and reusable

## Navigation
```
{
Navigation lets users move between routes.

Ways to navigate:

<Link /> → user clicks

useNavigate() → programmatic navigation
}
```

`
<Link to="/blogs">Blogs</Link>
navigate("/login");
`

### Navigation is instant (no page reload).

## Controlled & Uncontrolled Components

**Controlled Components**
Form input is controlled by React state.
`
<input value={name} onChange={e => setName(e.target.value)} />
 Easy validation
 React controls data
`

**Uncontrolled Components**
Form input is controlled by the DOM, not React state.
`
<input ref={inputRef} />

`
Less code
Harder validation
Controlled components are preferred.

**Form Validation (Zod)**

Zod is a schema-based validation library.
It ensures form data matches rules.

`

const schema = z.object({
  email: z.string().email(),
  password: z.string().min(6),
});

`
Clean, reusable, and type-safe validation.

## Multi-Page Forms
```
{
Multi-page forms split long forms into steps.
Example:

Step 1 → Personal info

Step 2 → Address

Step 3 → Review

Benefits:

Better UX

Less overwhelming

Easier validation per step

Often combined with:

React Router

Global state

Zod validation
}
```








































