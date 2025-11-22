# TanStack Query v5: জুনিয়র ফ্রন্টএন্ড ডেভেলপারদের জন্য কমপ্লিট গাইড (Next.js App Router & JavaScript)

এই গাইডটি আপনাকে **TanStack Query v5** (যা আগে React Query নামে পরিচিত ছিল) একদম শুরু থেকে প্রফেশনাল লেভেল পর্যন্ত শিখতে সাহায্য করবে। এটি বিশেষ করে তাদের জন্য তৈরি যারা ইউরোপ বা আমেরিকার রিমোট জবের জন্য প্রস্তুতি নিচ্ছেন।

---

## ১. TanStack Query কী এবং কেন? (What & Why)

### TanStack Query কী?

সহজ কথায়, **TanStack Query** হলো React অ্যাপ্লিকেশনে **সার্ভার স্টেট (Server State)** ম্যানেজ করার জন্য একটি শক্তিশালী লাইব্রেরি। এটি আপনার অ্যাপের ডেটা ফেচিং (fetching), ক্যাশিং (caching), সিঙ্ক্রোনাইজেশন (synchronizing) এবং সার্ভার স্টেট আপডেট করার কাজকে অনেক সহজ করে দেয়।

### কেন এটি আধুনিক প্রজেক্টে ব্যবহার করা হয়?

সাধারণত `useEffect` এবং `useState` দিয়ে ডেটা ফেচ করতে গেলে আপনাকে লোডিং স্টেট, এরর হ্যান্ডলিং, এবং ডেটা ক্যাশিং ম্যানুয়ালি হ্যান্ডেল করতে হয়। TanStack Query এই সব কাজ অটোমেটিক্যালি করে দেয়। এটি অ্যাপকে ফাস্ট করে এবং কোডকে ক্লিন রাখে।

### কখন এটি ব্যবহার করবেন?

যখনই আপনার অ্যাপে কোনো এক্সটার্নাল API থেকে ডেটা আনার প্রয়োজন হবে, তখন TanStack Query ব্যবহার করা উচিত। তবে যদি শুধু ক্লায়েন্ট সাইড স্টেট (যেমন: মডাল ওপেন/ক্লোজ, ফর্ম ইনপুট) ম্যানেজ করতে হয়, তখন `useState` বা Zustand/Redux ব্যবহার করা ভালো।

---

## ২. কোর কনসেপ্ট (Core Concepts)

এই ৫টি মূল বিষয় বুঝলে আপনার জন্য TanStack Query শেখা পানির মতো সহজ হয়ে যাবে:

1.  **Query (কুয়েরি):** ডেটা নিয়ে আসার প্রক্রিয়া। যেমন: সার্ভার থেকে ইউজার লিস্ট আনা। (GET request)
2.  **Mutation (মিউটেশন):** ডেটা পরিবর্তন করার প্রক্রিয়া। যেমন: নতুন ইউজার তৈরি করা, আপডেট করা বা ডিলিট করা। (POST, PUT, DELETE requests)
3.  **Query Key (কুয়েরি কি):** প্রতিটি কুয়েরির একটি ইউনিক নাম বা ID। TanStack Query এই কি (Key) দিয়ে ডেটা চিনে রাখে এবং ক্যাশ (Cache) করে।
4.  **Stale Time (স্টেট টাইম):** কতক্ষণ পর্যন্ত ডেটা "ফ্রেশ" বা সতেজ থাকবে। এই সময়ের মধ্যে নতুন করে ফেচ হবে না, ক্যাশ থেকে ডেটা দেখাবে।
5.  **Invalidation (ইনভ্যালিডেশন):** যখন আমরা জানি যে সার্ভারের ডেটা চেঞ্জ হয়েছে (যেমন নতুন পোস্ট করার পর), তখন পুরনো ক্যাশ করা ডেটাকে "বাতিল" বা stale ঘোষণা করা, যাতে অটোমেটিক নতুন ডেটা ফেচ হয়।

**Mental Model:** ভাবুন TanStack Query আপনার অ্যাপ এবং সার্ভারের মাঝখানে একটি স্মার্ট অ্যাসিস্ট্যান্ট। আপনি যখন ডেটা চান, সে প্রথমে দেখে তার কাছে (Cache-এ) আছে কিনা। থাকলে সাথে সাথে দিয়ে দেয়, আর না থাকলে সার্ভার থেকে এনে দেয় এবং নিজের কাছে কপি রেখে দেয়।

---

## ৩. প্র্যাকটিক্যাল সেটআপ (Practical Setup)

আমরা **Next.js (App Router)** এবং **JavaScript** ব্যবহার করব।

### ১. ইনস্টলেশন

টার্মিনালে এই কমান্ডটি রান করুন:

```bash
npm install @tanstack/react-query
```

### ২. ফোল্ডার স্ট্রাকচার (Scalable Project)

একটি প্রফেশনাল প্রজেক্টে ফাইলগুলো এভাবে সাজানো উচিত:

```
src/
├── app/
│   ├── providers.js       # QueryClientProvider সেটআপ
│   ├── layout.js          # গ্লোবাল লেআউট
│   └── page.js            # হোম পেজ
├── components/            # UI কম্পোনেন্ট
├── hooks/                 # কাস্টম হুকস (সব কুয়েরি এখানে থাকবে)
│   ├── useTodos.js
│   └── useUser.js
├── services/              # API কল ফাংশন (Axios বা Fetch)
│   ├── api.js             # Axios ইনস্ট্যান্স
│   └── todoService.js     # নির্দিষ্ট ফিচারের API কল
└── utils/                 # ইউটিলিটি ফাংশন
```

### ৩. কনফিগারেশন (Providers Setup)

Next.js App Router-এ `QueryClientProvider` ব্যবহার করার জন্য একটি আলাদা ক্লায়েন্ট কম্পোনেন্ট তৈরি করতে হয়।

**`src/app/providers.js`**

```javascript
"use client";

import { QueryClient, QueryClientProvider } from "@tanstack/react-query";
import { ReactQueryDevtools } from "@tanstack/react-query-devtools";
import { useState } from "react";

export default function Providers({ children }) {
  // useState ব্যবহার করা জরুরি যাতে রি-রেন্ডারে ক্লায়েন্ট রিসেট না হয়
  const [queryClient] = useState(
    () =>
      new QueryClient({
        defaultOptions: {
          queries: {
            staleTime: 60 * 1000, // ১ মিনিট পর্যন্ত ডেটা ফ্রেশ থাকবে
          },
        },
      })
  );

  return (
    <QueryClientProvider client={queryClient}>
      {children}
      {/* DevTools ডিফল্টভাবে প্রোডাকশনে বন্ধ থাকে */}
      <ReactQueryDevtools initialIsOpen={false} />
    </QueryClientProvider>
  );
}
```

> **Note:** `ReactQueryDevtools` ব্যবহার করার জন্য আপনাকে এটি ইমপোর্ট করতে হবে:
> `import { ReactQueryDevtools } from '@tanstack/react-query-devtools';`
> এবং `npm install @tanstack/react-query-devtools` কমান্ড দিয়ে ইনস্টল করতে হবে।

**`src/app/layout.js`**

```javascript
import Providers from "./providers";
import "./globals.css";

export default function RootLayout({ children }) {
  return (
    <html lang="en">
      <body>
        <Providers>{children}</Providers>
      </body>
    </html>
  );
}
```

---

## ৪. প্রফেশনাল কোড অর্গানাইজেশন (Professional Code Organization)

কোড অগোছালো না করার জন্য আমরা **Service Layer Pattern** এবং **Custom Hooks** ব্যবহার করব।

### ✅ Service Layer (API Calls)

সরাসরি কম্পোনেন্টে `fetch` বা `axios` কল করবেন না। এগুলো `services` ফোল্ডারে রাখুন।

**`src/services/todoService.js`**

```javascript
import axios from "axios";

const API_URL = "https://jsonplaceholder.typicode.com/todos";

export const fetchTodos = async () => {
  const { data } = await axios.get(API_URL);
  return data;
};

export const createTodo = async (newTodo) => {
  const { data } = await axios.post(API_URL, newTodo);
  return data;
};
```

### ✅ Custom Hooks (TanStack Query Logic)

সব `useQuery` এবং `useMutation` লজিক `hooks` ফোল্ডারে থাকবে। এতে UI ক্লিন থাকে।

**`src/hooks/useTodos.js`**

```javascript
import { useQuery, useMutation, useQueryClient } from "@tanstack/react-query";
import { fetchTodos, createTodo } from "@/services/todoService";

// কুয়েরি কি (Key) কনস্ট্যান্ট হিসেবে রাখা ভালো প্র্যাকটিস
export const TODO_KEYS = {
  all: ["todos"],
};

export const useGetTodos = () => {
  return useQuery({
    queryKey: TODO_KEYS.all,
    queryFn: fetchTodos,
  });
};

export const useCreateTodo = () => {
  const queryClient = useQueryClient();

  return useMutation({
    mutationFn: createTodo,
    onSuccess: () => {
      // নতুন টুডু অ্যাড হলে লিস্ট রিফ্রেশ হবে
      queryClient.invalidateQueries({ queryKey: TODO_KEYS.all });
    },
  });
};
```

---

## ৫. মডার্ন সিনট্যাক্স ও স্ট্যান্ডার্ড (Modern Syntax)

- **Async/Await:** সবসময় `async/await` ব্যবহার করুন, `.then()` চেইন পরিহার করুন।
- **Arrow Functions:** ফাংশন ডিফাইন করতে অ্যারো ফাংশন ব্যবহার করুন।
- **Error Handling:** `try/catch` ব্লকের চেয়ে TanStack Query-র বিল্ট-ইন `isError` এবং `error` অবজেক্ট ব্যবহার করা বেশি সুবিধাজনক।

---

## ৬. কোড এক্সাম্পল (Real-world Use Cases: A to Z Implementation)

এখানে আমরা একটি **Todo List** ফিচার ইমপ্লিমেন্ট করব একদম প্রোডাকশন গ্রেড আর্কিটেকচার ফলো করে। আমরা দেখব কিভাবে `services`, `hooks`, এবং `components` একে অপরের সাথে কানেক্টেড থাকে।

### ধাপ ১: Axios Instance সেটআপ (Services)

প্রথমে আমরা একটি গ্লোবাল Axios ইনস্ট্যান্স তৈরি করব যাতে বারবার বেস URL লিখতে না হয়।

**`src/services/api.js`**

```javascript
import axios from "axios";

const api = axios.create({
  baseURL: "https://jsonplaceholder.typicode.com",
  headers: {
    "Content-Type": "application/json",
  },
});

export default api;
```

### ধাপ ২: API Calls ডিফাইন করা (Services)

এখন আমরা `todoService.js` ফাইলে স্পেসিফিক API কলগুলো লিখব। এখানে আমরা আমাদের তৈরি করা `api` ইনস্ট্যান্স ব্যবহার করব।

**`src/services/todoService.js`**

```javascript
import api from "./api";

// সব টুডু আনার জন্য
export const fetchTodos = async () => {
  const { data } = await api.get("/todos?_limit=10"); // ডেমোর জন্য ১০টা লিমিট দিলাম
  return data;
};

// নতুন টুডু অ্যাড করার জন্য
export const createTodo = async (newTodo) => {
  const { data } = await api.post("/todos", newTodo);
  return data;
};

// টুডু আপডেট করার জন্য (যেমন: completed মার্ক করা)
export const updateTodo = async ({ id, ...updates }) => {
  const { data } = await api.patch(`/todos/${id}`, updates);
  return data;
};
```

### ধাপ ৩: Custom Hooks তৈরি করা (Hooks)

এখন আমরা TanStack Query ব্যবহার করে এই সার্ভিসগুলোকে হুকে কনভার্ট করব।

**`src/hooks/useTodos.js`**

```javascript
import { useQuery, useMutation, useQueryClient } from "@tanstack/react-query";
import { fetchTodos, createTodo, updateTodo } from "@/services/todoService";

// Query Key ফ্যাক্টরি (Best Practice)
export const TODO_KEYS = {
  all: ["todos"],
  detail: (id) => ["todos", id],
};

// ১. ডেটা ফেচ করার হুক
export const useGetTodos = () => {
  return useQuery({
    queryKey: TODO_KEYS.all,
    queryFn: fetchTodos,
  });
};

// ২. ডেটা ক্রিয়েট করার হুক
export const useCreateTodo = () => {
  const queryClient = useQueryClient();

  return useMutation({
    mutationFn: createTodo,
    onSuccess: () => {
      // নতুন ডেটা অ্যাড হলে লিস্ট রিফ্রেশ হবে
      queryClient.invalidateQueries({ queryKey: TODO_KEYS.all });
    },
  });
};

// ৩. ডেটা আপডেট করার হুক
export const useUpdateTodo = () => {
  const queryClient = useQueryClient();

  return useMutation({
    mutationFn: updateTodo,
    onSuccess: () => {
      queryClient.invalidateQueries({ queryKey: TODO_KEYS.all });
    },
  });
};
```

### ধাপ ৪: UI কম্পোনেন্টে ব্যবহার (Components/Page)

ফাইনালি, আমরা আমাদের পেজে এই হুকগুলো ব্যবহার করব। দেখুন কোড কত ক্লিন থাকে!

**`src/app/page.js`**

```javascript
"use client";

import { useState } from "react";
import { useGetTodos, useCreateTodo, useUpdateTodo } from "@/hooks/useTodos";

export default function TodoPage() {
  // হুকস কল করা
  const { data: todos, isLoading, isError, error } = useGetTodos();
  const { mutate: addTodo, isPending: isAdding } = useCreateTodo();
  const { mutate: toggleTodo } = useUpdateTodo();

  const [title, setTitle] = useState("");

  // ফর্ম সাবমিট হ্যান্ডলার
  const handleSubmit = (e) => {
    e.preventDefault();
    if (!title) return;

    addTodo(
      { title, completed: false, userId: 1 },
      {
        onSuccess: () => {
          setTitle(""); // সফল হলে ইনপুট ক্লিয়ার
          alert("Todo added successfully!");
        },
        onError: () => {
          alert("Failed to add todo");
        },
      }
    );
  };

  // লোডিং এবং এরর স্টেট হ্যান্ডলিং
  if (isLoading)
    return <div className="text-center p-10">Loading todos...</div>;
  if (isError)
    return <div className="text-red-500 p-10">Error: {error.message}</div>;

  return (
    <div className="max-w-md mx-auto mt-10 p-6 bg-white rounded-xl shadow-md">
      <h1 className="text-2xl font-bold mb-6 text-gray-800">
        My Professional Todo App
      </h1>

      {/* Add Todo Form */}
      <form onSubmit={handleSubmit} className="flex gap-3 mb-8">
        <input
          type="text"
          value={title}
          onChange={(e) => setTitle(e.target.value)}
          className="border border-gray-300 p-3 flex-1 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 text-black"
          placeholder="What needs to be done?"
        />
        <button
          type="submit"
          disabled={isAdding}
          className="bg-blue-600 hover:bg-blue-700 text-white px-6 py-3 rounded-lg font-medium disabled:bg-blue-300 transition-colors"
        >
          {isAdding ? "Adding..." : "Add"}
        </button>
      </form>

      {/* Todo List */}
      <ul className="space-y-3">
        {todos?.map((todo) => (
          <li
            key={todo.id}
            className="p-4 bg-gray-50 border border-gray-100 rounded-lg flex items-center justify-between hover:bg-gray-100 transition-colors"
          >
            <span
              className={`text-gray-700 ${
                todo.completed ? "line-through text-gray-400" : ""
              }`}
            >
              {todo.title}
            </span>

            <button
              onClick={() =>
                toggleTodo({ id: todo.id, completed: !todo.completed })
              }
              className={`text-sm px-3 py-1 rounded-full border ${
                todo.completed
                  ? "text-green-600 border-green-200 bg-green-50"
                  : "text-yellow-600 border-yellow-200 bg-yellow-50"
              }`}
            >
              {todo.completed ? "Completed" : "Mark Done"}
            </button>
          </li>
        ))}
      </ul>
    </div>
  );
}
```

---

## ৭. বেস্ট প্র্যাকটিস ও অ্যান্টি-প্যাটার্ন (Best Practices)

### ✅ DO (কি করবেন)

1.  **Query Keys Factory:** কুয়েরি কিগুলো হার্ডকোড না করে একটি অবজেক্ট বা ফাংশনে রাখুন (যেমন `TODO_KEYS` উপরে দেখানো হয়েছে)।
2.  **Custom Hooks:** সবসময় `useQuery` লজিক কাস্টম হুকে র‍্যাপ করুন।
3.  **Loading/Error States:** সবসময় লোডিং এবং এরর স্টেট হ্যান্ডেল করুন।

### ❌ DON'T (কি করবেন না)

1.  **useEffect for Fetching:** ডেটা ফেচ করার জন্য `useEffect` ব্যবহার করবেন না যখন আপনার হাতে TanStack Query আছে।
2.  **Over-fetching:** দরকার নেই এমন ডেটা ফেচ করবেন না।
3.  **Destructuring without Rename:** `data` কে রিনেম করে মিনিংফুল নাম দিন (যেমন `const { data: todos } = ...`)।

---

## ৮. ইন্টিগ্রেশন গাইড (Integration Guide)

Next.js App Router-এ TanStack Query মূলত **Client Components**-এ ব্যবহৃত হয়। তবে আপনি চাইলে Server Component-এ ডেটা প্রি-ফেচ (Prefetch) করে Client Component-এ হাইড্রেট (Hydrate) করতে পারেন। এটি একটু অ্যাডভান্সড, তবে জুনিয়র হিসেবে শুরুতে ক্লায়েন্ট সাইড ফেচিং (উপরে দেখানো পদ্ধতি) জানলেই চলবে।

**Tools Integration:**

- **Axios:** API কলের জন্য সেরা।
- **React Hook Form:** ফর্ম হ্যান্ডলিংয়ের জন্য, যা মিউটেশনের সাথে চমৎকার কাজ করে।
- **Zod:** ডেটা ভ্যালিডেশনের জন্য।

---

## ৯. পারফরম্যান্স ও অপ্টিমাইজেশন (Performance)

1.  **Stale Time:** ডিফল্ট `staleTime` 0 থাকে, মানে প্রতিবার উইন্ডো ফোকাস করলে ফেচ হবে। এটি বাড়িয়ে (যেমন ১ মিনিট) সার্ভার রিকোয়েস্ট কমানো যায়।
2.  **Window Focus Refetching:** ডিফল্টভাবে ইউজার অন্য ট্যাবে গিয়ে ফিরে আসলে ডেটা রিফ্রেশ হয়। প্রয়োজন না হলে এটি বন্ধ করতে পারেন: `refetchOnWindowFocus: false`।
3.  **Pagination:** বড় লিস্টের জন্য `keepPreviousData: true` (v5 এ `placeholderData: keepPreviousData`) ব্যবহার করুন যাতে পেজ চেঞ্জ করার সময় লোডিং স্পিনার না দেখায়।

---

## ১০. ইন্টারভিউ প্রস্তুতি (Interview-Ready Knowledge)

**Top Questions:**

1.  **TanStack Query কেন ব্যবহার করব? Redux এর সাথে পার্থক্য কী?**
    - _উত্তর:_ TanStack Query সার্ভার স্টেট (API data) ম্যানেজ করে, আর Redux ক্লায়েন্ট স্টেট ম্যানেজ করে। সার্ভার ডেটার জন্য TanStack Query অনেক বেশি এফিশিয়েন্ট কারণ এতে ক্যাশিং, রি-ফেচিং বিল্ট-ইন থাকে।
2.  **`staleTime` এবং `gcTime` (cacheTime) এর পার্থক্য কী?**
    - _উত্তর:_ `staleTime` হলো কতক্ষণ ডেটা "ফ্রেশ" থাকবে (রি-ফেচ হবে না)। `gcTime` হলো অব্যবহৃত ডেটা কতক্ষণ মেমোরিতে থাকবে ডিলিট হওয়ার আগে।
3.  **Query Invalidation কী?**
    - _উত্তর:_ ম্যানুয়ালি ক্যাশ ক্লিয়ার করে নতুন ডেটা ফেচ করার প্রক্রিয়া।

---

## ১১. সমস্যা ও সমাধান (Gotchas & Troubleshooting)

- **সমস্যা:** ডেটা আপডেট করার পর UI আপডেট হচ্ছে না।
  - **সমাধান:** মিউটেশনের `onSuccess`-এ `queryClient.invalidateQueries` কল করেছেন কিনা চেক করুন।
- **সমস্যা:** "No QueryClient set, use QueryClientProvider" এরর।
  - **সমাধান:** আপনার অ্যাপটি `QueryClientProvider` দিয়ে র‍্যাপ করা নেই। `layout.js` বা `providers.js` চেক করুন।

---

## ১২. রিয়েল প্রজেক্ট চেকলিস্ট (Real Project Checklist)

নতুন প্রজেক্ট শুরু করার সময় এই ধাপগুলো অনুসরণ করুন:

- [ ] `npm install @tanstack/react-query axios`
- [ ] `src/services/api.js` তৈরি করুন (Axios instance সেটআপ)।
- [ ] `src/app/providers.js` তৈরি করুন এবং কনফিগার করুন।
- [ ] `src/app/layout.js`-এ Provider র‍্যাপ করুন।
- [ ] `src/hooks` ফোল্ডার তৈরি করুন সব কুয়েরি হুকের জন্য।
- [ ] `src/services` ফোল্ডার তৈরি করুন API ফাংশনগুলোর জন্য।

---

## ১৩. পরবর্তী ধাপ (Next Steps)

**Mini Project Idea:**
একটি **"Product Dashboard"** তৈরি করুন যেখানে:

1.  প্রোডাক্ট লিস্ট দেখাবে (Pagination সহ)।
2.  নতুন প্রোডাক্ট অ্যাড করা যাবে (Mutation)।
3.  প্রোডাক্ট ডিলিট করা যাবে।

**Resources:**

- [TanStack Query Official Docs](https://tanstack.com/query/latest)
- [TkDodo's Blog](https://tkdodo.eu/blog/practical-react-query) (অত্যন্ত জনপ্রিয় এবং ইন-ডেপথ ব্লগের জন্য)

শুভকামনা! এই গাইডটি ফলো করলে আপনি নিঃসন্দেহে একজন কনফিডেন্ট জুনিয়র ডেভেলপার হিসেবে নিজেকে তৈরি করতে পারবেন।
