# Next.js 14/15 App Router Mastery Guide (Bangla)

এই গাইডটি আপনাকে Next.js 14/15 এর App Router ব্যবহার করে একজন দক্ষ ফ্রন্টএন্ড ডেভেলপার হিসেবে গড়ে তোলার জন্য তৈরি করা হয়েছে। এখানে শুধুমাত্র **App Router** এবং আধুনিক প্যাটার্ন নিয়ে আলোচনা করা হয়েছে যা বর্তমানে ইউরোপ এবং আমেরিকার রিমোট জবের জন্য স্ট্যান্ডার্ড।

---

## 1. What & Why Next.js

### Next.js কি এবং এটি কেন প্রয়োজন?

Next.js হলো React এর একটি ফ্রেমওয়ার্ক যা প্রোডাকশন-গ্রেড অ্যাপ্লিকেশন তৈরির জন্য প্রয়োজনীয় সব ফিচার বিল্ট-ইন প্রদান করে। React শুধুমাত্র UI লাইব্রেরি, কিন্তু Next.js রাউটিং, ডেটা ফেচিং, এবং পারফরম্যান্স অপ্টিমাইজেশন সহজ করে দেয়।

### Next.js vs React

- **React:** যখন আপনি নিজের মতো করে সবকিছু সেটআপ করতে চান এবং শুধুমাত্র ক্লায়েন্ট-সাইড রেন্ডারিং (CSR) প্রয়োজন।
- **Next.js:** যখন আপনার SEO, ফাস্ট ইনিশিয়াল লোড, এবং ফুল-স্ট্যাক ফিচার (API routes, Server Actions) প্রয়োজন।

### কোম্পানিরা কেন Next.js ব্যবহার করে?

1.  **SEO (Search Engine Optimization):** সার্ভার সাইড রেন্ডারিং (SSR) এর কারণে গুগল সহজেই পেজ ইনডেক্স করতে পারে।
2.  **Performance:** অটোমেটিক কোড স্প্লিটিং এবং ইমেজ অপ্টিমাইজেশন।
3.  **Developer Experience (DX):** ফাইল-সিস্টেম বেসড রাউটিং এবং টাইপস্ক্রিপ্ট সাপোর্ট।

### App Router vs Pages Router

- **Pages Router (Old):** `pages` ডিরেক্টরি ব্যবহার করত, যা এখন লিগ্যাসি।
- **App Router (New):** `app` ডিরেক্টরি ব্যবহার করে। এটি React Server Components (RSC) এর উপর ভিত্তি করে তৈরি, যা অনেক বেশি শক্তিশালী এবং ফ্লেক্সিবল।

### Server Components vs Client Components (Game Changer!)

- **Server Components:** সার্ভারে রেন্ডার হয়, ক্লায়েন্টে কোনো JS পাঠায় না। ডেটা ফেচিংয়ের জন্য সেরা।
- **Client Components:** ব্রাউজারে ইন্টারেক্টিভিটির (state, effects) জন্য ব্যবহৃত হয়।

### Key Benefits

- **SSR (Server-Side Rendering):** রিকোয়েস্টের সময় সার্ভারে HTML জেনারেট হয়।
- **SSG (Static Site Generation):** বিল্ড টাইমে HTML জেনারেট হয় (ডিফল্ট)।
- **ISR (Incremental Static Regeneration):** বিল্ডের পরেও নির্দিষ্ট সময় পর পর পেজ আপডেট করা যায়।

---

## 2. Core Concepts (Foundation)

### App Router Architecture

App Router `app` ফোল্ডারের ভেতর কাজ করে। এখানে প্রতিটি ফোল্ডার একটি রাউট বা সেগমেন্ট রিপ্রেজেন্ট করে।

### Server Components (Default)

Next.js এর App Router এ সব কম্পোনেন্ট ডিফল্টভাবে **Server Components**। এর মানে আপনি সরাসরি ডেটাবেস কল করতে পারেন কম্পোনেন্টের ভেতর।

### Layouts & Nested Layouts

`layout.tsx` ফাইলটি ওই রাউট এবং তার চাইল্ড রাউটগুলোর জন্য কমন UI (যেমন নেভিগেশন বার) শেয়ার করে। নেস্টেড লেআউট দিয়ে আপনি কমপ্লেক্স UI তৈরি করতে পারেন।

### Streaming & Suspense

সার্ভার থেকে ডেটা আসার সময় পুরো পেজ আটকে না রেখে, `loading.tsx` বা `<Suspense>` দিয়ে লোডিং স্টেট দেখানো যায় এবং ডেটা আসলে তা স্ট্রিম করে দেখানো হয়।

---

## 3. Modern Next.js Setup (2024-2025)

### Installation

টার্মিনালে নিচের কমান্ডটি রান করুন:

```bash
npx create-next-app@latest my-app
```

সেটআপের সময় নিচের অপশনগুলো সিলেক্ট করুন:

- TypeScript: **Yes**
- ESLint: **Yes**
- Tailwind CSS: **Yes**
- `src/` directory: **No** (অথবা আপনার পছন্দমত, তবে `app` ফোল্ডার রুটে রাখা সহজ)
- App Router: **Yes** (অবশ্যই!)
- Customize default import alias (@/\*): **Yes**

### Recommended Folder Structure

```
/app
  /(routes)          # Route groups (URL এ প্রভাব ফেলে না)
    /(auth)
      /login
        page.tsx
      /register
        page.tsx
    /(dashboard)
      /dashboard
        page.tsx
        layout.tsx
      /settings
        page.tsx
  /api               # API routes (যদি লাগে)
    /users
      route.ts
  layout.tsx         # Root layout (Required)
  page.tsx           # Home page
  loading.tsx        # Global loading
  error.tsx          # Global error
  not-found.tsx      # 404 page
/components
  /ui                # Reusable UI (Button, Input)
  /forms             # Form related components
  /layout            # Header, Footer, Sidebar
/lib                 # Utilities
  /actions           # Server Actions (Mutations)
  /utils             # Helper functions
  /db                # Database client (Prisma/Drizzle)
/hooks               # Custom Hooks
/types               # TypeScript interfaces
/public              # Images, fonts
```

---

## 4. App Router File Conventions

Next.js এ ফাইলের নামগুলোর বিশেষ অর্থ আছে:

- **`page.tsx`**: এটিই মূল পেজ যা ব্রাউজারে রেন্ডার হয়।
- **`layout.tsx`**: পেজগুলোর র‍্যাপার (Wrapper)। কমন UI এখানে থাকে।
- **`loading.tsx`**: পেজ লোড হওয়ার সময় অটোমেটিক লোডিং স্কেলেটন দেখায় (Suspense এর মাধ্যমে)।
- **`error.tsx`**: রানটাইম এরর হ্যান্ডেল করার জন্য এরর বাউন্ডারি।
- **`not-found.tsx`**: যদি কোনো রাউট না পাওয়া যায়, এই পেজ দেখাবে।
- **`route.ts`**: API এন্ডপয়েন্ট তৈরি করার জন্য।
- **`template.tsx`**: লেআউটের মতোই, কিন্তু প্রতি নেভিগেশনে নতুন করে মাউন্ট হয় (state রিসেট হয়)।

---

## 5. Routing System (File-Based)

### Basic Routes

ফোল্ডার স্ট্রাকচার অনুযায়ী URL তৈরি হয়।

- `/app/about/page.tsx` -> `example.com/about`

### Nested Routes

- `/app/blog/tech/page.tsx` -> `example.com/blog/tech`

### Dynamic Routes (`[folderName]`)

যখন URL এর কোনো অংশ ডাইনামিক হয় (যেমন ID)।

- `/app/products/[id]/page.tsx` -> `example.com/products/123`

```tsx
// app/products/[id]/page.tsx
export default async function ProductPage({
  params,
}: {
  params: Promise<{ id: string }>;
}) {
  const { id } = await params; // Next.js 15 এ params async হয়
  return <h1>Product ID: {id}</h1>;
}
```

### Catch-all Routes (`[...slug]`)

একাধিক সেগমেন্ট ধরার জন্য।

- `/app/docs/[...slug]/page.tsx` -> `example.com/docs/a/b/c`

### Route Groups (`(folderName)`)

ফোল্ডারকে গ্রুপিং করার জন্য, কিন্তু URL এ এর নাম আসবে না।

- `/app/(auth)/login/page.tsx` -> `example.com/login`

### Parallel Routes (`@folder`)

একই লেআউটে একাধিক পেজ বা স্লট রেন্ডার করার জন্য।

- `/app/dashboard/@analytics/page.tsx`
- `/app/dashboard/@team/page.tsx`

`layout.tsx` এ এগুলো props হিসেবে পাওয়া যায়:

```tsx
export default function Layout({ children, analytics, team }: any) {
  return (
    <>
      {children}
      {analytics}
      {team}
    </>
  );
}
```

### Intercepting Routes (`(.)folder`)

বর্তমান পেজে থেকে অন্য রাউট লোড করা (যেমন মডাল)।

- `/app/feed/(.)photo/[id]/page.tsx` -> ফিড পেজের উপর ফটো মডাল ওপেন হবে।

---

## 6. Server Components vs Client Components (CRITICAL)

### Server Components (Default)

এগুলো সার্ভারে রেন্ডার হয়।
**কখন ব্যবহার করবেন?**

- ডেটা ফেচ করার জন্য।
- সেনসিটিভ লজিক (API Keys) রাখার জন্য।
- ক্লায়েন্ট বান্ডল সাইজ কমানোর জন্য।

**সীমাবদ্ধতা:**

- `useState`, `useEffect`, `onClick` ব্যবহার করা যাবে না।

### Client Components

এগুলো ব্রাউজারে হাইড্রেট হয়। ফাইলের একদম শুরুতে `"use client"` লিখতে হয়।
**কখন ব্যবহার করবেন?**

- ইন্টারেক্টিভিটি (Button click, Form input) এর জন্য।
- `useState`, `useEffect` বা ব্রাউজার API (localStorage) ব্যবহারের জন্য।

**Example:**

```tsx
// app/components/Counter.tsx
"use client"; // Must be at the top

import { useState } from "react";

export default function Counter() {
  const [count, setCount] = useState(0);
  return <button onClick={() => setCount(count + 1)}>Count: {count}</button>;
}
```

**✅ Best Practice:**
যতটা সম্ভব Server Component ব্যবহার করুন। শুধুমাত্র ইন্টারেক্টিভ অংশটুকু (যেমন বাটন, ফর্ম) আলাদা ফাইলে নিয়ে `"use client"` করে Server Component এর ভেতর ইম্পোর্ট করুন।

---

## 7. Layouts (Shared UI)

### Root Layout (`app/layout.tsx`)

এটি পুরো অ্যাপ্লিকেশনের মেইন র‍্যাপার। এখানে `<html>` এবং `<body>` ট্যাগ থাকে।

```tsx
import type { Metadata } from "next";
import { Inter } from "next/font/google";
import "./globals.css";

const inter = Inter({ subsets: ["latin"] });

export const metadata: Metadata = {
  title: "My Next.js App",
  description: "Generated by create next app",
};

export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <html lang="en">
      <body className={inter.className}>
        <nav>Navbar goes here</nav>
        {children}
      </body>
    </html>
  );
}
```

---

## 8. Data Fetching (Modern Approach)

### Server Components Data Fetching

Next.js এ ডেটা ফেচিং খুব সহজ। সরাসরি `async/await` ব্যবহার করুন। `useEffect` এর দরকার নেই!

```tsx
// app/users/page.tsx
async function getUsers() {
  const res = await fetch("https://jsonplaceholder.typicode.com/users");
  if (!res.ok) throw new Error("Failed to fetch data");
  return res.json();
}

export default async function UsersPage() {
  const users = await getUsers();

  return (
    <ul>
      {users.map((user: any) => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  );
}
```

### Client Components Data Fetching

যদি ক্লায়েন্ট সাইডে ডেটা ফেচ করতে হয় (যেমন ইউজার ইন্টারঅ্যাকশনের পর), তবে **TanStack Query** ব্যবহার করা রেকমেন্ডেড। অথবা সাধারণ `useEffect` দিয়েও করা যায়।

---

## 9. Server Actions (Game Changer!)

API Route তৈরি না করেই সার্ভারে ফাংশন কল করার উপায় হলো Server Actions। ফর্ম সাবমিশনের জন্য এটি সেরা।

**Example:**

```tsx
// lib/actions/todo-actions.ts
"use server"; // Mark as server action

import { revalidatePath } from "next/cache";

export async function createTodo(formData: FormData) {
  const title = formData.get("title");

  // Database logic here...
  console.log("Creating todo:", title);

  // Cache আপডেট করার জন্য
  revalidatePath("/todos");
}
```

**Usage in Component:**

```tsx
// app/todos/page.tsx
import { createTodo } from "@/lib/actions/todo-actions";

export default function TodoPage() {
  return (
    <form action={createTodo}>
      <input name="title" type="text" required />
      <button type="submit">Add Todo</button>
    </form>
  );
}
```

---

## 10. Loading & Error Handling

### Loading UI

`loading.tsx` ফাইল তৈরি করলে Next.js অটোমেটিক্যালি লোডিং স্টেট দেখাবে।

```tsx
// app/dashboard/loading.tsx
export default function Loading() {
  return <div>Loading dashboard skeleton...</div>;
}
```

### Error Handling

`error.tsx` ফাইল রানটাইম এরর হ্যান্ডেল করে। এটি অবশ্যই Client Component হতে হবে।

```tsx
// app/dashboard/error.tsx
"use client";

export default function Error({
  error,
  reset,
}: {
  error: Error;
  reset: () => void;
}) {
  return (
    <div>
      <h2>Something went wrong!</h2>
      <button onClick={() => reset()}>Try again</button>
    </div>
  );
}
```

---

## 11. Caching & Revalidation

Next.js ডিফল্টভাবে ডেটা ক্যাশ করে রাখে।

### Revalidation

যদি আপনি চান ডেটা নির্দিষ্ট সময় পর পর আপডেট হোক:

```tsx
// Time-based revalidation (ISR)
fetch("https://api.example.com/data", { next: { revalidate: 3600 } }); // 1 hour

// On-demand Revalidation (Tag-based)
fetch("https://api.example.com/data", { next: { tags: ["collection"] } });
// পরে Server Action এ: revalidateTag("collection");
```

### Opt-out of Caching

যদি রিয়েল-টাইম ডেটা লাগে:

```tsx
fetch("https://api.example.com/data", { cache: "no-store" });
```

---

## 12. Rendering Strategies

- **Static Rendering (Default):** বিল্ড টাইমে পেজ জেনারেট হয়। ফাস্টেস্ট পারফরম্যান্স।
- **Dynamic Rendering:** যদি কুকিজ, হেডার্স বা `searchParams` ব্যবহার করেন, অথবা `no-store` ফেচ ব্যবহার করেন, তবে পেজটি ডাইনামিক হয়ে যাবে (প্রতি রিকোয়েস্টে সার্ভারে রেন্ডার হবে)।

---

## 13. Metadata & SEO

প্রতিটি পেজে মেটাডেটা এক্সপোর্ট করে SEO ইম্প্রুভ করা যায়।

```tsx
// app/page.tsx
import type { Metadata } from "next";

export const metadata: Metadata = {
  title: "Home - My App",
  description: "Welcome to my awesome Next.js app",
};
```

**Dynamic Metadata:**

```tsx
export async function generateMetadata({ params }: any): Promise<Metadata> {
  const product = await getProduct(params.id);
  return {
    title: product.title,
  };
}
```

---

## 14. Navigation

- **`<Link>` Component:** পেজ নেভিগেশনের জন্য। এটি ক্লায়েন্ট-সাইড নেভিগেশন করে (রিফ্রেশ ছাড়া)।
- **`useRouter` Hook:** প্রোগ্রাম্যাটিক নেভিগেশনের জন্য (যেমন ফর্ম সাবমিটের পর রিডাইরেক্ট)।
- **`usePathname`:** বর্তমান URL পাথ পাওয়ার জন্য।

```tsx
"use client";
import { useRouter } from "next/navigation";

export default function LoginButton() {
  const router = useRouter();
  return <button onClick={() => router.push("/dashboard")}>Login</button>;
}
```

---

## 15. Forms & Mutations

Server Actions এর সাথে `useFormStatus` হুক ব্যবহার করে পেন্ডিং স্টেট দেখানো যায়।

```tsx
// app/components/SubmitButton.tsx
"use client";
import { useFormStatus } from "react-dom";

export function SubmitButton() {
  const { pending } = useFormStatus();
  return (
    <button type="submit" disabled={pending}>
      {pending ? "Saving..." : "Save"}
    </button>
  );
}
```

---

## 16. API Integration Patterns

API কল কোথায় করবেন?

1. **Server Components:** সরাসরি `fetch` বা DB কল করুন। (Best for GET)
2. **Server Actions:** ডেটা মিউটেশনের জন্য (POST, PUT, DELETE)।
3. **Route Handlers (`route.ts`):** যদি আপনার অ্যাপের ডেটা থার্ড-পার্টিকে দিতে হয় (REST API)।

---

## 17. Authentication Patterns (Auth.js / NextAuth v5)

NextAuth v5 এখন সার্ভার কম্পোনেন্ট ফ্রেন্ডলি।

```tsx
// auth.ts
import NextAuth from "next-auth";
import GitHub from "next-auth/providers/github";

export const { handlers, auth, signIn, signOut } = NextAuth({
  providers: [GitHub],
});

// app/api/auth/[...nextauth]/route.ts
export const { GET, POST } = handlers;
```

---

## 18. Middleware

`middleware.ts` ফাইলটি রিকোয়েস্ট প্রসেস হওয়ার আগেই রান করে। এটি অথেন্টিকেশন চেক বা রিডাইরেক্টের জন্য ব্যবহার করা হয়।

```tsx
// middleware.ts
import { NextResponse } from "next/server";
import type { NextRequest } from "next/server";

export function middleware(request: NextRequest) {
  const token = request.cookies.get("token");
  if (!token) {
    return NextResponse.redirect(new URL("/login", request.url));
  }
}

export const config = {
  matcher: "/dashboard/:path*",
};
```

---

## 19. Image Optimization

`next/image` কম্পোনেন্ট অটোমেটিক্যালি ইমেজ রিসাইজ, ফরম্যাট চেঞ্জ (WebP/AVIF) এবং লেজি লোড করে।

```tsx
import Image from "next/image";
import heroPic from "../public/hero.jpg";

<Image src={heroPic} alt="Hero" placeholder="blur" />;
```

---

## 20. Professional Code Organization

প্রফেশনাল প্রজেক্টে কোড অর্গানাইজেশন খুব গুরুত্বপূর্ণ।

- **Colocation:** কম্পোনেন্টগুলো যেখানে ব্যবহার হচ্ছে তার কাছেই রাখুন।
- **Private Folders (`_components`):** রাউটের ভেতর প্রাইভেট ফোল্ডার তৈরি করতে `_` ব্যবহার করুন।
- **Separation of Concerns:** UI কম্পোনেন্ট, বিজনেস লজিক (Actions), এবং ডেটাবেস কোড আলাদা রাখুন।

---

## 21. Modern Next.js Patterns (2024-2025)

- **✅ DO:** Server Components ডিফল্ট হিসেবে ব্যবহার করুন।
- **✅ DO:** মিউটেশনের জন্য Server Actions ব্যবহার করুন।
- **✅ DO:** লোডিং স্টেটের জন্য Suspense ব্যবহার করুন।
- **❌ DON'T:** সব কম্পোনেন্টে `"use client"` ব্যবহার করবেন না।
- **❌ DON'T:** ডেটা ফেচিংয়ের জন্য ক্লায়েন্টে `useEffect` ব্যবহার করবেন না (যদি না খুব প্রয়োজন হয়)।

---

## 22. TypeScript with Next.js

Next.js এবং TypeScript একসাথে চমৎকার কাজ করে।

```tsx
// Typing Page Props (Next.js 15)
type Props = {
  params: Promise<{ id: string }>;
  searchParams: Promise<{ [key: string]: string | string[] | undefined }>;
};

export default async function Page({ params, searchParams }: Props) {
  const { id } = await params;
  return <h1>ID: {id}</h1>;
}
```

---

## 23. Performance Optimization

- **Dynamic Imports:** বড় কম্পোনেন্টগুলো লেজি লোড করুন।
  ```tsx
  const HeavyComponent = dynamic(() => import("./HeavyComponent"));
  ```
- **Font Optimization:** `next/font` ব্যবহার করুন যা লেআউট শিফট কমায়।
- **Script Optimization:** `next/script` দিয়ে থার্ড-পার্টি স্ক্রিপ্ট লোড কন্ট্রোল করুন।

---

## 24. Environment Variables

এনভায়রনমেন্ট ভেরিয়েবল `.env.local` ফাইলে রাখুন।

- সার্ভার সাইড: `API_KEY=xyz` (সিক্রেট)
- ক্লায়েন্ট সাইড: `NEXT_PUBLIC_ANALYTICS_ID=123` (পাবলিক)

---

## 25. Deployment (Vercel)

Next.js এর মাদার কোম্পানি Vercel এ ডিপ্লয় করা সবচেয়ে সহজ।

1. GitHub এ কোড পুশ করুন।
2. Vercel এ প্রজেক্ট ইম্পোর্ট করুন।
3. এনভায়রনমেন্ট ভেরিয়েবল সেট করুন।
4. Deploy!

---

## 26. Integration with Modern Tools

- **Prisma/Drizzle:** টাইপ-সেফ ডেটাবেস কুয়েরির জন্য।
- **Zod:** স্কিমা ভ্যালিডেশনের জন্য (বিশেষ করে ফর্ম ডেটা)।
- **React Hook Form:** ক্লায়েন্ট সাইড ফর্ম হ্যান্ডলিংয়ের জন্য।
- **Shadcn UI:** মডার্ন এবং এক্সেসিবল UI কম্পোনেন্টের জন্য।

---

## 27. Real-World Example: Blog App Structure

একটি কমপ্লিট ব্লগ অ্যাপের স্ট্রাকচার কেমন হতে পারে:

```
/app
  /page.tsx (Home - List of posts)
  /blog
    /[slug]
      /page.tsx (Single post - SSG)
  /admin
    /posts
      /create
        /page.tsx (Form with Server Action)
      /[id]/edit
        /page.tsx
  /api/auth/[...nextauth]/route.ts
/lib
  /actions.ts (createPost, updatePost, deletePost)
  /db.ts (Prisma client)
```

---

## 28. Common Mistakes & Gotchas

- **ভুল:** Server Component এ `onClick` ইভেন্ট ব্যবহার করা।
  - **সমাধান:** ইন্টারেক্টিভ পার্টটুকু আলাদা Client Component এ নিয়ে যান।
- **ভুল:** `useEffect` দিয়ে ইনিশিয়াল ডেটা লোড করা।
  - **সমাধান:** সরাসরি Server Component এ `await fetch()` করুন।
- **ভুল:** সিক্রেট কী `NEXT_PUBLIC_` দিয়ে এক্সপোজ করা।
  - **সমাধান:** শুধুমাত্র পাবলিক কী গুলোর আগে `NEXT_PUBLIC_` দিন।

---

## 29. Interview-Ready Knowledge

**Q: Server Components এবং Client Components এর পার্থক্য কি?**
A: Server Components সার্ভারে রেন্ডার হয়, ক্লায়েন্টে কোনো JS পাঠায় না, এবং সরাসরি ব্যাকএন্ড রিসোর্স এক্সেস করতে পারে। Client Components ব্রাউজারে রান করে এবং ইন্টারেক্টিভিটির জন্য ব্যবহৃত হয়।

**Q: Next.js এ Caching কিভাবে কাজ করে?**
A: Next.js এ ৪ লেভেলের ক্যাশিং আছে: Request Memoization, Data Cache, Full Route Cache, এবং Router Cache।

---

## 30. Debugging Next.js Apps

- **Server Logs:** টার্মিনালে `console.log` আউটপুট দেখুন (Server Components এর জন্য)।
- **Browser Console:** Client Components এর লগ এবং এরর দেখুন।
- **Network Tab:** API কল এবং Server Actions এর নেটওয়ার্ক রিকোয়েস্ট চেক করুন।

---

## 31. Next Steps

বেসিক শেখার পর যা শিখবেন:

1. **Database:** PostgreSQL এর সাথে Prisma বা Drizzle ORM।
2. **Advanced Auth:** Role-based access control (RBAC)।
3. **State Management:** Zustand (যদি খুব কমপ্লেক্স স্টেট লাগে)।
4. **Testing:** Playwright বা Jest দিয়ে E2E টেস্টিং।

এই গাইডটি ফলো করে প্র্যাকটিস শুরু করুন, এবং ছোট ছোট প্রজেক্ট তৈরি করুন। শুভকামনা! 🚀
