# React Mastery Guide: Fundamentals to Job-Ready (2024-2025)

এই গাইডটি আপনাকে React-এর একদম বেসিক থেকে শুরু করে প্রফেশনাল লেভেল পর্যন্ত নিয়ে যাবে। এটি বিশেষভাবে তৈরি করা হয়েছে যারা ইউরোপ বা আমেরিকার রিমোট জবের জন্য প্রস্তুতি নিচ্ছেন। এখানে আমরা শুধুমাত্র Modern React (Hooks, Functional Components) শিখব যা ২০২৪-২০২৫ সালের ইন্ডাস্ট্রির স্ট্যান্ডার্ড।

---

## 1. What & Why React (React কি এবং কেন?)

### React কি এবং এটি কোন সমস্যার সমাধান করে?

React হলো একটি JavaScript Library (Framework নয়) যা ইউজার ইন্টারফেস (UI) তৈরি করার জন্য ব্যবহৃত হয়। এটি Facebook (বর্তমানে Meta) তৈরি করেছে।
**সমস্যা:** আগে ভ্যানিলা জাভাস্ক্রিপ্ট দিয়ে বড় অ্যাপলিকেশন তৈরি করলে কোড ম্যানেজ করা খুব কঠিন হয়ে যেত। একটি ছোট পরিবর্তনের জন্য পুরো পেজ রিলোড বা অনেকগুলো DOM ম্যানিপুলেশন করতে হতো, যা অ্যাপকে স্লো করে দিত।
**সমাধান:** React এই সমস্যার সমাধান করেছে **Component-Based Architecture** এবং **Virtual DOM** এর মাধ্যমে। এটি অ্যাপকে ছোট ছোট অংশে ভাগ করে এবং শুধুমাত্র প্রয়োজনীয় অংশটুকুই আপডেট করে।

### Why React vs Vanilla JavaScript?

| Feature              | Vanilla JavaScript                  | React                                 |
| :------------------- | :---------------------------------- | :------------------------------------ |
| **Code Structure**   | সব কোড এক ফাইলে বা অগোছালো হতে পারে | ছোট ছোট Component-এ ভাগ করা থাকে      |
| **DOM Manipulation** | সরাসরি DOM আপডেট করতে হয় (Slow)     | Virtual DOM ব্যবহার করে (Fast)        |
| **Reusability**      | কোড পুনরায় ব্যবহার করা কঠিন         | Component বারবার ব্যবহার করা যায়      |
| **State Management** | ম্যানুয়ালি ভেরিয়েবল ট্র্যাক করতে হয় | অটোমেটিক স্টেট আপডেট এবং রি-রেন্ডারিং |

### Virtual DOM Concept (সহজ ভাষায়)

মনে করুন আপনি একটি বাড়ির ব্লুপ্রিন্ট (নকশা) পরিবর্তন করতে চান।

- **Real DOM:** আপনি সরাসরি বাড়িটি ভেঙে নতুন করে বানাচ্ছেন। এটি অনেক সময়সাপেক্ষ এবং ব্যয়বহুল।
- **Virtual DOM:** আপনি কম্পিউটারে নকশাটি এডিট করছেন। React প্রথমে এই ভার্চুয়াল নকশায় পরিবর্তন আনে, তারপর আসল বাড়ির সাথে তুলনা করে (Diffing) এবং শুধুমাত্র যে দেওয়ালটি পরিবর্তন হয়েছে, সেটিই বাস্তবে পরিবর্তন করে (Reconciliation)। এটিই React-কে এত ফাস্ট করে তোলে।

### Component-Based Architecture Benefits

- **Reusability:** একবার `Button` কম্পোনেন্ট বানিয়ে পুরো অ্যাপে হাজারবার ব্যবহার করা যায়।
- **Maintainability:** কোড ছোট ছোট অংশে ভাগ থাকায় ডিবাগ করা সহজ।
- **Collaboration:** টিমের একেকজন একেক কম্পোনেন্টে কাজ করতে পারে।

### When to use React vs other frameworks

- **React:** যখন আপনি অনেক ফ্লেক্সিবিলিটি চান এবং বড় কমিউনিটি সাপোর্ট দরকার। জবের বাজারে এর চাহিদা সবচেয়ে বেশি।
- **Vue/Angular:** যদি আপনি নির্দিষ্ট স্ট্রাকচার পছন্দ করেন। তবে React বর্তমানে মার্কেট লিডার।

### React's role in modern web development

বর্তমানে মডার্ন ওয়েব ডেভেলপমেন্টে React হলো "De Facto Standard"। Next.js, Remix-এর মতো ফ্রেমওয়ার্কগুলো React-এর ওপর ভিত্তি করেই তৈরি। তাই React শেখা মানে আপনি পুরো ইকোসিস্টেমের চাবি হাতে পেলেন।

---

## 2. Core Concepts (Foundation)

### Components (The Building Blocks)

React অ্যাপ হলো অনেকগুলো লেগো (Lego) ব্লকের মতো। প্রতিটি ব্লক হলো একটি **Component**। যেমন: Header, Footer, Sidebar, Button ইত্যাদি। সব ব্লক মিলে একটি পূর্ণাঙ্গ অ্যাপ তৈরি হয়।

### JSX Syntax and Rules

JSX (JavaScript XML) দেখতে HTML-এর মতো, কিন্তু এটি আসলে JavaScript।

```jsx
// JSX
const element = <h1>Hello, world!</h1>;
```

**Rules:**

1. অবশ্যই একটি প্যারেন্ট এলিমেন্ট রিটার্ন করতে হবে (বা Fragment `<>...</>`)।
2. ট্যাগ অবশ্যই ক্লোজ করতে হবে (যেমন `<img />`)।
3. `class` এর বদলে `className` ব্যবহার করতে হবে।
4. JavaScript এক্সপ্রেশন `{ }` এর মধ্যে লিখতে হবে।

### Props (Passing Data Down)

Props (Properties) হলো কম্পোনেন্টের ইনপুট। এটি দিয়ে প্যারেন্ট থেকে চাইল্ড কম্পোনেন্টে ডাটা পাঠানো হয়। Props **Read-Only** (পরিবর্তন করা যায় না)।
**Analogy:** আপনি কাউকে গিফট (Props) দিলেন। সে গিফটটি রিসিভ করল, কিন্তু গিফটের ভেতরের জিনিস সে পাল্টাতে পারবে না।

### State (Component Memory)

State হলো কম্পোনেন্টের নিজস্ব মেমোরি। যখন স্টেট পরিবর্তন হয়, তখন কম্পোনেন্টটি নতুন করে রেন্ডার হয়।
**Analogy:** একটি ডিজিটাল ঘড়ি। সময় (State) প্রতি সেকেন্ডে পাল্টাচ্ছে এবং ডিসপ্লে (UI) আপডেট হচ্ছে।

### Rendering and Re-rendering

- **Rendering:** যখন React প্রথমবার কম্পোনেন্টটি স্ক্রিনে দেখায়।
- **Re-rendering:** যখন State বা Props পরিবর্তন হয়, তখন React কম্পোনেন্টটি আবার আঁকে।

### One-way Data Flow

React-এ ডাটা সবসময় **উপর থেকে নিচে** (Parent -> Child) প্রবাহিত হয়। একে Unidirectional Data Flow বলে। এটি অ্যাপের ডাটা ফ্লো ট্র্যাক করা সহজ করে।

### Component Lifecycle (Simplified with Hooks)

1. **Mounting:** কম্পোনেন্ট জন্ম নিল (স্ক্রিনে এল)। -> `useEffect(() => {}, [])`
2. **Updating:** কম্পোনেন্ট পরিবর্তন হলো (State/Props আপডেট)। -> `useEffect(() => {}, [dep])`
3. **Unmounting:** কম্পোনেন্ট মারা গেল (স্ক্রিন থেকে চলে গেল)। -> `useEffect(() => { return () => cleanup }, [])`

---

## 3. Modern React Setup (2024-2025)

### Create React App vs Vite

- **Create React App (CRA):** আগে ব্যবহার হতো, কিন্তু এখন অনেক স্লো এবং আউটডেটেড। **ব্যবহার করবেন না।**
- **Vite:** বর্তমানে স্ট্যান্ডার্ড। এটি অনেক ফাস্ট, লাইটওয়েট এবং মডার্ন। **অবশ্যই Vite ব্যবহার করবেন।**

### Step-by-step Project Setup with Vite

টার্মিনালে নিচের কমান্ডগুলো দিন:

```bash
npm create vite@latest my-react-app -- --template react
cd my-react-app
npm install
npm run dev
```

### Recommended Folder Structure

একটি স্কেলেবল অ্যাপের জন্য এই স্ট্রাকচার ফলো করুন:

```
/src
  /components     # Reusable UI components (Button, Card)
  /pages          # Page-level components (Home, About)
  /hooks          # Custom hooks (useFetch, useAuth)
  /services       # API calls (api.js)
  /utils          # Helper functions (formatDate.js)
  /types          # TypeScript types (user.ts)
  /assets         # Images, fonts
  /lib            # Third-party config (firebase.js)
  App.jsx
  main.jsx
```

### Essential Dependencies

- **react-router-dom:** পেজ নেভিগেশনের জন্য।
- **prop-types:** প্রপস ভ্যালিডেশনের জন্য (যদি TypeScript না ব্যবহার করেন)।
- **eslint-plugin-react-hooks:** হুকসের নিয়ম মানার জন্য।

### ESLint + Prettier Configuration

কোড ক্লিন রাখার জন্য `.eslintrc.cjs` এবং `.prettierrc` ফাইল কনফিগার করা জরুরি। এটি অটোমেটিক ভুল ধরবে এবং কোড ফরম্যাট করবে।

---

## 4. JSX Deep Dive

### JSX Syntax Rules

```jsx
// ❌ Wrong
return (
  <h1>Title</h1>
  <p>Text</p>
)

// ✅ Right (Single Parent)
return (
  <div>
    <h1>Title</h1>
    <p>Text</p>
  </div>
)
```

### Embedding JavaScript Expressions

```jsx
const name = "Omar";
return <h1>Hello, {name}</h1>; // Hello, Omar
```

### Conditional Rendering

```jsx
// Ternary Operator
{
  isLoggedIn ? <Dashboard /> : <Login />;
}

// && Operator (If true, then render)
{
  hasError && <ErrorMessage />;
}
```

### List Rendering with .map()

```jsx
const fruits = ["Apple", "Banana", "Orange"];
return (
  <ul>
    {fruits.map((fruit, index) => (
      <li key={index}>{fruit}</li> // Key is crucial for performance
    ))}
  </ul>
);
```

### Event Handling

React-এ ইভেন্টগুলো camelCase হয়।

```jsx
<button onClick={handleClick}>Click Me</button> // ✅
<button onclick="handleClick()">Click Me</button> // ❌
```

### Fragments

অপ্রয়োজনীয় `div` এড়াতে Fragment ব্যবহার করুন।

```jsx
return (
  <>
    <h1>Title</h1>
    <p>Description</p>
  </>
);
```

---

## 5. Components (Functional Components Only)

### ✅ Functional Components (Modern Standard)

```jsx
function Welcome({ name }) {
  return <h1>Hello, {name}</h1>;
}
export default Welcome;
```

### ❌ Class Components (Outdated - Avoid)

Class components এখন আর নতুন প্রজেক্টে ব্যবহার করা হয় না। ইন্টারভিউ বা লিগ্যাসি কোড ছাড়া এগুলো শেখার দরকার নেই।

### Component Structure

1. Imports
2. Component Definition
3. Hooks
4. Helper Functions
5. Return (JSX)
6. Export

### Props Destructuring

```jsx
// Clean Way
const UserCard = ({ name, email, age }) => {
  return (
    <div className="card">
      <h2>{name}</h2>
      <p>{email}</p>
    </div>
  );
};
```

### Children Prop

কম্পোনেন্টের ভেতরে অন্য কন্টেন্ট পাস করার জন্য `children` প্রপ ব্যবহার হয়।

```jsx
const Card = ({ children }) => {
  return <div className="card-box">{children}</div>;
};

// Usage
<Card>
  <h1>This is inside the card</h1>
</Card>;
```

---

## 6. React Hooks (CRITICAL - You'll use these daily)

### useState Hook

স্টেট ম্যানেজ করার জন্য।

```jsx
import { useState } from "react";

function Counter() {
  // [currentState, functionToUpdateState] = useState(initialValue)
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}
```

**Common Mistake:** স্টেট সরাসরি মিউটেট করবেন না (`count = 5` ❌)। সবসময় `setCount(5)` ব্যবহার করুন।

### useEffect Hook

সাইড ইফেক্ট (API call, DOM update) হ্যান্ডেল করার জন্য।

```jsx
import { useEffect, useState } from "react";

function UserLoader() {
  const [users, setUsers] = useState([]);

  useEffect(() => {
    // Mounting: Runs only once
    fetch("https://api.example.com/users")
      .then((res) => res.json())
      .then((data) => setUsers(data));

    // Cleanup function (Unmounting)
    return () => {
      console.log("Component unmounted");
    };
  }, []); // Empty dependency array means run once

  return <div>{/* Render users */}</div>;
}
```

### useRef Hook

DOM এলিমেন্ট এক্সেস করতে বা ভ্যালু স্টোর করতে যা রি-রেন্ডার ঘটায় না।

```jsx
const inputRef = useRef(null);

const focusInput = () => {
  inputRef.current.focus(); // Accessing DOM directly
};

return <input ref={inputRef} />;
```

### useContext Hook

Prop Drilling এড়াতে গ্লোবাল ডাটা পাস করার জন্য।

```jsx
// 1. Create Context
const ThemeContext = createContext();

// 2. Provide Context
<ThemeContext.Provider value="dark">
  <App />
</ThemeContext.Provider>;

// 3. Consume Context
const theme = useContext(ThemeContext);
```

### useMemo & useCallback (Performance)

- **useMemo:** কোনো ভারী ক্যালকুলেশনের রেজাল্ট ক্যাশ (cache) করে রাখার জন্য।
- **useCallback:** কোনো ফাংশন যাতে বারবার নতুন করে তৈরি না হয়, তা নিশ্চিত করার জন্য।
  _নোট: এগুলো সব সময় ব্যবহার করবেন না, শুধুমাত্র পারফরম্যান্স সমস্যা হলে ব্যবহার করুন।_

---

## 7. Custom Hooks (Reusable Logic)

Custom Hook হলো সাধারণ জাভাস্ক্রিপ্ট ফাংশন যার নাম "use" দিয়ে শুরু হয় এবং এটি অন্যান্য হুক ব্যবহার করতে পারে।

### Example: useFetch

```jsx
// hooks/useFetch.js
import { useState, useEffect } from "react";

const useFetch = (url) => {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    const fetchData = async () => {
      try {
        const response = await fetch(url);
        if (!response.ok) throw new Error("Network response was not ok");
        const result = await response.json();
        setData(result);
      } catch (err) {
        setError(err);
      } finally {
        setLoading(false);
      }
    };

    fetchData();
  }, [url]);

  return { data, loading, error };
};

export default useFetch;
```

### Example: useToggle

```jsx
// hooks/useToggle.js
import { useState } from "react";

const useToggle = (initialValue = false) => {
  const [value, setValue] = useState(initialValue);
  const toggle = () => setValue(!value);
  return [value, toggle];
};
```

---

## 8. State Management Patterns

### Local State vs Global State

- **Local State:** শুধুমাত্র একটি কম্পোনেন্টে দরকার (যেমন: ফর্ম ইনপুট, টগল বাটন)। -> `useState`
- **Global State:** পুরো অ্যাপে দরকার (যেমন: ইউজার অথেনটিকেশন, থিম, কার্ট)। -> `Context API`, `Zustand`, `Redux`

### Lifting State Up

যখন দুটি চাইল্ড কম্পোনেন্টের একই স্টেট দরকার হয়, তখন তাদের প্যারেন্টে স্টেট ডিক্লেয়ার করে প্রপস হিসেবে পাঠাতে হয়।

### State Colocation

স্টেট সবসময় সেখানেই রাখুন যেখানে এটি ব্যবহার হচ্ছে। অপ্রয়োজনে সব স্টেট অ্যাপের টপে নিয়ে যাবেন না।

### When to use External Libraries

ছোট বা মাঝারি অ্যাপের জন্য `Context API` যথেষ্ট। খুব জটিল অ্যাপের জন্য `Zustand` (সহজ এবং মডার্ন) বা `Redux Toolkit` (ইন্ডাস্ট্রি স্ট্যান্ডার্ড) ব্যবহার করতে পারেন।
**Rule of Thumb:** `useState` দিয়ে শুরু করুন, সমস্যা হলে `Context`, তারপরও না হলে `Zustand`।

---

## 9. Forms in React

### Controlled vs Uncontrolled Components

- **Controlled:** React স্টেট ফর্মের ভ্যালু কন্ট্রোল করে। (Recommended ✅)
- **Uncontrolled:** DOM নিজেই ভ্যালু হ্যান্ডেল করে (`useRef` দিয়ে)।

### Handling Form Submission

```jsx
const SimpleForm = () => {
  const [name, setName] = useState("");

  const handleSubmit = (e) => {
    e.preventDefault(); // পেজ রিলোড বন্ধ করে
    console.log(name);
  };

  return (
    <form onSubmit={handleSubmit}>
      <input
        type="text"
        value={name}
        onChange={(e) => setName(e.target.value)}
      />
      <button type="submit">Submit</button>
    </form>
  );
};
```

### React Hook Form (Recommended Library)

বড় ফর্মের জন্য `react-hook-form` ব্যবহার করুন। এটি অনেক ফাস্ট এবং কম কোড লাগে।

```jsx
import { useForm } from "react-hook-form";

const HookForm = () => {
  const {
    register,
    handleSubmit,
    formState: { errors },
  } = useForm();
  const onSubmit = (data) => console.log(data);

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <input {...register("email", { required: true })} />
      {errors.email && <span>This field is required</span>}
      <button type="submit">Submit</button>
    </form>
  );
};
```

---

## 10. React Router (Navigation)

### Setup

```bash
npm install react-router-dom
```

### Basic Routing

`main.jsx` ফাইলে `BrowserRouter` দিয়ে অ্যাপ র‍্যাপ করুন।

```jsx
// App.jsx
import { Routes, Route, Link } from "react-router-dom";

function App() {
  return (
    <div>
      <nav>
        <Link to="/">Home</Link>
        <Link to="/about">About</Link>
      </nav>

      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
        <Route path="/users/:id" element={<UserProfile />} />
      </Routes>
    </div>
  );
}
```

### Hooks for Navigation

- **useNavigate:** প্রোগ্রাম্যাটিক্যালি পেজ চেঞ্জ করতে।
- **useParams:** URL প্যারামিটার (যেমন `:id`) ধরতে।

```jsx
import { useNavigate, useParams } from "react-router-dom";

const UserProfile = () => {
  const { id } = useParams();
  const navigate = useNavigate();

  return (
    <div>
      <h1>User ID: {id}</h1>
      <button onClick={() => navigate("/")}>Go Home</button>
    </div>
  );
};
```

---

## 11. API Integration (Real-World)

### Where to put API calls?

API কলগুলো সবসময় `/src/services` ফোল্ডারে আলাদা ফাইলে রাখা উচিত।

### Fetching Data with Async/Await

```jsx
// services/userService.js
import axios from "axios";

const API_URL = "https://api.example.com";

export const getUsers = async () => {
  const response = await axios.get(`${API_URL}/users`);
  return response.data;
};
```

### Handling Loading & Error States (CRITICAL!)

```jsx
const UserList = () => {
  const [users, setUsers] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    const fetchUsers = async () => {
      try {
        const data = await getUsers();
        setUsers(data);
      } catch (err) {
        setError("Failed to fetch users");
      } finally {
        setLoading(false);
      }
    };
    fetchUsers();
  }, []);

  if (loading) return <p>Loading...</p>;
  if (error) return <p>Error: {error}</p>;

  return (
    <ul>
      {users.map((user) => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  );
};
```

---

## 12. Styling in React

### CSS Modules

লোকাল স্কোপড স্টাইলিংয়ের জন্য। ফাইলের নাম `Button.module.css`।

```jsx
import styles from "./Button.module.css";
<button className={styles.btn}>Click</button>;
```

### Tailwind CSS (Modern Standard)

ইউটিলিটি ক্লাস দিয়ে দ্রুত ডিজাইন করার জন্য।

```jsx
<button className="bg-blue-500 text-white px-4 py-2 rounded hover:bg-blue-600">
  Click Me
</button>
```

### Styled Components (CSS-in-JS)

ডাইনামিক স্টাইলিংয়ের জন্য ভালো।

```jsx
import styled from "styled-components";

const Button = styled.button`
  background: ${(props) => (props.primary ? "blue" : "gray")};
  color: white;
`;
```

**Recommendation:** নতুন প্রজেক্টের জন্য **Tailwind CSS** সেরা চয়েস।

---

## 13. Professional Code Organization

### Folder Structure for 50+ Component Apps

```
/src
  /components
    /ui              # Reusable UI (Button, Input, Modal)
    /layout          # Layout components (Header, Sidebar)
    /features        # Feature-specific components (UserList, ProductCard)
  /pages             # Route components
  /hooks             # Global hooks
  /context           # Global context
  /services          # API services
  /utils             # Helpers
  /assets            # Static files
```

### Best Practices

- **PascalCase** ফাইলের নাম (যেমন `UserProfile.jsx`)।
- **One Component Per File:** এক ফাইলে একাধিক কম্পোনেন্ট রাখবেন না।
- **Index Files:** ইমপোর্ট ক্লিন রাখতে `index.js` ব্যবহার করুন।
- **Container vs Presentational:** লজিক এবং UI আলাদা রাখার চেষ্টা করুন (যদিও হুকস আসার পর এটি কম স্ট্রিক্ট)।

---

## 14. Modern React Patterns (2024-2025)

### ✅ Do's

- **Functional Components & Hooks:** ক্লাস কম্পোনেন্ট ভুলে যান।
- **Custom Hooks:** লজিক শেয়ার করার জন্য।
- **Compound Components:** ফ্লেক্সিবল কম্পোনেন্ট ডিজাইনের জন্য (যেমন `<Select><Option /></Select>`)।
- **Optional Chaining:** `user?.address?.city` (এরর এড়াতে)।

### ❌ Don'ts

- **Mutating State:** `state.value = 5` (কখনোই না!)।
- **Props Drilling:** ৩-৪ লেভেলের বেশি প্রপস পাস করবেন না, Context ব্যবহার করুন।
- **Index as Key:** লিস্ট রেন্ডারিংয়ে `key={index}` এড়িয়ে চলুন যদি লিস্টের আইটেম পরিবর্তন হয়।

---

## 15. Performance Optimization

### When to optimize?

"Premature optimization is the root of all evil." আগে কোড লিখুন, তারপর স্লো হলে অপটিমাইজ করুন।

### React.memo

কম্পোনেন্ট মেমোইজ করার জন্য, যাতে প্রপস পরিবর্তন না হলে রি-রেন্ডার না হয়।

```jsx
const MyComponent = React.memo(function MyComponent(props) {
  /* render using props */
});
```

### Code Splitting (Lazy Loading)

বড় অ্যাপের ইনিশিয়াল লোড টাইম কমাতে।

```jsx
import React, { Suspense } from "react";
const OtherComponent = React.lazy(() => import("./OtherComponent"));

function MyComponent() {
  return (
    <Suspense fallback={<div>Loading...</div>}>
      <OtherComponent />
    </Suspense>
  );
}
```

---

## 16. TypeScript with React

### Why TypeScript?

বড় প্রজেক্টে বাগ কমাতে এবং অটো-কমপ্লিশন পেতে TypeScript অপরিহার্য। জবের জন্য এটি এখন **Must-Have** স্কিল।

### Typing Props

```tsx
interface ButtonProps {
  label: string;
  onClick: () => void;
  disabled?: boolean; // Optional
}

const Button: React.FC<ButtonProps> = ({ label, onClick, disabled }) => {
  return (
    <button onClick={onClick} disabled={disabled}>
      {label}
    </button>
  );
};
```

### Typing Hooks

```tsx
const [user, setUser] = useState<User | null>(null);
```

---

## 17. React Best Practices & Code Quality

### ✅ ESLint & Prettier

সবসময় `eslint-config-react-app` বা `eslint-plugin-react-hooks` ব্যবহার করুন। এটি আপনাকে ভুল কোড লেখা থেকে বাঁচাবে।

### ✅ Meaningful Naming

- Component: `UserProfile` (PascalCase)
- Function/Hook: `getUser`, `useAuth` (camelCase)
- Constant: `MAX_USERS` (UPPER_SNAKE_CASE)

### ✅ Keep Components Small

একটি কম্পোনেন্ট যদি ২০০-৩০০ লাইনের বেশি হয়, তবে সেটি ভেঙে ছোট করুন। প্রতিটি কম্পোনেন্টের একটি নির্দিষ্ট কাজ থাকা উচিত (Single Responsibility Principle)।

### ✅ Accessibility (A11y)

- ইমেজে `alt` ট্যাগ দিন।
- বাটনে `aria-label` ব্যবহার করুন।
- ফর্ম ইনপুটে `label` ব্যবহার করুন।

---

## 18. Common Mistakes & Gotchas

### ❌ Infinite Loops in useEffect

ডিপেন্ডেন্সি অ্যারেতে ভুল ভেরিয়েবল দিলে বা স্টেট আপডেট করলে ইনফিনিট লুপ হতে পারে।

```jsx
// ❌ Wrong
useEffect(() => {
  setCount(count + 1); // Infinite Loop!
}, [count]);
```

### ❌ Stale Closures

`useEffect` এর ভেতরে পুরনো স্টেটের ভ্যালু পাওয়া। এটি ফিক্স করতে ফাংশনাল আপডেট ব্যবহার করুন `setCount(prev => prev + 1)`।

### ❌ Not Cleaning Up Side Effects

ইভেন্ট লিসেনার বা টাইমার সেট করলে `return` ফাংশনে সেটি ক্লিয়ার করতে ভুলবেন না।

---

## 19. Testing Basics (Important for Jobs)

### React Testing Library (RTL)

এখন এনজাইম (Enzyme) এর বদলে RTL ব্যবহার করা হয়। এটি ইউজার যেভাবে অ্যাপ ব্যবহার করে, সেভাবে টেস্ট করে।

### Example Test

```jsx
import { render, screen, fireEvent } from "@testing-library/react";
import Counter from "./Counter";

test("increments counter", () => {
  render(<Counter />);
  const button = screen.getByText(/increment/i);
  fireEvent.click(button);
  expect(screen.getByText(/count: 1/i)).toBeInTheDocument();
});
```

---

## 20. Integration with Modern Tools

### React + Next.js

SEO এবং সার্ভার সাইড রেন্ডারিং (SSR) এর জন্য Next.js সেরা। জবের জন্য এটি শেখা খুব জরুরি।

### React + TanStack Query

সার্ভার স্টেট (API data) ম্যানেজ করার জন্য এটি জাদুর মতো কাজ করে। `useEffect` দিয়ে ডাটা ফেচ করার চেয়ে এটি অনেক ভালো।

```jsx
const { data, isLoading } = useQuery(["users"], fetchUsers);
```

---

## 21. Real-World Complete Example: User Dashboard

### Folder Structure

```
/src
  /features/users
    UserList.jsx
    UserForm.jsx
    userSlice.js (if using Redux)
  /services/api.js
```

### Implementation Steps

1. **API Service:** `axios` দিয়ে ডাটা ফেচিং সেটআপ।
2. **State:** `useState` বা `TanStack Query` দিয়ে ডাটা রাখা।
3. **UI:** লোডিং স্পিনার, এরর মেসেজ এবং ডাটা টেবিল দেখানো।
4. **Actions:** ডিলিট বা এডিট বাটন হ্যান্ডেল করা।

---

## 22. Interview-Ready Knowledge

### Top Questions

1. **Virtual DOM কি এবং কিভাবে কাজ করে?** (Diffing & Reconciliation)
2. **React Lifecycle কি?** (Mounting, Updating, Unmounting)
3. **useEffect এর ডিপেন্ডেন্সি অ্যারে কিভাবে কাজ করে?**
4. **useMemo vs useCallback এর পার্থক্য কি?**
5. **Prop Drilling কি এবং কিভাবে সমাধান করবেন?** (Context, Redux)

### Code Challenges

- একটি Todo List বানানো (Add, Delete, Toggle)।
- API থেকে ডাটা এনে সার্চ/ফিল্টার করা।
- একটি কাউন্টার বানানো যা ১ সেকেন্ড পর পর বাড়ে।

---

## 23. Debugging React Apps

### React DevTools

ব্রাউজারে React DevTools এক্সটেনশন ইনস্টল করুন। এটি দিয়ে কম্পোনেন্ট ট্রি এবং স্টেট/প্রপস চেক করা যায়।

### Profiler

অ্যাপ কেন স্লো হচ্ছে তা দেখার জন্য DevTools এর Profiler ট্যাব ব্যবহার করুন। এটি দেখাবে কোন কম্পোনেন্ট কতবার রেন্ডার হচ্ছে।

---

## 24. Next Steps & Advanced Topics

React বেসিক শেষ করার পর যা শিখবেন:

1. **Next.js:** ফুলস্ট্যাক ফ্রেমওয়ার্ক।
2. **TypeScript:** টাইপ সেফটির জন্য।
3. **Redux Toolkit / Zustand:** কমপ্লেক্স স্টেট ম্যানেজমেন্ট।
4. **Unit Testing:** Jest & React Testing Library.

---

**শুভকামনা!** এই গাইডটি ফলো করলে এবং প্রজেক্ট বানালে আপনি নিশ্চিতভাবেই একজন দক্ষ React ডেভেলপার হিসেবে নিজেকে তৈরি করতে পারবেন।
