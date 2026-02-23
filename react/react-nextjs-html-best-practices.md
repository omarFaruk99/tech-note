# React & Next.js HTML Best Practices Guide (Bangla)

React এবং Next.js ডেভেলপারদের জন্য HTML, Accessibility (A11y), এবং SEO এর একটি কমপ্লিট গাইড। আমরা অনেকেই React বা Next.js এ কাজ করার সময় শুধু `div` ব্যবহার করি, যা একদম ভুল। এই গাইডে আমরা দেখব কিভাবে প্রফেশনাল এবং জব-রেডি কোড লিখতে হয়।

---

## 1. Semantic HTML (Div এর বদলে সঠিক ট্যাগ)

Semantic HTML মানে হলো এমন ট্যাগ ব্যবহার করা যা ব্রাউজার এবং ডেভেলপার উভয়কেই বলে দেয় যে কন্টেন্টটি আসলে কী।

### কেন ব্যবহার করবেন?

- **SEO**: সার্চ ইঞ্জিন আপনার পেজের স্ট্রাকচার বুঝতে পারে।
- **Accessibility**: স্ক্রিন রিডার ব্যবহারকারীরা সহজে নেভিগেট করতে পারে।
- **Code Readability**: কোড পড়ে বোঝা সহজ হয়।

### Common Semantic Tags

| Tag         | ব্যবহার                                             | ভুল ব্যবহার (Bad)           |
| ----------- | --------------------------------------------------- | --------------------------- |
| `<header>`  | পেজ বা সেকশনের হেডার (Logo, Nav)                    | `<div className="header">`  |
| `<nav>`     | মেইন নেভিগেশন মেনু                                  | `<div className="nav">`     |
| `<main>`    | পেজের প্রধান কন্টেন্ট (একবারই ব্যবহার হবে)          | `<div className="content">` |
| `<section>` | কন্টেন্টের একটি নির্দিষ্ট গ্রুপ (Heading থাকা উচিত) | `<div>`                     |
| `<article>` | স্বতন্ত্র কন্টেন্ট (Blog post, Card)                | `<div>`                     |
| `<aside>`   | সাইডবার বা অতিরিক্ত তথ্য                            | `<div className="sidebar">` |
| `<footer>`  | পেজ বা সেকশনের ফুটার                                | `<div className="footer">`  |

### ✅ Example (React/Next.js Component)

```tsx
// Bad ❌
export default function BlogPage() {
  return (
    <div className="blog">
      <div className="top-bar">My Blog</div>
      <div className="content">
        <div className="post">
          <div className="title">Post 1</div>
          <div>Content...</div>
        </div>
      </div>
    </div>
  );
}

// Good ✅
export default function BlogPage() {
  return (
    <>
      <header>
        <h1>My Blog</h1>
        <nav>
          <a href="/">Home</a>
        </nav>
      </header>

      <main>
        <article>
          <h2>Post 1</h2>
          <p>Content...</p>
        </article>
      </main>

      <footer>
        <p>&copy; 2024 My Blog</p>
      </footer>
    </>
  );
}
```

---

## 2. Accessibility (A11y) - CRITICAL

ইউরোপ এবং আমেরিকার জবের জন্য Accessibility জানা বাধ্যতামূলক।

### ১. ফর্ম লেবেল (Labels)

সব ইনপুটের সাথে লেবেল থাকতে হবে। `placeholder` লেবেল নয়!

```tsx
// Bad ❌
<input type="text" placeholder="Enter Name" />

// Good ✅
<label htmlFor="name">Name</label>
<input id="name" type="text" />

// Good (Hidden Label) ✅
<label htmlFor="search" className="sr-only">Search</label>
<input id="search" type="search" placeholder="Search..." />
```

_Note: `sr-only` ক্লাসটি এলিমেন্টকে ভিজুয়ালি হাইড করে কিন্তু স্ক্রিন রিডারের জন্য রাখে।_

### ২. ছবির Alt Text

ছবি লোড না হলে বা অন্ধ ব্যবহারকারীদের জন্য এটি জরুরি।

```tsx
// Bad ❌
<img src="logo.png" />
<img src="icon.png" alt="image" />

// Good ✅
<img src="logo.png" alt="Company Name Logo" />
// ডেকোরেটিভ ইমেজের জন্য (খালি alt)
<img src="bg-pattern.png" alt="" aria-hidden="true" />
```

### ৩. কীবোর্ড নেভিগেশন

মাউস ছাড়াও যেন ট্যাব (Tab) কী দিয়ে সব ব্যবহার করা যায়।

- `div` বা `span` এ `onClick` ব্যবহার করবেন না। বাটন বা লিংকের জন্য `<button>` বা `<a>` ব্যবহার করুন।

```tsx
// Bad ❌
<div onClick={submitForm}>Submit</div>

// Good ✅
<button onClick={submitForm}>Submit</button>
```

---

## 3. Forms (Accessible & User-Friendly)

### React Client Component Example (React Hook Form)

```tsx
"use client";
import { useForm } from "react-hook-form";

export default function ContactForm() {
  const {
    register,
    handleSubmit,
    formState: { errors },
  } = useForm();

  const onSubmit = (data) => console.log(data);

  return (
    <form onSubmit={handleSubmit(onSubmit)} noValidate>
      <div>
        <label htmlFor="email">Email</label>
        <input
          id="email"
          type="email"
          aria-invalid={errors.email ? "true" : "false"}
          aria-describedby={errors.email ? "email-error" : undefined}
          {...register("email", { required: "Email is required" })}
        />
        {errors.email && (
          <p id="email-error" role="alert" style={{ color: "red" }}>
            {errors.email.message?.toString()}
          </p>
        )}
      </div>
      <button type="submit">Send</button>
    </form>
  );
}
```

### Next.js Server Action Example

```tsx
// app/actions.ts
"use server";
export async function signup(formData: FormData) {
  // Server validation logic...
}

// app/page.tsx
import { signup } from "./actions";

export default function SignupPage() {
  return (
    <form action={signup}>
      <div>
        <label htmlFor="username">Username</label>
        <input id="username" name="username" type="text" required />
      </div>
      <button type="submit">Sign Up</button>
    </form>
  );
}
```

---

## 4. SEO Best Practices

### Heading Hierarchy

একটি পেজে **মাত্র একটি** `<h1>` থাকবে। এরপর ক্রমানুসারে `<h2>`, `<h3>` আসবে। লেভেল স্কিপ করবেন না (যেমন `<h2>` এর পর `<h4>` দেবেন না)।

### Meta Tags

#### React (Vite/CRA)

`react-helmet-async` ব্যবহার করুন অথবা `index.html` এ স্ট্যাটিক ট্যাগ দিন।

#### Next.js App Router (Metadata API)

```tsx
// app/layout.tsx or app/page.tsx
import type { Metadata } from "next";

export const metadata: Metadata = {
  title: "My Awesome App",
  description: "Best app for learning React",
  openGraph: {
    title: "My Awesome App",
    description: "Best app for learning React",
  },
};

export default function Page() {
  return <h1>Home Page</h1>;
}
```

---

## 5. Common Mistakes in React/Next.js JSX

| ভুল (Wrong) ❌                   | সঠিক (Right) ✅              | কারণ                                   |
| -------------------------------- | ---------------------------- | -------------------------------------- |
| `<div onClick={...}>`            | `<button onClick={...}>`     | Accessibility & Keyboard Support       |
| `placeholder="Email"` (no label) | `<label>Email</label>`       | Screen Readers need labels             |
| `<b>Bold Text</b>`               | `<strong>Bold Text</strong>` | Semantic meaning (Strong importance)   |
| `<i>Italic</i>`                  | `<em>Italic</em>`            | Semantic meaning (Emphasis)            |
| `<h1>Title</h1>` multiple times  | One `<h1>`, then `<h2>`      | SEO Hierarchy                          |
| `<a href="#">` for buttons       | `<button>`                   | Links go somewhere, Buttons do actions |

---

## 6. JSX-Specific Reminders

React/Next.js এ HTML লেখার সময় কিছু সিনট্যাক্স পার্থক্য মনে রাখতে হবে:

1.  **Class vs ClassName**:
    ```tsx
    // Wrong: <div class="box">
    // Right: <div className="box">
    ```
2.  **For vs HtmlFor**:
    ```tsx
    // Wrong: <label for="id">
    // Right: <label htmlFor="id">
    ```
3.  **CamelCase Events**:
    `onclick` -> `onClick`, `onchange` -> `onChange`
4.  **Self-Closing Tags**:
    `<img>`, `<input>`, `<br>` অবশ্যই ক্লোজ করতে হবে।
    ```tsx
    <input type="text" /> // Right
    ```
5.  **Boolean Attributes**:
    ```tsx
    <input disabled={true} /> অথবা শুধু <input disabled />
    ```

---

## 7. Real Examples for Both Frameworks

### Accessible Card Component

```tsx
export default function Card({ title, description, link }) {
  return (
    <article className="card">
      <h3>{title}</h3>
      <p>{description}</p>
      {/* Link এর ভিতরে টেক্সট যেন অর্থপূর্ণ হয়, "Click Here" নয় */}
      <a href={link} aria-label={`Read more about ${title}`}>
        Read More
      </a>
    </article>
  );
}
```

### Accessible Modal/Dialog

মডাল ওপেন হলে ফোকাস মডালের ভেতরে থাকা উচিত এবং `Esc` চাপলে বন্ধ হওয়া উচিত।

```tsx
// Simple concept
<dialog open>
  <form method="dialog">
    <h2>Confirmation</h2>
    <p>Are you sure?</p>
    <button value="cancel">Cancel</button>
    <button value="confirm">Confirm</button>
  </form>
</dialog>
```

---

## 8. Next.js App Router Specifics

### Server Components

Server Component এও Semantic HTML ব্যবহার করতে হবে। এটি ব্রাউজারে HTML হিসেবেই রেন্ডার হয়, তাই SEO এর জন্য এটি খুব ভালো।

### Image Component (`next/image`)

Next.js এ `<img>` এর বদলে `<Image />` ব্যবহার করা ভালো, তবে `alt` প্রপ বাধ্যতামূলক।

```tsx
import Image from "next/image";

<Image
  src="/hero.jpg"
  alt="A description of the hero image"
  width={500}
  height={300}
/>;
```

---

## 9. Quick Accessibility Checklist (Universal)

কাজ শেষ করার আগে এই চেকলিস্টটি মিলিয়ে নিন:

- [ ] **Images**: সব ছবির `alt` টেক্সট আছে কি? (ডেকোরেটিভ হলে `alt=""`)
- [ ] **Forms**: সব ইনপুটের সাথে `<label>` আছে কি?
- [ ] **Buttons**: ক্লিকের কাজের জন্য `<div>` এর বদলে `<button>` ব্যবহার করেছেন?
- [ ] **Headings**: `<h1>` থেকে `<h6>` এর অর্ডার ঠিক আছে? (১টা `<h1>` প্রতি পেজে)
- [ ] **Contrast**: টেক্সট এবং ব্যাকগ্রাউন্ড কালারের কন্ট্রাস্ট কি পড়ার যোগ্য?
- [ ] **Keyboard**: মাউস ছাড়া শুধু `Tab` কী দিয়ে পুরো সাইট ব্যবহার করা যাচ্ছে?
- [ ] **Focus**: ফোকাস করা এলিমেন্টের চারপাশ কি হাইলাইট হচ্ছে (outline)?
- [ ] **Links**: লিংকের টেক্সট কি বোঝা যাচ্ছে? ("Click here" এর বদলে "Read Guide")

---

এই গাইডটি ফলো করলে আপনার কোড হবে **Professional**, **SEO Friendly**, এবং **Accessible**। এটি আপনাকে ইন্টারভিউ এবং রিমোট জবের জন্য অন্যদের চেয়ে এগিয়ে রাখবে।
