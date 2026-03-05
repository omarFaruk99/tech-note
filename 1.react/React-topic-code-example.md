# React Custom Hooks এবং Context API: ফাউন্ডেশন থেকে প্রোডাকশন লেভেল গাইড

## 📑 সূচিপত্র (Index)

1.  **🪝 Part 1: Custom Hooks**

    - [Custom Hook কি এবং এর উদ্দেশ্য](#১-custom-hook-কি-এবং-এর-উদ্দেশ্য-কি-what--purpose)
    - [কিভাবে কাজ করে](#২-এটি-কিভাবে-কাজ-করে-how-it-works)
    - [সিনট্যাক্স](#৩-সিনট্যাক্স-syntax)
    - [Use Case 1: useFetch (Data Fetching)](#use-case-1-usefetch-data-fetching)
    - [Use Case 2: useLocalStorage (Persisting State)](#use-case-2-uselocalstorage-persisting-state)
    - [Use Case 3: useDebounce (Performance Optimization)](#use-case-3-usedebounce-performance-optimization)

2.  **🌐 Part 2: Context API**
    - [Context API কি এবং এর উদ্দেশ্য](#১-context-api-কি-এবং-এর-উদ্দেশ্য-কি-what--purpose-1)
    - [কিভাবে কাজ করে](#২-এটি-কিভাবে-কাজ-করে-how-it-works-1)
    - [সিনট্যাক্স](#৩-সিনট্যাক্স-syntax-1)
    - [Use Case 1: Theme Context](#use-case-1-theme-context-darklight-mode)
    - [Use Case 2: Auth Context](#use-case-2-auth-context-user-authentication)
    - [Use Case 3: Toast Context](#use-case-3-toastnotification-context)

---

## 🪝 Part 1: Custom Hooks

### ১. Custom Hook কি এবং এর উদ্দেশ্য কি? (What & Purpose)

**কি:** Custom Hook হলো সাধারণ JavaScript ফাংশন, যার নাম অবশ্যই `use` দিয়ে শুরু হয় (যেমন: `useFetch`, `useAuth`)। এটি React এর বিল্ট-ইন হুকগুলো (useState, useEffect ইত্যাদি) ব্যবহার করে তৈরি করা হয়।

**উদ্দেশ্য:**

- **Logic Reusability:** একই লজিক বারবার বিভিন্ন কম্পোনেন্টে না লিখে একবার লিখে সব জায়গায় ব্যবহার করা।
- **Clean Code:** কম্পোনেন্টকে ক্লিন এবং ছোট রাখা। জটিল লজিকগুলো হুকের মধ্যে লুকিয়ে রাখা (Abstraction)।
- **Separation of Concerns:** UI এবং Business Logic আলাদা করা।

### ২. এটি কিভাবে কাজ করে? (How it works)

Custom Hook সাধারণ ফাংশনের মতোই কাজ করে। যখন আপনি একটি কম্পোনেন্টে Custom Hook কল করেন, তখন সেই হুকের ভেতরের `useState` বা `useEffect` গুলো ওই নির্দিষ্ট কম্পোনেন্টের জন্যই আলাদাভাবে রান করে। অর্থাৎ, এক কম্পোনেন্টে হুকের স্টেট পরিবর্তন করলে অন্য কম্পোনেন্টে এর প্রভাব পড়ে না।

### ৩. সিনট্যাক্স (Syntax)

```javascript
// useMyHook.js
import { useState, useEffect } from "react";

// ১. নাম অবশ্যই 'use' দিয়ে শুরু হবে
const useMyHook = (initialValue) => {
  // ২. এখানে বিল্ট-ইন হুক ব্যবহার করা যাবে
  const [value, setValue] = useState(initialValue);

  // ৩. লজিক ইমপ্লিমেন্টেশন
  const updateValue = () => setValue(value + 1);

  // ৪. যা প্রয়োজন তা রিটার্ন করা (Array বা Object)
  return [value, updateValue];
};

export default useMyHook;
```

### ৪. ৩টি রিয়েল-ওয়ার্ল্ড ইউজ কেস (Real-world Use Cases)

#### Use Case 1: `useFetch` (Data Fetching)

সবচেয়ে কমন ব্যবহার। বারবার `useEffect` এবং `fetch` না লিখে একটি হুক ব্যবহার করা।

```javascript
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

**ব্যবহার (Usage Example):**

```javascript
import useFetch from "./hooks/useFetch";

const UserList = () => {
  // হুক কল করা হচ্ছে
  const { data, loading, error } = useFetch(
    "https://jsonplaceholder.typicode.com/users"
  );

  if (loading) return <p>Loading users...</p>;
  if (error) return <p>Error loading users!</p>;

  return (
    <ul>
      {data.map((user) => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  );
};
```

#### Use Case 1.1: `useApi` (For Create, Update, Delete)

**প্রশ্ন:** `useFetch` কি শুধু GET এর জন্য? Create/Update/Delete কিভাবে করব?
**উত্তর:** `useFetch` সাধারণত কম্পোনেন্ট লোড হওয়ার সাথে সাথে ডাটা আনার (GET) জন্য ব্যবহার হয় (`useEffect` দিয়ে)। কিন্তু Create, Update বা Delete অটোমেটিক হতে নেই, এগুলো ইউজারের অ্যাকশন (যেমন বাটন ক্লিক) এর পর হতে হয়। এর জন্য আমরা আলাদা একটি হুক ব্যবহার করতে পারি, ধরুন নাম দিলাম `useApi`।

```javascript
// hooks/useApi.js
import { useState } from "react";

const useApi = () => {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(false);
  const [error, setError] = useState(null);

  const request = async (url, method = "GET", body = null) => {
    setLoading(true);
    setError(null);
    try {
      const options = {
        method,
        headers: { "Content-Type": "application/json" },
      };
      if (body) options.body = JSON.stringify(body);

      const response = await fetch(url, options);
      if (!response.ok) throw new Error("Request failed");

      const result = await response.json();
      setData(result);
      return result; // সফল হলে ডাটা রিটার্ন করবে
    } catch (err) {
      setError(err.message);
      throw err; // এরর হলে তা থ্রো করবে যাতে কম্পোনেন্টে catch করা যায়
    } finally {
      setLoading(false);
    }
  };

  return { request, data, loading, error };
};

export default useApi;
```

**ব্যবহার (Usage Example for POST/DELETE):**

```javascript
import useApi from "./hooks/useApi";

const CreateUser = () => {
  const { request, loading, error } = useApi();

  const handleCreateUser = async () => {
    try {
      await request("https://api.example.com/users", "POST", {
        name: "Rahim",
        age: 25,
      });
      alert("User Created Successfully!");
    } catch (err) {
      alert("Failed to create user");
    }
  };

  return (
    <div>
      <button onClick={handleCreateUser} disabled={loading}>
        {loading ? "Creating..." : "Create User"}
      </button>
      {error && <p style={{ color: "red" }}>{error}</p>}
    </div>
  );
};

> [!NOTE]
> **Real World / Industry Standard (প্রো টিপ):**
> ছোট বা মাঝারি প্রজেক্টে উপরের `useFetch` বা `useApi` হুকগুলো চমৎকার কাজ করে। তবে **বড় প্রোডাকশন লেভেল অ্যাপ্লিকেশনে** আমরা সাধারণত **[TanStack Query (React Query)](https://tanstack.com/query/latest)** বা **SWR** ব্যবহার করি।
> *   **কেন?** কারণ এরা অটোমেটিক ক্যাশিং (Caching), রি-ফেচিং (Refetching), এবং লোডিং স্টেট ম্যানেজমেন্ট অনেক বেশি এফিশিয়েন্টলি হ্যান্ডেল করে।
> *   **তাহলে Custom Hook কেন শিখব?** কারণ React Query এর ভেতরেও এই একই লজিক কাজ করে। তাছাড়া সব লজিক (যেমন ফর্ম হ্যান্ডলিং, ইভেন্ট লিসেনার) এর জন্য লাইব্রেরি থাকে না, তখন Custom Hook ই ভরসা।

```

#### Use Case 2: `useLocalStorage` (Persisting State)

ব্রাউজারের লোকাল স্টোরেজে ডাটা সেভ এবং রিড করার জন্য।

```javascript
// hooks/useLocalStorage.js
import { useState, useEffect } from "react";

const useLocalStorage = (key, initialValue) => {
  // ইনিশিয়াল লোড
  const [value, setValue] = useState(() => {
    try {
      const item = window.localStorage.getItem(key);
      return item ? JSON.parse(item) : initialValue;
    } catch (error) {
      console.error(error);
      return initialValue;
    }
  });

  // ভ্যালু চেঞ্জ হলে লোকাল স্টোরেজ আপডেট
  useEffect(() => {
    window.localStorage.setItem(key, JSON.stringify(value));
  }, [key, value]);

  return [value, setValue];
};

export default useLocalStorage;
```

**ব্যবহার (Usage Example):**

```javascript
import useLocalStorage from "./hooks/useLocalStorage";

const ThemeToggler = () => {
  // হুক ব্যবহার করে থিম স্টেট তৈরি, যা রিফ্রেশ দিলেও থাকবে
  const [theme, setTheme] = useLocalStorage("app-theme", "light");

  return (
    <div
      style={{
        background: theme === "dark" ? "#333" : "#fff",
        color: theme === "dark" ? "#fff" : "#000",
        padding: "20px",
      }}
    >
      <p>Current Theme: {theme}</p>
      <button onClick={() => setTheme(theme === "light" ? "dark" : "light")}>
        Toggle Theme
      </button>
    </div>
  );
};
```

#### Use Case 3: `useDebounce` (Performance Optimization)

সার্চ ইনপুটের জন্য খুব জরুরি। ইউজার টাইপ করা থামালে কিছুক্ষণ পর API কল হবে।

```javascript
// hooks/useDebounce.js
import { useState, useEffect } from "react";

const useDebounce = (value, delay) => {
  const [debouncedValue, setDebouncedValue] = useState(value);

  useEffect(() => {
    const handler = setTimeout(() => {
      setDebouncedValue(value);
    }, delay);

    return () => {
      clearTimeout(handler); // ক্লিনআপ ফাংশন
    };
  }, [value, delay]);

  return debouncedValue;
};

export default useDebounce;
```

**ব্যবহার (Usage Example):**

```javascript
import { useState, useEffect } from "react";
import useDebounce from "./hooks/useDebounce";

const SearchBox = () => {
  const [searchTerm, setSearchTerm] = useState("");
  // ৫০০ms ডিলে সেট করা হলো
  const debouncedSearchTerm = useDebounce(searchTerm, 500);

  useEffect(() => {
    // এই ইফেক্টটি তখনই রান হবে যখন ইউজার টাইপ করা থামাবে ৫০০ms এর জন্য
    if (debouncedSearchTerm) {
      console.log("Searching API for:", debouncedSearchTerm);
      // API Call logic here...
    }
  }, [debouncedSearchTerm]);

  return (
    <input
      type="text"
      placeholder="Search..."
      value={searchTerm}
      onChange={(e) => setSearchTerm(e.target.value)}
    />
  );
};
```

---

## 🌐 Part 2: Context API

### ১. Context API কি এবং এর উদ্দেশ্য কি? (What & Purpose)

**কি:** Context API হলো React এর একটি ফিচার যা কম্পোনেন্ট ট্রি (Component Tree) এর সব লেভেলে ডাটা পাস করার সুযোগ দেয়, ম্যানুয়ালি প্রপস পাস করা ছাড়াই।

**উদ্দেশ্য:**

- **Prop Drilling বন্ধ করা:** প্যারেন্ট থেকে চাইল্ড, তারপর গ্র্যান্ড-চাইল্ড - এভাবে প্রপস পাস করার ঝামেলা দূর করা।
- **Global State Management:** অ্যাপ্লিকেশনের গ্লোবাল ডাটা (যেমন: ইউজার লগইন ইনফো, থিম, ভাষা) সব জায়গায় এক্সেসযোগ্য করা।

### ২. এটি কিভাবে কাজ করে? (How it works)

এটি মূলত ৩টি ধাপে কাজ করে:

1.  **Create Context:** একটি ডাটা স্টোর তৈরি করা।
2.  **Provider:** অ্যাপ্লিকেশনের বা নির্দিষ্ট অংশের প্যারেন্ট কম্পোনেন্টকে র‍্যাপ করে ডাটা সাপ্লাই দেওয়া।
3.  **Consumer (useContext):** যেকোনো চাইল্ড কম্পোনেন্ট থেকে সেই ডাটা ব্যবহার করা।

### ৩. সিনট্যাক্স (Syntax)

```javascript
import { createContext, useContext, useState } from "react";

// ১. Context তৈরি
const MyContext = createContext();

// ২. Provider তৈরি
const MyProvider = ({ children }) => {
  const [value, setValue] = useState("Hello World");
  return (
    <MyContext.Provider value={{ value, setValue }}>
      {children}
    </MyContext.Provider>
  );
};

// ৩. ব্যবহার (Custom Hook প্যাটার্ন ফলো করা বেস্ট প্র্যাকটিস)
const useMyContext = () => {
  return useContext(MyContext);
};
```

### ৪. ৩টি রিয়েল-ওয়ার্ল্ড ইউজ কেস (Real-world Use Cases)

#### Use Case 1: Theme Context (Dark/Light Mode)

পুরো অ্যাপে ডার্ক বা লাইট মোড ম্যানেজ করার জন্য।

```javascript
// context/ThemeContext.js
import { createContext, useContext, useState } from "react";

const ThemeContext = createContext();

export const ThemeProvider = ({ children }) => {
  const [theme, setTheme] = useState("light");

  const toggleTheme = () => {
    setTheme((prev) => (prev === "light" ? "dark" : "light"));
  };

  return (
    <ThemeContext.Provider value={{ theme, toggleTheme }}>
      <div className={theme === "dark" ? "dark-class" : "light-class"}>
        {children}
      </div>
    </ThemeContext.Provider>
  );
};

export const useTheme = () => useContext(ThemeContext);
```

**ব্যবহার (Usage Example):**

```javascript
// 1. Wrap App with Provider
// App.js
import { ThemeProvider } from "./context/ThemeContext";

const App = () => (
  <ThemeProvider>
    <Navbar />
    <MainContent />
  </ThemeProvider>
);

// 2. Use inside any component
// Navbar.js
import { useTheme } from "./context/ThemeContext";

const Navbar = () => {
  const { theme, toggleTheme } = useTheme();

  return (
    <nav>
      <h1>My App ({theme})</h1>
      <button onClick={toggleTheme}>
        Switch to {theme === "light" ? "Dark" : "Light"} Mode
      </button>
    </nav>
  );
};
```

#### Use Case 2: Auth Context (User Authentication)

ইউজার লগইন আছে কিনা, ইউজারের তথ্য এবং লগআউট ফাংশনালিটি গ্লোবালি ম্যানেজ করা।

```javascript
// context/AuthContext.js
import { createContext, useContext, useState, useEffect } from "react";

const AuthContext = createContext(null);

export const AuthProvider = ({ children }) => {
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    // চেক করা ইউজার আগে থেকেই লগইন আছে কিনা
    const storedUser = localStorage.getItem("user");
    if (storedUser) setUser(JSON.parse(storedUser));
    setLoading(false);
  }, []);

  const login = (userData) => {
    setUser(userData);
    localStorage.setItem("user", JSON.stringify(userData));
  };

  const logout = () => {
    setUser(null);
    localStorage.removeItem("user");
  };

  return (
    <AuthContext.Provider value={{ user, login, logout, loading }}>
      {!loading && children}
    </AuthContext.Provider>
  );
};

export const useAuth = () => useContext(AuthContext);
```

**ব্যবহার (Usage Example):**

```javascript
// LoginButton.js
import { useAuth } from "./context/AuthContext";

const LoginButton = () => {
  const { user, login, logout } = useAuth();

  if (user) {
    return (
      <div>
        <p>Welcome, {user.name}!</p>
        <button onClick={logout}>Logout</button>
      </div>
    );
  }

  return (
    <button onClick={() => login({ name: "Rahim", id: 1 })}>
      Login as Rahim
    </button>
  );
};
```

#### Use Case 3: Toast/Notification Context

অ্যাপের যেকোনো জায়গা থেকে পপ-আপ নোটিফিকেশন বা টোস্ট মেসেজ দেখানোর জন্য।

```javascript
// context/ToastContext.js
import { createContext, useContext, useState } from "react";

const ToastContext = createContext();

export const ToastProvider = ({ children }) => {
  const [toasts, setToasts] = useState([]);

  const addToast = (message, type = "info") => {
    const id = Date.now();
    setToasts((prev) => [...prev, { id, message, type }]);

    // ৩ সেকেন্ড পর অটোমেটিক রিমুভ
    setTimeout(() => {
      setToasts((prev) => prev.filter((t) => t.id !== id));
    }, 3000);
  };

  return (
    <ToastContext.Provider value={{ addToast }}>
      {children}
      <div
        className="toast-container"
        style={{ position: "fixed", bottom: 20, right: 20 }}
      >
        {toasts.map((toast) => (
          <div
            key={toast.id}
            className={`toast toast-${toast.type}`}
            style={{
              margin: "5px",
              padding: "10px",
              background: "#333",
              color: "#fff",
            }}
          >
            {toast.message}
          </div>
        ))}
      </div>
    </ToastContext.Provider>
  );
};

export const useToast = () => useContext(ToastContext);
```

**ব্যবহার (Usage Example):**

```javascript
// FormComponent.js
import { useToast } from "./context/ToastContext";

const FormComponent = () => {
  const { addToast } = useToast();

  const handleSave = () => {
    // ডাটা সেভ করার লজিক...
    // সফল হলে টোস্ট দেখানো
    addToast("Data Saved Successfully!", "success");
  };

  return <button onClick={handleSave}>Save Data</button>;
};
```

---

## 💡 প্রো টিপস (Pro Tips)

1.  **কখন Context ব্যবহার করবেন না:** যদি ডাটা শুধুমাত্র ১-২ লেভেল নিচে পাস করতে হয়, তবে Context ব্যবহার না করে Props ব্যবহার করাই ভালো। Context অতিরিক্ত ব্যবহার করলে অ্যাপের পারফর্মেন্স কমতে পারে (Unnecessary Re-renders)।
2.  **Custom Hook এর শক্তি:** যখনই দেখবেন একই কোড বা লজিক একাধিক কম্পোনেন্টে লিখছেন, তখনই সেটাকে Custom Hook এ কনভার্ট করে ফেলুন।
3.  **Context + Custom Hook:** Context এর ভ্যালু সরাসরি `useContext(MyContext)` দিয়ে এক্সেস না করে, সবসময় একটি Custom Hook (যেমন `useAuth`) বানিয়ে এক্সপোর্ট করুন। এতে ইমপোর্ট করা সহজ হয় এবং ভুল হওয়ার সম্ভাবনা কমে।
