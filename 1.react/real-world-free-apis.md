# Real-World Practice এর জন্য সেরা Free APIs

আপনি যদি JSONPlaceholder এর চেয়ে অ্যাডভান্সড এবং রিয়েল লাইফ প্রোজেক্টের মতো ফিচার (যেমন: Authentication, Pagination, Filtering) প্র্যাকটিস করতে চান, তবে নিচের API গুলো সেরা:

## 1. Platzi Fake Store API (Best for Auth & CRUD)

এটি রিয়েল ই-কমার্স অ্যাপের সব ফিচার প্র্যাকটিস করার জন্য চমৎকার।

- **Website:** [https://fakeapi.platzi.com/](https://fakeapi.platzi.com/)
- **Key Features:**
  - **JWT Authentication:** `access_token` এবং `refresh_token` নিয়ে কাজ করার সুযোগ আছে।
  - **Pagination:** `offset` এবং `limit` ব্যবহার করে পেজিনেশন করা যায়।
  - **Filtering:** প্রাইস রেঞ্জ, টাইটেল বা ক্যাটাগরি দিয়ে ফিল্টার করা যায়।
  - **File Upload:** ইমেজ আপলোড করার API ও আছে।
  - **CRUD:** Products, Users, Categories এর জন্য সম্পূর্ণ Create, Read, Update, Delete সাপোর্ট করে।

**Example Endpoint:**

```bash
GET https://api.escuelajs.co/api/v1/products?offset=0&limit=10
```

## 2. DummyJSON (Best Overall)

এটি অনেকটা JSONPlaceholder এর মতো কিন্তু অনেক বেশি ফিচার সমৃদ্ধ এবং ডাটাগুলো দেখতে রিয়েল মনে হয়।

- **Website:** [https://dummyjson.com/](https://dummyjson.com/)
- **Key Features:**
  - **Auth:** ইউজার লগইন এবং অথেন্টিকেটেড রাউট এক্সেস করার সুযোগ (Token based)।
  - **Search & Filter:** চমৎকার সার্চ এবং ফিল্টারিং অপশন।
  - **Pagination:** `limit` এবং `skip` দিয়ে পেজিনেশন।
  - **Resources:** Products, Carts, Users, Posts, Comments, Todos, Quotes ইত্যাদি।

**Example Endpoint:**

```bash
GET https://dummyjson.com/products/search?q=phone
```

## 3. The Movie DB (TMDB) (Best for Real Data)

যদি একদম রিয়েল প্রোডাকশন ডাটা নিয়ে কাজ করতে চান (যেমন Netflix ক্লোন), তবে এটি সেরা। তবে এর জন্য ফ্রি সাইন-আপ করে API Key নিতে হয়।

- **Website:** [https://developer.themoviedb.org/docs](https://developer.themoviedb.org/docs)
- **Key Features:**
  - **Complex Queries:** অনেক ধরনের প্যারামিটার এবং কুয়েরি।
  - **Images:** হাই কোয়ালিটি ইমেজ হ্যান্ডলিং।
  - **Auth:** Session based authentication প্র্যাকটিস করা যায়।

## 4. ReqRes (Best for Testing Status Codes)

এটি মূলত ফ্রন্টএন্ডে লোডিং স্টেট, এরর হ্যান্ডলিং (404, 401, 403) টেস্ট করার জন্য ভালো।

- **Website:** [https://reqres.in/](https://reqres.in/)
- **Key Features:**
  - **Simulated Delay:** `?delay=3` দিয়ে স্লো নেটওয়ার্ক সিমুলেট করা যায়।
  - **Auth:** সিম্পল লগইন/রেজিস্ট্রেশন ফ্লো।

---

### আমার রিকমেন্ডেশন:

**Platzi Fake Store API** অথবা **DummyJSON** দিয়ে শুরু করুন। এই দুটি দিয়ে আপনি একটি পূর্ণাঙ্গ ই-কমার্স সাইট বানাতে পারবেন যেখানে লগইন, প্রোডাক্ট ফিল্টারিং এবং পেজিনেশন থাকবে।
