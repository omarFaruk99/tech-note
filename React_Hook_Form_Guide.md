# React Hook Form (RHF) - কমপ্লিট লার্নিং গাইড (২০২৪-২০২৫)

এই গাইডটি এমনভাবে তৈরি করা হয়েছে যাতে আপনি একজন **Junior Frontend Developer** হিসেবে ইউরোপ বা আমেরিকার রিমোট জবের জন্য **React Hook Form (RHF)** সম্পূর্ণভাবে শিখতে পারেন। এখানে **Next.js (App Router)**, **Tailwind CSS**, এবং **JavaScript** ব্যবহার করা হয়েছে।

---

## ১. RHF কী এবং কেন? (What & Why)

**React Hook Form (RHF)** হলো রিয়্যাক্ট অ্যাপ্লিকেশনে ফর্ম হ্যান্ডেল করার জন্য একটি লাইব্রেরি। সহজ কথায়, এটি ফর্মের ইনপুট নেওয়া, ভ্যালিডেশন (যাচাইকরণ) করা এবং ফর্ম সাবমিট করার প্রক্রিয়াকে অনেক সহজ এবং ফাস্ট করে তোলে। সাধারণ রিয়্যাক্ট `useState` দিয়ে ফর্ম বানাতে গেলে প্রতিটি ইনপুটের জন্য স্টেট ম্যানেজ করতে হয়, যা বড় ফর্মে অ্যাপকে স্লো করে দেয় (Re-render ইস্যু)। RHF এই সমস্যার সমাধান করে।

**কেন এটি মডার্ন প্রজেক্টে ব্যবহার করা হয়?**
১. **পারফরম্যান্স:** এটি "Uncontrolled Components" কনসেপ্ট ব্যবহার করে, তাই টাইপ করার সময় পুরো ফর্ম বা পেজ বারবার রেন্ডার হয় না।
২. **সহজ ভ্যালিডেশন:** Zod বা Yup এর মতো লাইব্রেরির সাথে এটি খুব সহজে কাজ করে।
৩. **ডেভেলপার এক্সপেরিয়েন্স:** কম কোড লিখে জটিল ফর্ম হ্যান্ডেল করা যায়।

**কখন ব্যবহার করবেন?**
যখন আপনার ফর্মে ২-৩টির বেশি ফিল্ড থাকে, ভ্যালিডেশন প্রয়োজন হয়, অথবা ফর্মটি জটিল হয় (যেমন: মাল্টি-স্টেপ ফর্ম), তখন RHF ব্যবহার করা উচিত। ছোট একটি সার্চ বারের জন্য সাধারণ `useState` যথেষ্ট, কিন্তু প্রফেশনাল প্রজেক্টে প্রায় সব ফর্মে RHF স্ট্যান্ডার্ড।

---

## ২. মূল কনসেপ্ট (Core Concepts)

নতুন হিসেবে এই ৫টি কনসেপ্ট আপনাকে বুঝতেই হবে:

১. **register (রেজিস্ট্রেশন):**

- **অ্যানালজি:** স্কুলে ভর্তি হওয়ার সময় যেমন নাম রেজিস্ট্রি খাতায় তুলতে হয়, তেমনি ফর্মের ইনপুটগুলোকে RHF এর হুকের সাথে কানেক্ট করতে `register` ফাংশন ব্যবহার করা হয়। এটি ইনপুট ফিল্ডকে RHF এর নিয়ন্ত্রণে নিয়ে আসে।

২. **handleSubmit (ফর্ম জমা দেওয়া):**

- **অ্যানালজি:** এটি হলো গেটকিপার। ফর্ম সাবমিট বাটনে ক্লিক করলে সে আগে চেক করে সব তথ্য ঠিক আছে কিনা (ভ্যালিডেশন)। সব ঠিক থাকলে সে আপনার দেওয়া ফাংশনটি (যেমন: API কল) রান করে।

৩. **watch (নজর রাখা):**

- **অ্যানালজি:** সিসিটিভি ক্যামেরা। আপনি যদি কোনো স্পেসিফিক ইনপুটের ভ্যালু লাইভ দেখতে চান (যেমন: পাসওয়ার্ড ফিল্ডে কী টাইপ হচ্ছে তা দেখানোর জন্য), তখন `watch` ব্যবহার করা হয়।

৪. **formState (ফর্মের অবস্থা):**

- **অ্যানালজি:** গাড়ির ড্যাশবোর্ড। ফর্মে কোনো এরর (errors) আছে কিনা, ফর্মটি সাবমিট হচ্ছে কিনা (isSubmitting), বা ইউজার ফর্মে হাত দিয়েছে কিনা (isDirty) - এসব তথ্য এখানে থাকে।

৫. **Controller (কন্ট্রোলার):**

- **অ্যানালজি:** অ্যাডাপ্টার। সাধারণ HTML ইনপুট (`<input />`) সরাসরি `register` দিয়ে কাজ করে। কিন্তু থার্ড-পার্টি লাইব্রেরি (যেমন: React Select, Datepicker) সরাসরি কাজ করে না। তাদের কানেক্ট করতে `Controller` ব্যবহার করা হয়।

---

## ৩. প্র্যাকটিক্যাল সেটআপ (Practical Setup)

আমরা **Next.js (App Router)** প্রজেক্টে সেটআপ করব।

### ১. ইন্সটলেশন

টার্মিনালে এই কমান্ডটি দিন:

```bash
npm install react-hook-form zod @hookform/resolvers
```

_নোট: আমরা ভ্যালিডেশনের জন্য `zod` এবং কানেকশনের জন্য `@hookform/resolvers` ব্যবহার করব। এটি এখন ইন্ডাস্ট্রি স্ট্যান্ডার্ড।_

### ২. ফোল্ডার স্ট্রাকচার (Scalable)

বড় প্রজেক্টের জন্য নিচের স্ট্রাকচারটি ফলো করবেন:

```
src/
├── app/
│   ├── (auth)/
│   │   ├── login/
│   │   │   └── page.js       # লগিন পেজ
│   │   └── register/
│   │   │   └── page.js       # রেজিস্টার পেজ
├── components/
│   ├── ui/                   # রিইউজেবল UI কম্পোনেন্ট (Input, Button)
│   └── forms/                # ফর্ম কম্পোনেন্ট (LoginForm, RegisterForm)
├── lib/
│   └── axios.js              # Axios কনফিগারেশন
├── schemas/                  # Zod ভ্যালিডেশন স্কিমা
│   └── authSchema.js
├── services/                 # API কল ফাংশন
│   └── authService.js
└── hooks/                    # কাস্টম হুক
    └── useAuth.js
```

---

## ৪. প্রফেশনাল কোড অর্গানাইজেশন

একজন জুনিয়র হিসেবে আপনাকে কোড গুছিয়ে লিখতে হবে।

- **Separation of Concerns:** ফর্মের লজিক (Logic) এবং ডিজাইন (UI) আলাদা রাখার চেষ্টা করবেন।
- **File Naming:** ফাইল নাম `PascalCase` (যেমন: `LoginForm.js`) এবং ফোল্ডার বা ইউটিলিটি `kebab-case` বা `camelCase` (যেমন: `authService.js`)।
- **Services Folder:** সরাসরি কম্পোনেন্টের ভেতর `fetch` বা `axios` কল করবেন না। এগুলো `/services` ফোল্ডারে রাখবেন।

**উদাহরণ:**

- **ভুল:** `LoginForm.js` এর ভেতর `axios.post('/login', data)` কল করা।
- **সঠিক:** `authService.js` এ `loginUser(data)` ফাংশন বানানো এবং `LoginForm.js` থেকে সেটি কল করা।

---

## ৫. মডার্ন সিনট্যাক্স এবং স্ট্যান্ডার্ড (২০২৪-২০২৫)

আমরা **Async/Await** এবং **Arrow Functions** ব্যবহার করব। `.then().catch()` চেইন এখন পুরনো হয়ে গেছে।

**✅ সঠিক পদ্ধতি:**

```javascript
const onSubmit = async (data) => {
  try {
    await loginUser(data);
    // সফল হলে রিডাইরেক্ট বা টোস্ট মেসেজ
  } catch (error) {
    console.error("Login failed", error);
    // এরর হ্যান্ডলিং
  }
};
```

**❌ ভুল পদ্ধতি (Avoid):**

```javascript
const onSubmit = (data) => {
  loginUser(data)
    .then((res) => {
      // ...
    })
    .catch((err) => {
      // ...
    });
};
```

---

## ৬. কোড উদাহরণ (Production-Ready Code)

নিচে একটি সম্পূর্ণ **Login Form** এর উদাহরণ দেওয়া হলো যা বেস্ট প্র্যাকটিস মেনে তৈরি।

### ধাপ ১: ভ্যালিডেশন স্কিমা তৈরি (`src/schemas/authSchema.js`)

```javascript
import { z } from "zod";

export const loginSchema = z.object({
  email: z.string().email("সঠিক ইমেইল দিন"),
  password: z.string().min(6, "পাসওয়ার্ড অন্তত ৬ অক্ষরের হতে হবে"),
});
```

### ধাপ ২: লগিন ফর্ম কম্পোনেন্ট (`src/components/forms/LoginForm.js`)

```javascript
"use client"; // Next.js Client Component

import { useForm } from "react-hook-form";
import { zodResolver } from "@hookform/resolvers/zod";
import { loginSchema } from "@/schemas/authSchema";
import { useState } from "react";

export default function LoginForm() {
  const [serverError, setServerError] = useState("");

  // 1. Hook সেটআপ
  const {
    register,
    handleSubmit,
    formState: { errors, isSubmitting },
    reset,
  } = useForm({
    resolver: zodResolver(loginSchema), // Zod কানেক্ট করা হলো
    defaultValues: {
      email: "",
      password: "",
    },
  });

  // 2. সাবমিট হ্যান্ডলার
  const onSubmit = async (data) => {
    setServerError("");
    try {
      // এখানে API কল হবে (Simulated)
      console.log("Form Data:", data);
      await new Promise((resolve) => setTimeout(resolve, 2000)); // ২ সেকেন্ড অপেক্ষা

      alert("লগিন সফল হয়েছে!");
      reset(); // ফর্ম রিসেট
    } catch (error) {
      setServerError("সার্ভারে সমস্যা হয়েছে। আবার চেষ্টা করুন।");
    }
  };

  return (
    <div className="max-w-md mx-auto mt-10 p-6 bg-white rounded-lg shadow-md">
      <h2 className="text-2xl font-bold mb-6 text-gray-800">লগিন করুন</h2>

      <form onSubmit={handleSubmit(onSubmit)} className="space-y-4">
        {/* Email Field */}
        <div>
          <label className="block text-sm font-medium text-gray-700">
            ইমেইল
          </label>
          <input
            {...register("email")}
            type="email"
            className={`mt-1 block w-full px-3 py-2 border rounded-md shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500 ${
              errors.email ? "border-red-500" : "border-gray-300"
            }`}
            placeholder="you@example.com"
          />
          {errors.email && (
            <p className="text-red-500 text-xs mt-1">{errors.email.message}</p>
          )}
        </div>

        {/* Password Field */}
        <div>
          <label className="block text-sm font-medium text-gray-700">
            পাসওয়ার্ড
          </label>
          <input
            {...register("password")}
            type="password"
            className={`mt-1 block w-full px-3 py-2 border rounded-md shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500 ${
              errors.password ? "border-red-500" : "border-gray-300"
            }`}
          />
          {errors.password && (
            <p className="text-red-500 text-xs mt-1">
              {errors.password.message}
            </p>
          )}
        </div>

        {/* Server Error Message */}
        {serverError && (
          <div className="p-3 bg-red-100 text-red-700 rounded text-sm">
            {serverError}
          </div>
        )}

        {/* Submit Button */}
        <button
          type="submit"
          disabled={isSubmitting}
          className="w-full flex justify-center py-2 px-4 border border-transparent rounded-md shadow-sm text-sm font-medium text-white bg-blue-600 hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500 disabled:bg-blue-300"
        >
          {isSubmitting ? "লোড হচ্ছে..." : "লগিন"}
        </button>
      </form>
    </div>
  );
}
```

---

## ৭. বেস্ট প্র্যাকটিস এবং অ্যান্টি-প্যাটার্ন

**✅ DO (যা করবেন):**

- **Zod ব্যবহার করুন:** ম্যানুয়াল ভ্যালিডেশনের চেয়ে স্কিমা ভ্যালিডেশন অনেক ক্লিন।
- **`isSubmitting` ব্যবহার করুন:** সাবমিট বাটনে লোডিং স্টেট দেখান যাতে ইউজার একাধিকবার ক্লিক না করে।
- **Reusable Components:** ইনপুট ফিল্ডগুলো আলাদা কম্পোনেন্ট বানিয়ে `React.forwardRef` দিয়ে ব্যবহার করুন (যদি প্রজেক্ট বড় হয়)।

**❌ DON'T (যা করবেন না):**

- **`watch` অতিরিক্ত ব্যবহার:** `watch` পুরো কম্পোনেন্ট রি-রেন্ডার করতে পারে। দরকার ছাড়া ব্যবহার করবেন না।
- **Inline Validation:** JSX এর ভেতর জটিল ভ্যালিডেশন লজিক লিখবেন না, স্কিমা ব্যবহার করুন।
- **Form State in Redux/Context:** ফর্মের লোকাল স্টেট গ্লোবাল স্টোরে (Redux/Zustand) রাখার দরকার নেই, যদি না মাল্টি-স্টেপ ফর্ম হয়।

---

## ৮. ইন্টিগ্রেশন গাইড

**Next.js & Server Actions:**
Next.js এর Server Actions এর সাথে RHF খুব ভালো কাজ করে। তবে ক্লায়েন্ট সাইড ভ্যালিডেশন (RHF) এবং সার্ভার সাইড ভ্যালিডেশন (Zod) দুটোই রাখা উচিত সিকিউরিটির জন্য।

**TanStack Query (React Query):**
ফর্ম সাবমিশনের জন্য `useMutation` ব্যবহার করা বেস্ট প্র্যাকটিস।

**উদাহরণ (Hooks ফোল্ডারে):**

```javascript
// src/hooks/useLogin.js
import { useMutation } from "@tanstack/react-query";
import { loginUser } from "@/services/authService";

export const useLogin = () => {
  return useMutation({
    mutationFn: loginUser,
    onSuccess: (data) => {
      console.log("Login success", data);
    },
  });
};
```

---

## ৯. পারফরম্যান্স এবং অপ্টিমাইজেশন

১. **Re-render কমানো:** `formState` থেকে শুধু যা দরকার তা destructure করুন। যেমন: `const { errors } = formState;`। আপনি যদি পুরো `formState` কনসোলে প্রিন্ট করেন, তবে প্রতিটি পরিবর্তনে রেন্ডার হবে।
২. **Debounce:** ইউজার টাইপ করার সাথে সাথে যদি API কল করতে হয় (যেমন: ইউজারনেম অ্যাভেইলেবল কিনা চেক করা), তবে `debounce` ব্যবহার করুন।

---

## ১০. ইন্টারভিউ প্রস্তুতি (Interview-Ready)

**প্রশ্ন ১: RHF এবং সাধারণ `useState` ফর্মের মধ্যে পার্থক্য কী?**
_উত্তর:_ RHF আনকন্ট্রোল্ড কম্পোনেন্ট (ref) ব্যবহার করে, তাই ইনপুট টাইপ করার সময় পুরো ফর্ম রি-রেন্ডার হয় না। `useState` এ প্রতিটি কি-স্ট্রোক এ স্টেট আপডেট হয় ও রেন্ডার হয়। RHF পারফরম্যান্সে অনেক এগিয়ে।

**প্রশ্ন ২: `register` ফাংশন কী কাজ করে?**
_উত্তর:_ এটি ইনপুট এলিমেন্টের `onChange`, `onBlur`, `name`, এবং `ref` ইভেন্টগুলোকে হুক আপ করে RHF এর সাথে কানেক্ট করে।

**প্রশ্ন ৩: `Controller` কেন ব্যবহার করা হয়?**
_উত্তর:_ যেসব কম্পোনেন্ট সরাসরি `ref` সাপোর্ট করে না (যেমন React Select, Material UI), সেগুলোকে RHF এর সাথে ইন্টিগ্রেট করতে `Controller` র‍্যাপার ব্যবহার করা হয়।

---

## ১১. সমস্যা সমাধান (Gotchas & Troubleshooting)

- **সমস্যা:** ইনপুট ভ্যালু কাজ করছে না বা সাবমিট হচ্ছে না।
  - **সমাধান:** চেক করুন ইনপুটে `register("name")` ঠিকমতো দিয়েছেন কিনা। প্রতিটি ইনপুটের ইউনিক `name` থাকতে হবে।
- **সমস্যা:** ডিফল্ট ভ্যালু আসছে না।
  - **সমাধান:** `useForm` এর `defaultValues` অবজেক্টে ইনিশিয়াল ডেটা পাস করুন। `useEffect` দিয়ে ভ্যালু সেট করতে চাইলে `reset(newData)` ব্যবহার করুন।

---

## ১২. রিয়েল প্রজেক্ট চেকলিস্ট

নতুন প্রজেক্টে RHF ইমপ্লিমেন্ট করার ধাপ:

1. [ ] `npm install react-hook-form zod @hookform/resolvers` ইন্সটল করুন।
2. [ ] `/src/schemas` ফোল্ডারে Zod স্কিমা তৈরি করুন।
3. [ ] `/src/components/forms` এ ফর্ম কম্পোনেন্ট তৈরি করুন।
4. [ ] `useForm` হুক কল করুন এবং `resolver` সেট করুন।
5. [ ] ইনপুট ফিল্ডে `register` যুক্ত করুন।
6. [ ] এরর মেসেজ দেখানোর ব্যবস্থা করুন।
7. [ ] `onSubmit` ফাংশনে API কল ইন্টিগ্রেট করুন (try/catch সহ)।
8. [ ] লোডিং স্টেট (`isSubmitting`) হ্যান্ডেল করুন।

---

## ১৩. অ্যাডভান্সড টপিকস (Advanced Topics)

যদিও জুনিয়র হিসেবে এগুলো সবসময় লাগবে না, তবে জেনে রাখা ভালো।

### ১. ডায়নামিক ফিল্ডস (`useFieldArray`)

যখন ইউজারকে একাধিক একই ধরনের তথ্য দিতে হয় (যেমন: একাধিক ফোন নম্বর বা শিক্ষার তথ্য), তখন `useFieldArray` ব্যবহার করা হয়।

**কোড উদাহরণ:**

```javascript
import { useForm, useFieldArray } from "react-hook-form";

function EducationForm() {
  const { register, control, handleSubmit } = useForm({
    defaultValues: {
      education: [{ school: "", degree: "" }], // ডিফল্ট ১টি ফিল্ড
    },
  });

  const { fields, append, remove } = useFieldArray({
    control,
    name: "education",
  });

  return (
    <form onSubmit={handleSubmit((data) => console.log(data))}>
      {fields.map((field, index) => (
        <div key={field.id} className="flex gap-2 mb-2">
          <input
            {...register(`education.${index}.school`)}
            placeholder="School Name"
            className="border p-2"
          />
          <input
            {...register(`education.${index}.degree`)}
            placeholder="Degree"
            className="border p-2"
          />
          <button
            type="button"
            onClick={() => remove(index)}
            className="text-red-500"
          >
            Delete
          </button>
        </div>
      ))}

      <button
        type="button"
        onClick={() => append({ school: "", degree: "" })}
        className="bg-blue-500 text-white p-2 rounded"
      >
        Add Education
      </button>

      <button
        type="submit"
        className="bg-green-500 text-white p-2 rounded ml-2"
      >
        Submit
      </button>
    </form>
  );
}
```

### ২. ডিপেন্ডেন্ট ফিল্ডস (Dependent Fields)

যখন একটি ফিল্ডের ভ্যালু অন্য ফিল্ডের উপর নির্ভর করে। যেমন: "Country" সিলেক্ট করলে "City" চেঞ্জ হবে। এর জন্য `watch` ব্যবহার করা হয়।

```javascript
const { watch, register } = useForm();
const selectedCountry = watch("country"); // লাইভ ভ্যালু দেখা

// JSX এর মধ্যে:
<select {...register("country")}>
  <option value="BD">Bangladesh</option>
  <option value="US">USA</option>
</select>;

{
  selectedCountry === "BD" && (
    <select {...register("city")}>
      <option value="Dhaka">Dhaka</option>
      <option value="Chittagong">Chittagong</option>
    </select>
  );
}
```

### ৩. মাল্টি-স্টেপ ফর্ম (Multi-step Forms)

বড় ফর্মকে ছোট ছোট ধাপে ভাগ করা। এখানে চ্যালেঞ্জ হলো এক ধাপ থেকে অন্য ধাপে গেলে ডেটা হারিয়ে না যাওয়া।

- **সহজ সমাধান:** পুরো ফর্মটি একটি প্যারেন্ট কম্পোনেন্টে রাখুন এবং CSS দিয়ে স্টেপগুলো হাইড/শো করুন।
- **প্রফেশনাল সমাধান:** Zustand বা Context API ব্যবহার করে ফর্মের ডেটা গ্লোবাল স্টেটে সেভ রাখুন, যাতে পেজ রিফ্রেশ বা কম্পোনেন্ট আনমাউন্ট হলেও ডেটা থাকে।

---

## ১৪. পরবর্তী ধাপ (Next Steps)

**মিনি প্রজেক্ট আইডিয়া:**
একটি **"Job Application Form"** তৈরি করুন যেখানে:

- নাম, ইমেইল, ফোন নম্বর থাকবে।
- সিভি আপলোড অপশন থাকবে (ফাইল ভ্যালিডেশন সহ)।
- "Experience" সেকশন থাকবে যেখানে ইউজার ডায়নামিকালি একাধিক জবের তথ্য যোগ করতে পারবে (`useFieldArray` ব্যবহার করে)।

**রিসোর্স:**

- অফিসিয়াল ডকুমেন্টেশন: [react-hook-form.com](https://react-hook-form.com/)
- Zod ডকুমেন্টেশন: [zod.dev](https://zod.dev/)

---

_শুভকামনা! এই গাইডটি ফলো করে প্র্যাকটিস শুরু করুন, আপনি দ্রুতই রিমোট জবের জন্য তৈরি হয়ে যাবেন।_
