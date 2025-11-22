# Axios কমপ্লিট লার্নিং গাইড (২০২৪-২০২৫) - জুনিয়র ফ্রন্টএন্ড ডেভেলপারদের জন্য

এই গাইডটি আপনাকে **Axios** শিখতে সাহায্য করবে একদম শুরু থেকে প্রফেশনাল লেভেল পর্যন্ত। এটি বিশেষ করে যারা রিমোট জবের জন্য প্রস্তুতি নিচ্ছেন তাদের জন্য তৈরি। আমরা এখানে **Next.js (App Router)**, **Tailwind CSS**, এবং **JavaScript** ব্যবহার করব।

---

## ১. Axios কি এবং কেন? (What & Why)

**Axios কি?**
Axios হলো একটি প্রমিজ-বেসড (promise-based) HTTP ক্লায়েন্ট যা ব্রাউজার এবং node.js এ কাজ করে। সহজ কথায়, আপনার ফ্রন্টএন্ড অ্যাপ্লিকেশন (যেমন React বা Next.js) থেকে ব্যাকএন্ড সার্ভার বা ডাটাবেস থেকে ডাটা আনা-নেওয়া করার জন্য এটি ব্যবহৃত হয়।

**কেন এটি মডার্ন প্রজেক্টে ব্যবহৃত হয়?**
যদিও জাভাস্ক্রিপ্টে বিল্ট-ইন `fetch` API আছে, তবুও প্রফেশনালরা Axios পছন্দ করেন কারণ:

- এটি অটোমেটিক JSON ডাটা ট্রান্সফর্ম করে (fetch এ `res.json()` ম্যানুয়ালি করতে হয়)।
- **Interceptors** এর মাধ্যমে রিকোয়েস্ট বা রেসপন্স মাঝপথে মডিফাই করা যায় (যেমন অটোমেটিক টোকেন পাঠানো)।
- এরর হ্যান্ডলিং অনেক সহজ এবং বিস্তারিত।

**কখন ব্যবহার করবেন?**
যখন আপনার প্রজেক্টে অনেক বেশি API কল থাকে, অথেন্টিকেশন (লগিন/রেজিস্ট্রেশন) হ্যান্ডেল করতে হয়, অথবা আপনি ক্লিন কোড লিখতে চান। ছোট প্রজেক্টের জন্য `fetch` ঠিক আছে, কিন্তু বড় অ্যাপ্লিকেশনে Axios স্ট্যান্ডার্ড।

---

## ২. মূল কনসেপ্ট (Core Concepts)

এই ৫টি কনসেপ্ট আপনাকে অবশ্যই বুঝতে হবে:

১. **HTTP Methods (CRUD):**

- **GET**: ডাটা নিয়ে আসা (Read)।
- **POST**: নতুন ডাটা পাঠানো (Create)।
- **PUT/PATCH**: ডাটা আপডেট করা (Update)।
- **DELETE**: ডাটা মুছে ফেলা (Delete)।

২. **Request & Response:**

- **Request**: আপনি সার্ভারকে যা পাঠাচ্ছেন (হেডার, বডি)।
- **Response**: সার্ভার আপনাকে যা ফেরত দিচ্ছে (ডাটা, স্ট্যাটাস কোড)।

৩. **Headers:**

- মেটা-ডাটা, যেমন `Authorization` টোকেন বা ডাটার টাইপ (`Content-Type: application/json`)।

৪. **Async/Await:**

- কোডকে "অপেক্ষা" করতে বলা যতক্ষণ না সার্ভার থেকে ডাটা আসে।

৫. **Interceptors (মিডলম্যান):**

- রিকোয়েস্ট বা রেসপন্স মাঝপথে চেক বা পরিবর্তন করার সিস্টেম।

---

## ৩. প্র্যাকটিক্যাল সেটআপ (Practical Setup)

**ইনস্টলেশন:**

```bash
npm install axios @tanstack/react-query
```

_(নোট: আমরা TanStack Query ও ইনস্টল করলাম কারণ প্রফেশনাল জবে Axios এর সাথে এটি ব্যবহার করা হয়)_

**ফোল্ডার স্ট্রাকচার (Scalable Project):**

```
src/
├── app/                 # Next.js App Router পেজ
├── components/          # UI কম্পোনেন্ট
├── hooks/               # Custom Hooks (TanStack Query)
│   └── usePosts.js
├── lib/                 # কনফিগারেশন ফাইল
│   └── axios.js         # গ্লোবাল Axios ইনস্ট্যান্স
├── services/            # সব API কল এখানে থাকবে
│   ├── authService.js
│   └── postService.js
└── utils/               # ছোট হেল্পার ফাংশন
```

---

## ৪. প্রফেশনাল কোড অর্গানাইজেশন (Professional Code Organization)

আমরা একটি **Singleton Instance** তৈরি করব এবং সেখানে অ্যাডভান্সড ইন্টারসেপ্টর যোগ করব।

**ফাইল: `src/lib/axios.js`**

```javascript
import axios from "axios";

// ১. গ্লোবাল ইনস্ট্যান্স তৈরি
const api = axios.create({
  baseURL: process.env.NEXT_PUBLIC_API_URL || "https://api.example.com/v1",
  headers: {
    "Content-Type": "application/json",
  },
  timeout: 10000,
});

// ২. রিকোয়েস্ট ইন্টারসেপ্টর (টোকেন যোগ করা)
api.interceptors.request.use(
  (config) => {
    const token =
      typeof window !== "undefined" ? localStorage.getItem("token") : null;
    if (token) {
      config.headers.Authorization = `Bearer ${token}`;
    }
    return config;
  },
  (error) => Promise.reject(error)
);

// ৩. রেসপন্স ইন্টারসেপ্টর (অটো লগআউট হ্যান্ডলিং)
api.interceptors.response.use(
  (response) => response,
  (error) => {
    // যদি 401 (Unauthorized) এরর আসে, মানে টোকেন মেয়াদোত্তীর্ণ
    if (error.response && error.response.status === 401) {
      if (typeof window !== "undefined") {
        localStorage.removeItem("token"); // টোকেন মুছে ফেলা
        window.location.href = "/login"; // লগিন পেজে রিডাইরেক্ট
      }
    }
    return Promise.reject(error);
  }
);

export default api;
```

**ফাইল: `src/services/postService.js`**

```javascript
import api from "@/lib/axios";

// সাধারণ GET
export const getPosts = async () => {
  const response = await api.get("/posts");
  return response.data;
};

// প্যারামিটার সহ GET (Search & Pagination)
export const getFilteredPosts = async (page, searchTerm) => {
  const response = await api.get("/posts", {
    params: {
      _page: page,
      _limit: 10,
      q: searchTerm, // সার্চ কুয়েরি
    },
  });
  return response.data;
};

export const createPost = async (postData) => {
  const response = await api.post("/posts", postData);
  return response.data;
};
```

---

## ৫. অ্যাডভান্সড ডাটা ফেচিং (TanStack Query + Axios) 🔥

প্রফেশনাল জবে `useEffect` দিয়ে ডাটা ফেচ করা হয় না। **TanStack Query** ব্যবহার করা হয় কারণ এটি লোডিং, এরর, ক্যাশিং এবং রি-ফেচিং অটোমেটিক হ্যান্ডেল করে।

**ধাপ ১: কাস্টম হুক তৈরি করা (`src/hooks/usePosts.js`)**

```javascript
import { useQuery, useMutation, useQueryClient } from "@tanstack/react-query";
import { getPosts, createPost } from "@/services/postService";

// ডাটা আনার হুক
export const usePosts = () => {
  return useQuery({
    queryKey: ["posts"], // ইউনিক কি (Key)
    queryFn: getPosts, // Axios ফাংশন
    staleTime: 1000 * 60 * 5, // ৫ মিনিট ডাটা ফ্রেশ থাকবে
  });
};

// ডাটা পাঠানোর হুক
export const useCreatePost = () => {
  const queryClient = useQueryClient();

  return useMutation({
    mutationFn: createPost,
    onSuccess: () => {
      // পোস্ট তৈরি হলে লিস্ট অটোমেটিক রিফ্রেশ হবে
      queryClient.invalidateQueries(["posts"]);
    },
  });
};
```

**ধাপ ২: কম্পোনেন্টে ব্যবহার (`src/app/posts/page.js`)**

```javascript
"use client";

import { usePosts } from "@/hooks/usePosts";

export default function PostsPage() {
  // এক লাইনে লোডিং, এরর এবং ডাটা হ্যান্ডলিং!
  const { data: posts, isLoading, error } = usePosts();

  if (isLoading) return <div>লোড হচ্ছে...</div>;
  if (error) return <div>সমস্যা হয়েছে: {error.message}</div>;

  return (
    <div className="p-4">
      {posts.map((post) => (
        <div key={post.id} className="border p-4 mb-2 rounded shadow">
          <h3 className="font-bold">{post.title}</h3>
        </div>
      ))}
    </div>
  );
}
```

---

## ৬. মডার্ন সিনট্যাক্স ও স্ট্যান্ডার্ড

✅ **Do (করবেন):**

- `async/await` ব্যবহার করুন।
- `params` অবজেক্ট ব্যবহার করে কুয়েরি প্যারামিটার পাঠান (ম্যানুয়ালি `?page=1&q=search` স্ট্রিং বানাবেন না)।
- API লজিক `services` ফোল্ডারে এবং হুক `hooks` ফোল্ডারে রাখুন।

❌ **Don't (করবেন না):**

- কম্পোনেন্টের ভেতর সরাসরি `axios` কল করা।
- `.then().catch()` চেইন ব্যবহার করা (যদি না বিশেষ প্রয়োজন হয়)।

---

## ৭. ইন্টারভিউ প্রস্তুতি (Interview Prep)

**Top Questions:**

1. **Axios Interceptor কি? রিয়েল লাইফ উদাহরণ দিন।**

   - _উত্তর:_ ইন্টারসেপ্টর হলো মিডলওয়্যার যা রিকোয়েস্ট/রেসপন্স থামিয়ে মডিফাই করতে পারে। যেমন: প্রতিটা রিকোয়েস্টে অটোমেটিক `Authorization` হেডার যোগ করা বা `401` এরর আসলে ইউজারকে লগআউট করানো।

2. **Axios vs Fetch?**

   - _উত্তর:_ Axios এ কোড কম লিখতে হয়, অটো JSON পার্সিং হয়, এবং ইন্টারসেপ্টর সাপোর্ট আছে যা `fetch` এ নেই।

3. **কিভাবে ডুপ্লিকেট রিকোয়েস্ট ক্যান্সেল করবেন?**
   - _উত্তর:_ `AbortController` ব্যবহার করে Axios রিকোয়েস্ট ক্যান্সেল করা যায়। এটি সার্চ বারে টাইপ করার সময় খুব কাজে লাগে (Debouncing এর সাথে)।

---

## ৮. রিয়েল প্রজেক্ট চেকলিস্ট (Checklist)

1. [ ] `npm install axios @tanstack/react-query`
2. [ ] `.env.local` এ API URL সেট করা।
3. [ ] `src/lib/axios.js` এ ইন্টারসেপ্টর সহ সেটআপ করা।
4. [ ] `src/services/` এ API ফাংশন লেখা।
5. [ ] `src/hooks/` এ TanStack Query হুক তৈরি করা।
6. [ ] কম্পোনেন্টে হুক ব্যবহার করে ডাটা দেখানো।

---

## ৯. সম্পূর্ণ মিনি প্রজেক্ট: Task Manager (Full CRUD) 🚀

এখন আমরা যা শিখলাম তা দিয়ে একটি **Task Manager** অ্যাপ বানাব। এখানে আমাদের নিজস্ব একটি ফেইক ব্যাকএন্ড থাকবে `json-server` ব্যবহার করে এবং আমরা **Create, Read, Update, Delete (CRUD)** সব অপারেশন ইমপ্লিমেন্ট করব।

### ধাপ ১: সেটআপ (Setup)

প্রথমে `json-server` ইনস্টল করুন:

```bash
npm install -D json-server
```

প্রজেক্টের রুটে `db.json` ফাইল তৈরি করুন:

```json
{
  "todos": [
    { "id": 1, "title": "Axios শিখতে হবে", "completed": false },
    { "id": 2, "title": "TanStack Query প্র্যাকটিস", "completed": true }
  ]
}
```

`package.json` এ স্ক্রিপ্ট যোগ করুন:

```json
"scripts": {
  "dev": "next dev",
  "server": "json-server --watch db.json --port 3001"
}
```

টার্মিনালে `npm run server` দিয়ে ব্যাকএন্ড চালু করুন।

---

### ধাপ ২: Axios কনফিগারেশন

`src/lib/axios.js` এ `baseURL` আপডেট করুন:

```javascript
baseURL: 'http://localhost:3001',
```

---

### ধাপ ৩: সার্ভিস লেয়ার (Full CRUD API)

ফাইল: `src/services/todoService.js`

```javascript
import api from "@/lib/axios";

// READ (সব টাস্ক আনা)
export const getTodos = async () => {
  const { data } = await api.get("/todos");
  return data;
};

// CREATE (নতুন টাস্ক যোগ করা)
export const addTodo = async (title) => {
  const { data } = await api.post("/todos", {
    title,
    completed: false,
  });
  return data;
};

// DELETE (টাস্ক মুছে ফেলা)
export const deleteTodo = async (id) => {
  await api.delete(`/todos/${id}`);
  return id;
};

// UPDATE (টাস্ক স্ট্যাটাস বা টাইটেল আপডেট করা - PATCH)
export const updateTodo = async ({ id, ...updates }) => {
  const { data } = await api.patch(`/todos/${id}`, updates);
  return data;
};
```

---

### ধাপ ৪: হুকস লেয়ার (TanStack Query)

ফাইল: `src/hooks/useTodos.js`

```javascript
import { useQuery, useMutation, useQueryClient } from "@tanstack/react-query";
import {
  getTodos,
  addTodo,
  deleteTodo,
  updateTodo,
} from "@/services/todoService";

export const useTodos = () => {
  return useQuery({
    queryKey: ["todos"],
    queryFn: getTodos,
  });
};

export const useTodoMutations = () => {
  const queryClient = useQueryClient();

  const onSuccess = () => queryClient.invalidateQueries(["todos"]);

  return {
    addMutation: useMutation({ mutationFn: addTodo, onSuccess }),
    deleteMutation: useMutation({ mutationFn: deleteTodo, onSuccess }),
    updateMutation: useMutation({ mutationFn: updateTodo, onSuccess }),
  };
};
```

---

### ধাপ ৫: ইউজার ইন্টারফেস (UI with Edit Mode)

ফাইল: `src/app/todos/page.js`

```javascript
"use client";

import { useState } from "react";
import { useTodos, useTodoMutations } from "@/hooks/useTodos";

export default function TodoApp() {
  const [text, setText] = useState("");
  const [editingId, setEditingId] = useState(null);
  const [editText, setEditText] = useState("");

  const { data: todos, isLoading, error } = useTodos();
  const { addMutation, deleteMutation, updateMutation } = useTodoMutations();

  // নতুন টাস্ক সাবমিট
  const handleSubmit = (e) => {
    e.preventDefault();
    if (!text.trim()) return;
    addMutation.mutate(text);
    setText("");
  };

  // এডিট শুরু করা
  const startEdit = (todo) => {
    setEditingId(todo.id);
    setEditText(todo.title);
  };

  // এডিট সেভ করা
  const saveEdit = (id) => {
    updateMutation.mutate({ id, title: editText });
    setEditingId(null);
  };

  if (isLoading) return <div className="text-center mt-10">লোড হচ্ছে...</div>;
  if (error)
    return (
      <div className="text-center mt-10 text-red-500">এরর: {error.message}</div>
    );

  return (
    <div className="max-w-md mx-auto mt-10 p-6 bg-white rounded-xl shadow-lg">
      <h1 className="text-2xl font-bold mb-6 text-gray-800">
        Task Manager (CRUD)
      </h1>

      {/* Add Form */}
      <form onSubmit={handleSubmit} className="flex gap-2 mb-6">
        <input
          type="text"
          value={text}
          onChange={(e) => setText(e.target.value)}
          placeholder="নতুন কাজ..."
          className="flex-1 p-2 border rounded"
        />
        <button
          type="submit"
          className="bg-blue-600 text-white px-4 py-2 rounded"
        >
          Add
        </button>
      </form>

      {/* List */}
      <ul className="space-y-3">
        {todos?.map((todo) => (
          <li
            key={todo.id}
            className="flex items-center justify-between p-3 bg-gray-50 rounded"
          >
            <div className="flex items-center gap-3 flex-1">
              <input
                type="checkbox"
                checked={todo.completed}
                onChange={() =>
                  updateMutation.mutate({
                    id: todo.id,
                    completed: !todo.completed,
                  })
                }
                className="w-5 h-5"
              />

              {editingId === todo.id ? (
                <div className="flex gap-2 flex-1">
                  <input
                    value={editText}
                    onChange={(e) => setEditText(e.target.value)}
                    className="p-1 border rounded flex-1"
                  />
                  <button
                    onClick={() => saveEdit(todo.id)}
                    className="text-green-600 text-sm"
                  >
                    Save
                  </button>
                  <button
                    onClick={() => setEditingId(null)}
                    className="text-gray-500 text-sm"
                  >
                    Cancel
                  </button>
                </div>
              ) : (
                <span
                  className={`flex-1 cursor-pointer ${
                    todo.completed ? "line-through text-gray-400" : ""
                  }`}
                  onClick={() => startEdit(todo)} // ক্লিক করলে এডিট মোড
                  title="Click to edit"
                >
                  {todo.title}
                </span>
              )}
            </div>

            <button
              onClick={() => deleteMutation.mutate(todo.id)}
              className="text-red-500 ml-2"
            >
              ✕
            </button>
          </li>
        ))}
      </ul>
    </div>
  );
}
```

---

## ১০. পরবর্তী ধাপ (Next Steps)

**রিসোর্স:**

- [TanStack Query Docs](https://tanstack.com/query/latest)
- [Axios Docs](https://axios-http.com/)
- [JSON Server](https://github.com/typicode/json-server)

_শুভকামনা! এই প্রজেক্টটি সম্পন্ন করলে আপনি একজন জুনিয়র ডেভেলপার হিসেবে পুরোপুরি প্রস্তুত।_

```

```
