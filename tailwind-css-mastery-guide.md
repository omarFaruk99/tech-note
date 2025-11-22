# Tailwind CSS Mastery Guide (Bangla) 🎨

Tailwind CSS এখন মডার্ন ওয়েব ডেভেলপমেন্টের **স্ট্যান্ডার্ড**। আপনি যদি এখনও ভ্যানিলা CSS বা Bootstrap ব্যবহার করেন, তবে আপনি পিছিয়ে আছেন। এই গাইডটি আপনাকে Tailwind CSS এর প্রো হতে সাহায্য করবে।

---

## ১. Tailwind CSS কেন? (Why Tailwind?)

1.  **Speed:** ক্লাস নাম চিন্তা করতে হয় না (`wrapper-inner-box` এর দিন শেষ)।
2.  **Consistency:** ডিজাইন সিস্টেমেটিক থাকে (স্পেসিং, কালার সব প্রি-ডিফাইনড)।
3.  **Responsive:** মোবাইল রেসপন্সিভ করা পানির মতো সহজ।
4.  **Small Bundle Size:** প্রোডাকশনে অব্যবহৃত CSS রিমুভ করে দেয়।

---

## ২. সেটআপ (Next.js)

Next.js প্রজেক্ট তৈরি করার সময় `Would you like to use Tailwind CSS?` এ `Yes` দিলে অটোমেটিক সেটআপ হয়ে যায়।

ম্যানুয়ালি করতে হলে:

```bash
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

`tailwind.config.js`:

```javascript
module.exports = {
  content: ["./app/**/*.{js,ts,jsx,tsx}", "./components/**/*.{js,ts,jsx,tsx}"],
  theme: {
    extend: {},
  },
  plugins: [],
};
```

`globals.css`:

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

---

## ৩. কোর কনসেপ্ট (Core Concepts)

### ১. কালার এবং ব্যাকগ্রাউন্ড

```jsx
<div className="bg-blue-500 text-white p-4">Hello World</div>
```

- `bg-{color}-{shade}`: ব্যাকগ্রাউন্ড কালার (50-950)।
- `text-{color}-{shade}`: টেক্সট কালার।

### ২. স্পেসিং (Padding & Margin)

Tailwind এ `1 unit = 4px`।

- `p-4` = `padding: 1rem` (16px)
- `m-2` = `margin: 0.5rem` (8px)
- `px-4` = ডানে-বামে প্যাডিং।
- `my-2` = উপরে-নিচে মার্জিন।

### ৩. ফ্লেক্সবক্স (Flexbox) - সবচেয়ে বেশি ব্যবহৃত

```jsx
<div className="flex items-center justify-between">
  <div>Logo</div>
  <div>Menu</div>
</div>
```

- `flex`: `display: flex`
- `items-center`: `align-items: center`
- `justify-center`: `justify-content: center`
- `gap-4`: `gap: 1rem`

### ৪. গ্রিড (Grid)

```jsx
<div className="grid grid-cols-3 gap-4">
  <div>1</div>
  <div>2</div>
  <div>3</div>
</div>
```

---

## ৪. রেসপন্সিভ ডিজাইন (Responsive Design) 📱

Tailwind এ মিডিয়া কুয়েরি লেখার দরকার নেই। শুধু প্রিফিক্স ব্যবহার করুন:

- `sm:` (640px+)
- `md:` (768px+)
- `lg:` (1024px+)
- `xl:` (1280px+)

**মোবাইল-ফার্স্ট অ্যাপ্রোচ:**
ডিফল্ট ক্লাসগুলো মোবাইলের জন্য লিখুন, তারপর বড় স্ক্রিনের জন্য চেঞ্জ করুন।

```jsx
// মোবাইলে ১ কলাম, ট্যাবলেটে ২ কলাম, ডেস্কটপে ৩ কলাম
<div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
  {/* Cards */}
</div>
```

---

## ৫. স্টেটস (Hover, Focus, Active)

```jsx
<button className="bg-blue-500 hover:bg-blue-700 focus:ring-2 focus:ring-blue-300 active:bg-blue-800 text-white px-4 py-2 rounded">
  Click Me
</button>
```

---

## ৬. রিইউজেবিলিটি (Reusability)

অনেকে বলে Tailwind এ কোড রিপিট হয়। এর সমাধান হলো **Component Extraction**।

**খারাপ প্র্যাকটিস (`@apply` ব্যবহার করা):**

```css
/* globals.css - Avoid this mostly */
.btn {
  @apply bg-blue-500 text-white px-4 py-2 rounded;
}
```

**ভালো প্র্যাকটিস (React Component):**

```jsx
// components/Button.jsx
export default function Button({ children, className, ...props }) {
  return (
    <button
      className={`bg-blue-500 text-white px-4 py-2 rounded hover:bg-blue-600 transition ${className}`}
      {...props}
    >
      {children}
    </button>
  );
}
```

এখন আপনি `<Button>Click</Button>` ব্যবহার করতে পারবেন এবং দরকার হলে `className` দিয়ে স্টাইল ওভাররাইড করতে পারবেন (`tailwind-merge` প্যাকেজটি এখানে খুব কাজের)।

---

## ৭. কাস্টমাইজেশন (Tailwind Config)

আপনার প্রজেক্টের নির্দিষ্ট কালার বা ফন্ট সেট করতে `tailwind.config.js` এ `extend` করুন।

```javascript
theme: {
  extend: {
    colors: {
      primary: "#FF5733", // এখন bg-primary ব্যবহার করা যাবে
      brand: {
        100: "#cffafe",
        900: "#164e63",
      }
    },
    fontFamily: {
      sans: ["Inter", "sans-serif"],
    }
  }
}
```

---

## ৮. ডার্ক মোড (Dark Mode) 🌙

১. কনফিগে `darkMode: 'class'` দিন।
২. `dark:` প্রিফিক্স ব্যবহার করুন।

```jsx
<div className="bg-white dark:bg-gray-900 text-black dark:text-white">
  <h1>Hello Dark Mode</h1>
</div>
```

---

## ৯. চেকলিস্ট (Job Ready Checklist)

- [ ] আমি ফ্লেক্সবক্স (`flex`, `justify-between`, `items-center`) দিয়ে লেআউট বানাতে পারি।
- [ ] আমি রেসপন্সিভ প্রিফিক্স (`md:`, `lg:`) ব্যবহার করতে পারি।
- [ ] আমি `hover:` এবং `focus:` স্টেট ব্যবহার করতে পারি।
- [ ] আমি কাস্টম কালার কনফিগার করতে পারি।
- [ ] আমি জানি কেন `@apply` এর চেয়ে React Component বানানো ভালো।

---

## ১০. প্রো টিপস (Pro Tips)

- **VS Code Extension:** `Tailwind CSS IntelliSense` অবশ্যই ইনস্টল করুন। এটি অটো-সাজেশন দেয়।
- **Prettier Plugin:** `prettier-plugin-tailwindcss` ইনস্টল করুন, এটি অটোমেটিক ক্লাসগুলো সাজিয়ে দেয়।
- **shadcn/ui:** বর্তমানে সবচেয়ে জনপ্রিয় UI লাইব্রেরি যা Tailwind দিয়ে তৈরি। এটি শেখা মাস্ট!

Tailwind CSS একবার হাতে চলে আসলে আপনি আর সাধারণ CSS এ ফিরে যেতে চাইবেন না। হ্যাপি কোডিং! 🎨

---

## ১১. Complete Real-World Components

এখানে কিছু copy-paste ready কম্পোনেন্ট দেওয়া হলো যা আপনি সরাসরি আপনার প্রজেক্টে ব্যবহার করতে পারেন।

### ১. Professional Navbar (Responsive & Sticky)

```jsx
import { useState } from "react";

export default function Navbar() {
  const [isOpen, setIsOpen] = useState(false);

  return (
    <nav className="sticky top-0 z-50 w-full bg-white/80 backdrop-blur-md border-b border-gray-100">
      <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div className="flex justify-between h-16 items-center">
          {/* Logo */}
          <div className="flex-shrink-0 flex items-center">
            <span className="text-2xl font-bold text-blue-600">BrandLogo</span>
          </div>

          {/* Desktop Menu */}
          <div className="hidden md:flex space-x-8">
            <a
              href="#"
              className="text-gray-700 hover:text-blue-600 px-3 py-2 rounded-md text-sm font-medium transition-colors"
            >
              Home
            </a>
            <a
              href="#"
              className="text-gray-700 hover:text-blue-600 px-3 py-2 rounded-md text-sm font-medium transition-colors"
            >
              Features
            </a>
            <a
              href="#"
              className="text-gray-700 hover:text-blue-600 px-3 py-2 rounded-md text-sm font-medium transition-colors"
            >
              Pricing
            </a>
            <a
              href="#"
              className="bg-blue-600 text-white px-4 py-2 rounded-full text-sm font-medium hover:bg-blue-700 transition-colors"
            >
              Get Started
            </a>
          </div>

          {/* Mobile Menu Button */}
          <div className="md:hidden flex items-center">
            <button
              onClick={() => setIsOpen(!isOpen)}
              className="text-gray-700 hover:text-blue-600 focus:outline-none p-2"
            >
              <svg
                className="h-6 w-6"
                fill="none"
                viewBox="0 0 24 24"
                stroke="currentColor"
              >
                {isOpen ? (
                  <path
                    strokeLinecap="round"
                    strokeLinejoin="round"
                    strokeWidth={2}
                    d="M6 18L18 6M6 6l12 12"
                  />
                ) : (
                  <path
                    strokeLinecap="round"
                    strokeLinejoin="round"
                    strokeWidth={2}
                    d="M4 6h16M4 12h16M4 18h16"
                  />
                )}
              </svg>
            </button>
          </div>
        </div>
      </div>

      {/* Mobile Menu */}
      {isOpen && (
        <div className="md:hidden bg-white border-t border-gray-100 absolute w-full">
          <div className="px-2 pt-2 pb-3 space-y-1 sm:px-3">
            <a
              href="#"
              className="block px-3 py-2 rounded-md text-base font-medium text-gray-700 hover:text-blue-600 hover:bg-gray-50"
            >
              Home
            </a>
            <a
              href="#"
              className="block px-3 py-2 rounded-md text-base font-medium text-gray-700 hover:text-blue-600 hover:bg-gray-50"
            >
              Features
            </a>
            <a
              href="#"
              className="block px-3 py-2 rounded-md text-base font-medium text-gray-700 hover:text-blue-600 hover:bg-gray-50"
            >
              Pricing
            </a>
            <a
              href="#"
              className="block px-3 py-2 rounded-md text-base font-medium text-blue-600 font-bold bg-blue-50"
            >
              Get Started
            </a>
          </div>
        </div>
      )}
    </nav>
  );
}
```

### ২. Card Component (Product/Blog)

এটি একটি ইন্টারেক্টিভ কার্ড যা হোভার করলে একটু বড় হবে এবং শ্যাডো বাড়বে।

```jsx
export default function ProductCard() {
  return (
    <div className="group relative bg-white rounded-2xl shadow-sm border border-gray-100 overflow-hidden hover:shadow-xl hover:-translate-y-1 transition-all duration-300">
      {/* Image Container */}
      <div className="aspect-w-16 aspect-h-9 w-full overflow-hidden bg-gray-200">
        <img
          src="https://images.unsplash.com/photo-1542291026-7eec264c27ff"
          alt="Product"
          className="h-48 w-full object-cover object-center group-hover:scale-105 transition-transform duration-500"
        />
      </div>

      {/* Content */}
      <div className="p-5">
        <div className="flex justify-between items-start">
          <div>
            <p className="text-sm text-blue-600 font-semibold mb-1">Sneakers</p>
            <h3 className="text-lg font-bold text-gray-900 mb-2">
              Nike Air Max
            </h3>
          </div>
          <span className="bg-green-100 text-green-800 text-xs font-bold px-2 py-1 rounded-full">
            $120
          </span>
        </div>

        <p className="text-gray-500 text-sm mb-4 line-clamp-2">
          The ultimate comfort for your daily run. Featuring breathable mesh and
          responsive cushioning.
        </p>

        <button className="w-full bg-gray-900 text-white py-2.5 rounded-xl font-medium hover:bg-blue-600 transition-colors flex items-center justify-center gap-2">
          Add to Cart
          <svg
            className="w-4 h-4"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
          >
            <path
              strokeLinecap="round"
              strokeLinejoin="round"
              strokeWidth="2"
              d="M16 11V7a4 4 0 00-8 0v4M5 9h14l1 12H4L5 9z"
            ></path>
          </svg>
        </button>
      </div>
    </div>
  );
}
```

### ৩. Form with Validation States

```jsx
export default function ContactForm() {
  // উদাহরণ হিসেবে error state দেখানো হয়েছে
  const isError = true;

  return (
    <form className="max-w-md mx-auto p-6 bg-white rounded-2xl shadow-lg border border-gray-100">
      <h2 className="text-2xl font-bold text-gray-800 mb-6">Contact Us</h2>

      <div className="space-y-4">
        {/* Name Input - Normal State */}
        <div>
          <label
            htmlFor="name"
            className="block text-sm font-medium text-gray-700 mb-1"
          >
            Full Name
          </label>
          <input
            type="text"
            id="name"
            className="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 outline-none transition-all"
            placeholder="John Doe"
          />
        </div>

        {/* Email Input - Error State */}
        <div>
          <label
            htmlFor="email"
            className="block text-sm font-medium text-gray-700 mb-1"
          >
            Email Address
          </label>
          <div className="relative">
            <input
              type="email"
              id="email"
              className={`w-full px-4 py-2 border rounded-lg outline-none transition-all ${
                isError
                  ? "border-red-500 focus:ring-2 focus:ring-red-200 text-red-900 placeholder-red-300"
                  : "border-gray-300 focus:ring-2 focus:ring-blue-500"
              }`}
              placeholder="john@example.com"
              defaultValue="invalid-email"
            />
            {isError && (
              <div className="absolute inset-y-0 right-0 pr-3 flex items-center pointer-events-none">
                <svg
                  className="h-5 w-5 text-red-500"
                  fill="currentColor"
                  viewBox="0 0 20 20"
                >
                  <path
                    fillRule="evenodd"
                    d="M18 10a8 8 0 11-16 0 8 8 0 0116 0zm-7 4a1 1 0 11-2 0 1 1 0 012 0zm-1-9a1 1 0 00-1 1v4a1 1 0 102 0V6a1 1 0 00-1-1z"
                    clipRule="evenodd"
                  />
                </svg>
              </div>
            )}
          </div>
          {isError && (
            <p className="mt-1 text-sm text-red-600">
              Please enter a valid email address.
            </p>
          )}
        </div>

        <button
          type="submit"
          className="w-full bg-blue-600 text-white py-2.5 rounded-lg font-semibold hover:bg-blue-700 focus:ring-4 focus:ring-blue-200 transition-all"
        >
          Send Message
        </button>
      </div>
    </form>
  );
}
```

### ৪. Modal/Dialog (with Backdrop)

```jsx
export default function Modal({ isOpen, onClose }) {
  if (!isOpen) return null;

  return (
    <div className="fixed inset-0 z-50 flex items-center justify-center p-4">
      {/* Backdrop with blur and fade */}
      <div
        className="fixed inset-0 bg-black/50 backdrop-blur-sm transition-opacity"
        onClick={onClose}
      ></div>

      {/* Modal Content */}
      <div className="relative bg-white rounded-2xl shadow-2xl w-full max-w-md p-6 transform transition-all scale-100 animate-in fade-in zoom-in duration-200">
        <div className="text-center">
          <div className="mx-auto flex items-center justify-center h-12 w-12 rounded-full bg-green-100 mb-4">
            <svg
              className="h-6 w-6 text-green-600"
              fill="none"
              stroke="currentColor"
              viewBox="0 0 24 24"
            >
              <path
                strokeLinecap="round"
                strokeLinejoin="round"
                strokeWidth="2"
                d="M5 13l4 4L19 7"
              ></path>
            </svg>
          </div>
          <h3 className="text-lg font-bold text-gray-900">
            Payment Successful!
          </h3>
          <p className="text-sm text-gray-500 mt-2">
            Your transaction has been completed. You will receive a confirmation
            email shortly.
          </p>
        </div>

        <div className="mt-6">
          <button
            onClick={onClose}
            className="w-full inline-flex justify-center px-4 py-2 text-sm font-medium text-white bg-blue-600 border border-transparent rounded-lg hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500"
          >
            Go to Dashboard
          </button>
        </div>
      </div>
    </div>
  );
}
```

### ৫. Hero Section

```jsx
export default function Hero() {
  return (
    <div className="relative bg-white overflow-hidden">
      <div className="max-w-7xl mx-auto">
        <div className="relative z-10 pb-8 bg-white sm:pb-16 md:pb-20 lg:max-w-2xl lg:w-full lg:pb-28 xl:pb-32">
          <main className="mt-10 mx-auto max-w-7xl px-4 sm:mt-12 sm:px-6 md:mt-16 lg:mt-20 lg:px-8 xl:mt-28">
            <div className="sm:text-center lg:text-left">
              <h1 className="text-4xl tracking-tight font-extrabold text-gray-900 sm:text-5xl md:text-6xl">
                <span className="block xl:inline">Data to enrich your</span>{" "}
                <span className="block text-blue-600 xl:inline">
                  online business
                </span>
              </h1>
              <p className="mt-3 text-base text-gray-500 sm:mt-5 sm:text-lg sm:max-w-xl sm:mx-auto md:mt-5 md:text-xl lg:mx-0">
                Anim aute id magna aliqua ad ad non deserunt sunt. Qui irure qui
                lorem cupidatat commodo. Elit sunt amet fugiat veniam occaecat
                fugiat aliqua.
              </p>
              <div className="mt-5 sm:mt-8 sm:flex sm:justify-center lg:justify-start">
                <div className="rounded-md shadow">
                  <a
                    href="#"
                    className="w-full flex items-center justify-center px-8 py-3 border border-transparent text-base font-medium rounded-md text-white bg-blue-600 hover:bg-blue-700 md:py-4 md:text-lg md:px-10"
                  >
                    Get started
                  </a>
                </div>
                <div className="mt-3 sm:mt-0 sm:ml-3">
                  <a
                    href="#"
                    className="w-full flex items-center justify-center px-8 py-3 border border-transparent text-base font-medium rounded-md text-blue-700 bg-blue-100 hover:bg-blue-200 md:py-4 md:text-lg md:px-10"
                  >
                    Live demo
                  </a>
                </div>
              </div>
            </div>
          </main>
        </div>
      </div>
      <div className="lg:absolute lg:inset-y-0 lg:right-0 lg:w-1/2">
        <img
          className="h-56 w-full object-cover sm:h-72 md:h-96 lg:w-full lg:h-full"
          src="https://images.unsplash.com/photo-1551434678-e076c223a692?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=2850&q=80"
          alt=""
        />
      </div>
    </div>
  );
}
```

---

## ১২. Advanced Utilities এবং Patterns

Tailwind এর কিছু পাওয়ারফুল ফিচার যা আপনার কাজকে অনেক সহজ করে দেবে।

### ১. Typography Utilities

- **Font Size:** `text-xs` (0.75rem) থেকে `text-9xl` (8rem) পর্যন্ত।
- **Font Weight:** `font-thin` (100) থেকে `font-black` (900)।
- **Line Height:** `leading-none`, `leading-tight`, `leading-loose`।
- **Letter Spacing:** `tracking-tighter` থেকে `tracking-widest`।

```jsx
<h1 className="text-5xl font-extrabold tracking-tight leading-tight text-gray-900">
  Mastering{" "}
  <span className="text-blue-600 underline decoration-wavy decoration-blue-300">
    Tailwind
  </span>
</h1>
```

### ২. Shadows, Borders, and Rounded

- **Shadows:** `shadow-sm`, `shadow-md`, `shadow-lg`, `shadow-xl`, `shadow-2xl`, `shadow-inner`।
- **Rounded:** `rounded-sm`, `rounded-md`, `rounded-lg`, `rounded-xl`, `rounded-2xl`, `rounded-full` (circle)।
- **Ring:** ফোকাস স্টেটের জন্য `ring` খুব কাজের।

```jsx
<button className="rounded-full bg-white p-4 shadow-lg ring-1 ring-gray-900/5 hover:scale-105 transition">
  Click Me
</button>
```

### ৩. Animations and Transitions

Tailwind এ বিল্ট-ইন কিছু অ্যানিমেশন আছে, তবে `transition` এবং `transform` দিয়ে আপনি যেকোনো কিছু বানাতে পারেন।

- **Built-in:** `animate-spin` (loading), `animate-bounce`, `animate-pulse` (skeleton loader)।

```jsx
// Loading Spinner
<div className="animate-spin h-8 w-8 border-4 border-blue-500 border-t-transparent rounded-full"></div>

// Interactive Button
<button className="bg-blue-500 hover:bg-blue-600 text-white px-6 py-2 rounded-lg transition-all duration-300 hover:scale-105 hover:shadow-lg active:scale-95">
  Hover Me
</button>
```

### ৪. Group and Peer Modifiers

প্যারেন্ট এলিমেন্টের হোভার বা ফোকাস স্টেটের উপর ভিত্তি করে চাইল্ড স্টাইল করতে `group` ব্যবহার করুন।

**Group Hover:**

```jsx
<div className="group bg-white p-6 hover:bg-blue-500 rounded-xl transition-colors cursor-pointer">
  <h3 className="text-gray-900 group-hover:text-white font-bold">Card Title</h3>
  <p className="text-gray-500 group-hover:text-blue-100">
    পুরো কার্ড হোভার করলে এই টেক্সটের কালারও চেঞ্জ হবে।
  </p>
</div>
```

**Peer Focus (Form Validation):**
ভাই-বোন (sibling) এলিমেন্টের স্টেটের উপর ভিত্তি করে স্টাইল করতে `peer` ব্যবহার করুন।

```jsx
<div className="relative">
  <input
    type="text"
    id="username"
    className="peer border border-gray-300 rounded px-4 py-2 w-full focus:outline-none focus:border-blue-500 placeholder-transparent"
    placeholder="Username"
  />
  <label
    htmlFor="username"
    className="absolute left-4 -top-2.5 bg-white px-1 text-sm text-gray-600 transition-all peer-placeholder-shown:text-base peer-placeholder-shown:text-gray-400 peer-placeholder-shown:top-2 peer-focus:-top-2.5 peer-focus:text-sm peer-focus:text-blue-600"
  >
    Username
  </label>
</div>
```

### ৫. Arbitrary Values (JIT Mode)

Tailwind এর ডিফল্ট ভ্যালু যথেষ্ট না হলে `[]` ব্যবহার করে কাস্টম ভ্যালু দিতে পারেন।

- `w-[137px]`: একদম নির্দিষ্ট উইডথ।
- `bg-[#1da1f2]`: নির্দিষ্ট হেক্স কোড (যেমন Twitter Blue)।
- `top-[15%]`: পার্সেন্টেজ পজিশনিং।

```jsx
<div className="bg-[#24292F] text-white text-[15px] p-[18px] rounded-[10px]">
  GitHub Style Custom Values
</div>
```

_টিপ: এটি খুব বেশি ব্যবহার করবেন না, এতে কনসিস্টেন্সি নষ্ট হয়। বারবার একই ভ্যালু লাগলে `tailwind.config.js` এ অ্যাড করে নিন।_

---

## ১৩. Dynamic Classes এবং Conditional Styling

React এ কন্ডিশনাল ক্লাস হ্যান্ডেল করার জন্য কিছু স্মার্ট টুলস আছে।

### ১. clsx/classnames Library

যখন অনেকগুলো কন্ডিশনাল ক্লাস থাকে, তখন টেম্পলেট লিটারেল `${isError ? 'bg-red' : 'bg-green'}` ব্যবহার করা কঠিন হয়ে যায়। `clsx` এটি সহজ করে।

**Installation:**

```bash
npm install clsx
```

**Usage:**

```jsx
import clsx from "clsx";

function Button({ isPrimary, isLarge, isDisabled }) {
  return (
    <button
      className={clsx(
        "rounded px-4 py-2 font-bold", // Always applied
        {
          "bg-blue-500 text-white": isPrimary, // Only if isPrimary is true
          "bg-gray-200 text-gray-800": !isPrimary,
          "text-lg": isLarge,
          "opacity-50 cursor-not-allowed": isDisabled,
        }
      )}
    >
      Click Me
    </button>
  );
}
```

### ২. tailwind-merge (cn function)

Tailwind এ একটি কমন সমস্যা হলো ক্লাস কনফ্লিক্ট। ধরুন আপনি একটি `Button` কম্পোনেন্ট বানালেন যার ডিফল্ট প্যাডিং `p-4`। এখন আপনি যদি `<Button className="p-8" />` ব্যবহার করেন, তবে `p-4` এবং `p-8` দুটোই ক্লাসে থাকবে এবং CSS এর নিয়ম অনুযায়ী যেটি পরে ডিফাইন করা সেটি কাজ করবে (যা সবসময় প্রেডিক্টেবল না)।

`tailwind-merge` এই ডুপ্লিকেট ক্লাসগুলো রিমুভ করে শেষেরটিকে রাখে।

**Installation:**

```bash
npm install clsx tailwind-merge
```

**Utility Function (lib/utils.js):**
এটি shadcn/ui সহ সব মডার্ন প্রজেক্টে স্ট্যান্ডার্ড।

```js
import { clsx } from "clsx";
import { twMerge } from "tailwind-merge";

export function cn(...inputs) {
  return twMerge(clsx(inputs));
}
```

**Usage:**

```jsx
import { cn } from "@/lib/utils";

export default function Button({ className, ...props }) {
  return (
    <button
      className={cn(
        "bg-blue-500 text-white px-4 py-2 rounded hover:bg-blue-600 transition",
        className // এখানে পাস করা ক্লাসগুলো ডিফল্ট ক্লাসকে ওভাররাইড করবে
      )}
      {...props}
    />
  );
}

// ব্যবহার:
// <Button className="bg-red-500" /> -> নীল কালার সরে লাল হয়ে যাবে।
```

---

## ১৪. shadcn/ui Integration

[shadcn/ui](https://ui.shadcn.com/) বর্তমানে React ইকোসিস্টেমের সবচেয়ে জনপ্রিয় কম্পোনেন্ট লাইব্রেরি। এটি কোনো npm প্যাকেজ নয়, বরং এটি আপনাকে কোড কপি-পেস্ট করার বা CLI দিয়ে জেনারেট করার সুবিধা দেয়। এটি Radix UI এবং Tailwind CSS এর উপর ভিত্তি করে তৈরি।

### ১. কেন ব্যবহার করবেন?

- **Full Control:** কোড আপনার প্রজেক্টে থাকে, তাই যা ইচ্ছা কাস্টমাইজ করতে পারেন।
- **Accessible:** কিবোর্ড নেভিগেশন এবং স্ক্রিন রিডার সাপোর্ট বিল্ট-ইন।
- **Beautiful:** ডিফল্ট ডিজাইন খুবই ক্লিন এবং মডার্ন।

### ২. Installation (Next.js)

```bash
npx shadcn-ui@latest init
```

সেটআপের সময় কিছু প্রশ্ন করবে (TypeScript, Style, Color), ডিফল্ট ভ্যালু সিলেক্ট করুন।

### ৩. Button Component ব্যবহার

```bash
npx shadcn-ui@latest add button
```

এটি `components/ui/button.tsx` ফাইলে বাটন কম্পোনেন্ট তৈরি করবে।

**Usage:**

```jsx
import { Button } from "@/components/ui/button";

export default function Home() {
  return (
    <div className="space-x-4">
      <Button>Default Button</Button>
      <Button variant="destructive">Delete</Button>
      <Button variant="outline">Cancel</Button>
      <Button variant="ghost">Ghost</Button>
      <Button variant="link">Link</Button>
    </div>
  );
}
```

### ৪. Form Components

```bash
npx shadcn-ui@latest add input label
```

**Complete Form Example:**

```jsx
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";
import { Label } from "@/components/ui/label";

export function LoginForm() {
  return (
    <div className="grid w-full max-w-sm items-center gap-1.5 space-y-4">
      <div className="space-y-2">
        <Label htmlFor="email">Email</Label>
        <Input type="email" id="email" placeholder="Email" />
      </div>
      <div className="space-y-2">
        <Label htmlFor="password">Password</Label>
        <Input type="password" id="password" placeholder="Password" />
      </div>
      <Button type="submit" className="w-full">
        Login
      </Button>
    </div>
  );
}
```

---

## ১৫. Responsive Design Advanced Patterns

Tailwind এ রেসপন্সিভ ডিজাইন করা খুবই সহজ, তবে কিছু অ্যাডভান্সড প্যাটার্ন জানলে আপনার কাজ আরও সহজ হবে।

### ১. Show/Hide Elements

মোবাইলে কিছু এলিমেন্ট লুকিয়ে রাখা এবং ডেস্কটপে দেখানো (বা উল্টোটা) খুবই কমন।

```jsx
// মোবাইলে লুকানো, ডেস্কটপে দেখানো
<div className="hidden md:block">
  এই কন্টেন্ট শুধু ট্যাবলেট এবং ডেস্কটপে দেখা যাবে
</div>

// মোবাইলে দেখানো, ডেস্কটপে লুকানো
<div className="block md:hidden">
  এই কন্টেন্ট শুধু মোবাইলে দেখা যাবে
</div>

// Hamburger Menu Example
<button className="md:hidden">
  {/* Mobile Menu Icon */}
  <svg>...</svg>
</button>
```

### ২. Layout Changes (Mobile → Desktop)

মোবাইলে স্ট্যাকড লেআউট, ডেস্কটপে সাইড-বাই-সাইড।

```jsx
// মোবাইলে উপর-নিচে, ডেস্কটপে পাশাপাশি
<div className="flex flex-col md:flex-row gap-4">
  <div className="w-full md:w-1/2 bg-blue-100 p-4">Left Content</div>
  <div className="w-full md:w-1/2 bg-green-100 p-4">Right Content</div>
</div>

// Grid Example
<div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">
  {/* মোবাইলে ১ কলাম, ট্যাবলেটে ২ কলাম, ডেস্কটপে ৪ কলাম */}
  <div>Card 1</div>
  <div>Card 2</div>
  <div>Card 3</div>
  <div>Card 4</div>
</div>
```

### ৩. Text Size Scaling

মোবাইলে ছোট টেক্সট, ডেস্কটপে বড় টেক্সট।

```jsx
<h1 className="text-2xl sm:text-3xl md:text-4xl lg:text-5xl font-bold">
  Responsive Heading
</h1>

<p className="text-sm md:text-base lg:text-lg">
  এই প্যারাগ্রাফের সাইজ স্ক্রিন সাইজের সাথে বাড়বে।
</p>
```

**Complete Responsive Page Example:**

```jsx
export default function ResponsivePage() {
  return (
    <div className="min-h-screen bg-gray-50">
      {/* Hero Section */}
      <section className="px-4 py-12 md:py-20 lg:py-28">
        <div className="max-w-7xl mx-auto">
          <h1 className="text-3xl sm:text-4xl md:text-5xl lg:text-6xl font-extrabold text-gray-900 text-center">
            Build Anything
          </h1>
          <p className="mt-4 text-base md:text-lg lg:text-xl text-gray-600 text-center max-w-2xl mx-auto">
            A complete responsive design example
          </p>
        </div>
      </section>

      {/* Features Grid */}
      <section className="px-4 py-12">
        <div className="max-w-7xl mx-auto grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
          {[1, 2, 3, 4, 5, 6].map((i) => (
            <div key={i} className="bg-white p-6 rounded-xl shadow-sm">
              <h3 className="text-lg font-bold">Feature {i}</h3>
              <p className="text-sm text-gray-600 mt-2">Description here</p>
            </div>
          ))}
        </div>
      </section>
    </div>
  );
}
```

---

## ১৬. Performance এবং Optimization

Tailwind CSS ডিফল্টভাবেই পারফরম্যান্স অপটিমাইজড, তবে কিছু বিষয় জানা জরুরি।

### ১. JIT Mode (Just-In-Time)

Tailwind v3+ এ JIT মোড ডিফল্ট। এটি অন-ডিমান্ড CSS জেনারেট করে, ফলে:

- **ডেভেলপমেন্ট দ্রুত হয়:** পুরো CSS ফাইল জেনারেট করতে হয় না।
- **Arbitrary Values সাপোর্ট:** `w-[137px]` এর মতো কাস্টম ভ্যালু ব্যবহার করা যায়।
- **ছোট বান্ডেল সাইজ:** শুধু ব্যবহৃত ক্লাসগুলোই ফাইনাল CSS এ যায়।

আপনার `tailwind.config.js` এ JIT মোড চালু আছে কিনা চেক করার দরকার নেই, এটি ডিফল্টভাবেই চালু।

### ২. PurgeCSS Configuration

প্রোডাকশনে অব্যবহৃত CSS রিমুভ করার জন্য `content` পাথ সঠিকভাবে কনফিগার করা জরুরি।

```javascript
// tailwind.config.js
module.exports = {
  content: [
    "./app/**/*.{js,ts,jsx,tsx,mdx}",
    "./pages/**/*.{js,ts,jsx,tsx,mdx}",
    "./components/**/*.{js,ts,jsx,tsx,mdx}",
    "./src/**/*.{js,ts,jsx,tsx,mdx}", // যদি src ফোল্ডার থাকে
  ],
  // ...
};
```

**গুরুত্বপূর্ণ:** যদি আপনি ডায়নামিক ক্লাস নেম ব্যবহার করেন (যেমন: `bg-${color}-500`), তবে সেগুলো পার্জ হয়ে যাবে। এর পরিবর্তে পুরো ক্লাস নেম লিখুন।

❌ **ভুল:**

```jsx
const color = "blue";
<div className={`bg-${color}-500`}>Text</div>; // এটি কাজ করবে না
```

✅ **সঠিক:**

```jsx
const colorClasses = {
  blue: "bg-blue-500",
  red: "bg-red-500",
};
<div className={colorClasses[color]}>Text</div>;
```

### ৩. Production Bundle Size

একটি সাধারণ Tailwind প্রজেক্টের প্রোডাকশন CSS সাইজ **5-15 KB** (gzipped) হওয়া উচিত। যদি এর চেয়ে বেশি হয়, তবে:

- `content` পাথ চেক করুন।
- অপ্রয়োজনীয় প্লাগইন রিমুভ করুন।
- `@apply` এর অতিরিক্ত ব্যবহার কমান।

### ৪. Common Performance Mistakes

❌ **Mistake 1: Arbitrary Values এর অতিরিক্ত ব্যবহার**

```jsx
// খারাপ
<div className="w-[237px] h-[189px] bg-[#FF5733] p-[23px]">...</div>
```

✅ **সমাধান:** বারবার ব্যবহৃত ভ্যালু `tailwind.config.js` এ অ্যাড করুন।

❌ **Mistake 2: Dynamic Class Names**

```jsx
// এটি পার্জ হয়ে যাবে
<div className={`text-${size}`}>Text</div>
```

❌ **Mistake 3: `!important` এর অতিরিক্ত ব্যবহার**

```jsx
// এড়িয়ে চলুন
<div className="!bg-red-500 !p-8">...</div>
```

---

## ১৭. Common Mistakes এবং Anti-Patterns

Tailwind ব্যবহার করার সময় কিছু কমন ভুল এড়িয়ে চলুন।

### ❌ Don't Do:

**১. `@apply` এর অতিরিক্ত ব্যবহার**

```css
/* globals.css - এড়িয়ে চলুন */
.btn {
  @apply bg-blue-500 text-white px-4 py-2 rounded hover:bg-blue-600;
}
.card {
  @apply bg-white p-6 rounded-xl shadow-md;
}
```

**সমস্যা:** এতে CSS ফাইল বড় হয়, Tailwind এর সুবিধা কমে যায়।

**২. Inline Styles + Tailwind Mix করা**

```jsx
// খারাপ
<div className="p-4" style={{ backgroundColor: "red" }}>
  ...
</div>
```

**সমস্যা:** কনসিস্টেন্সি নষ্ট হয়, ডিবাগ করা কঠিন।

**৩. `!important` এর অপব্যবহার**

```jsx
// এড়িয়ে চলুন
<div className="!bg-red-500 !text-white !p-8">...</div>
```

**সমস্যা:** CSS specificity সমস্যা তৈরি করে।

**৪. Arbitrary Values সর্বত্র ব্যবহার**

```jsx
// কনসিস্টেন্সি নষ্ট করে
<div className="w-[237px] h-[189px] p-[23px] text-[17px]">...</div>
```

**৫. Spacing Scale Ignore করা**

```jsx
// খারাপ
<div className="p-[13px] m-[7px]">...</div>

// ভালো
<div className="p-3 m-2">...</div> // Tailwind এর spacing scale ব্যবহার করুন
```

---

### ✅ Do Instead:

**১. React Components Extract করুন**

```jsx
// components/Button.jsx
export default function Button({ variant = "primary", children, ...props }) {
  const variants = {
    primary: "bg-blue-500 hover:bg-blue-600 text-white",
    secondary: "bg-gray-200 hover:bg-gray-300 text-gray-800",
    danger: "bg-red-500 hover:bg-red-600 text-white",
  };

  return (
    <button
      className={`px-4 py-2 rounded font-medium transition ${variants[variant]}`}
      {...props}
    >
      {children}
    </button>
  );
}
```

**২. Config এ Custom Values Define করুন**

```javascript
// tailwind.config.js
module.exports = {
  theme: {
    extend: {
      colors: {
        brand: {
          primary: "#FF5733",
          secondary: "#3498DB",
        },
      },
      spacing: {
        18: "4.5rem", // যদি বারবার লাগে
      },
    },
  },
};
```

**৩. Proper Component Composition**

```jsx
// ছোট, রিইউজেবল কম্পোনেন্ট বানান
function Card({ children }) {
  return <div className="bg-white p-6 rounded-xl shadow-md">{children}</div>;
}

function CardTitle({ children }) {
  return <h3 className="text-lg font-bold text-gray-900">{children}</h3>;
}

// ব্যবহার:
<Card>
  <CardTitle>My Card</CardTitle>
  <p>Content here</p>
</Card>;
```

**৪. `cn` Utility ব্যবহার করুন (tailwind-merge)**

```jsx
import { cn } from "@/lib/utils";

function Button({ className, ...props }) {
  return (
    <button
      className={cn("bg-blue-500 px-4 py-2 rounded", className)}
      {...props}
    />
  );
}
```

---

## শেষ কথা

Tailwind CSS শিখে ফেললে আপনার UI ডেভেলপমেন্ট স্পিড ৩-৫ গুণ বেড়ে যাবে। মনে রাখবেন:

- **Component-based thinking:** সবকিছু কম্পোনেন্টে ভাগ করুন।
- **Consistency is key:** Tailwind এর spacing/color scale ফলো করুন।
- **shadcn/ui শিখুন:** এটি বর্তমানে ইন্ডাস্ট্রি স্ট্যান্ডার্ড।

এখন আপনি Tailwind CSS এর প্রো! 🚀 হ্যাপি কোডিং!
