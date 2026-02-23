# React Hook Form Mastery Guide (2024-2025) 🚀

এই গাইডটি আপনাকে **React Hook Form (RHF)** এর একদম বেসিক থেকে শুরু করে অ্যাডভান্সড লেভেল পর্যন্ত নিয়ে যাবে। এটি বিশেষভাবে তৈরি করা হয়েছে যারা ইউরোপ বা আমেরিকার রিমোট জুনিয়র ফ্রন্টএন্ড ডেভেলপার পজিশনের জন্য প্রস্তুতি নিচ্ছেন। আমরা ফোকাস করব মডার্ন প্যাটার্ন, **Zod** ভ্যালিডেশন, **TypeScript**, এবং **Next.js App Router** ইন্টিগ্রেশনের উপর।

---

## ১. React Hook Form কি এবং কেন? (What & Why)

### React Hook Form কি?

React Hook Form হলো React-এর জন্য একটি লাইটওয়েট লাইব্রেরি যা ফর্ম হ্যান্ডলিং সহজ, পারফরম্যান্ট এবং ফ্লেক্সিবল করে তোলে। এটি মূলত **Uncontrolled Components** এবং **Hooks** এর উপর ভিত্তি করে তৈরি।

### কেন RHF ব্যবহার করবেন? (RHF vs Native/Formik)

1.  **পারফরম্যান্স (Performance):** RHF ইনপুট ভ্যালু ট্র্যাক করার জন্য `ref` ব্যবহার করে, যার ফলে টাইপ করার সময় পুরো ফর্ম রি-রেন্ডার হয় না। এটি বড় ফর্মের জন্য অত্যন্ত দ্রুত।
2.  **কম কোড (Less Code):** সাধারণ `useState` বা অন্যান্য লাইব্রেরির তুলনায় অনেক কম কোড লিখতে হয়।
3.  **বিল্ট-ইন ভ্যালিডেশন:** সহজেই ভ্যালিডেশন রুলস সেট করা যায়।
4.  **জনপ্রিয়তা:** বর্তমানে এটি Formik বা Redux Form-এর চেয়ে বেশি জনপ্রিয় এবং মডার্ন প্রজেক্টে স্ট্যান্ডার্ড হিসেবে ব্যবহৃত হয়।

### কখন ব্যবহার করবেন?

- যখন আপনার ফর্মে অনেকগুলো ফিল্ড থাকে।
- যখন পারফরম্যান্স ক্রিটিকাল।
- যখন আপনি জটিল ভ্যালিডেশন (যেমন Zod) ব্যবহার করতে চান।
- সাধারণ `useState` দিয়ে ফর্ম হ্যান্ডল করা যখন জটিল হয়ে যায়।

---

## ২. কোর কনসেপ্টস (Core Concepts)

- **Uncontrolled Components:** RHF মূলত DOM `ref` ব্যবহার করে ইনপুট ভ্যালু ম্যানেজ করে, যা React-এর ভার্চুয়াল DOM রি-রেন্ডার কমায়।
- **Register:** ইনপুট ফিল্ডকে হুকের সাথে কানেক্ট করার পদ্ধতি।
- **HandleSubmit:** ফর্ম সাবমিশন হ্যান্ডল করার ফাংশন যা ভ্যালিডেশন চেক করে ডেটা পাস করে।
- **FormState:** ফর্মের অবস্থা (errors, isSubmitting, isDirty) ট্র্যাক করার অবজেক্ট।

---

## ৩. সেটআপ এবং ইনস্টলেশন (Setup & Installation)

প্রথমে আপনার প্রজেক্টে প্যাকেজগুলো ইনস্টল করুন। আমরা ভ্যালিডেশনের জন্য **Zod** ব্যবহার করব যা বর্তমান ইন্ডাস্ট্রি স্ট্যান্ডার্ড।

```bash
npm install react-hook-form zod @hookform/resolvers
```

**TypeScript কনফিগারেশন (tsconfig.json):**
নিশ্চিত করুন `strict: true` সেট করা আছে যাতে টাইপ সেফটি ঠিক থাকে।

---

## ৪. বেসিক ব্যবহার (Basic Usage Pattern)

সবচেয়ে সহজ উদাহরণ দিয়ে শুরু করা যাক।

```tsx
import { useForm, SubmitHandler } from "react-hook-form";

type Inputs = {
  example: string;
  exampleRequired: string;
};

export default function App() {
  const {
    register,
    handleSubmit,
    watch,
    formState: { errors },
  } = useForm<Inputs>();

  const onSubmit: SubmitHandler<Inputs> = (data) => console.log(data);

  console.log(watch("example")); // ইনপুট ভ্যালু ওয়াচ করা

  return (
    /* "handleSubmit" ভ্যালিডেশন চেক করে onSubmit কল করবে */
    <form onSubmit={handleSubmit(onSubmit)}>
      {/* ইনপুট রেজিস্টার করা */}
      <input defaultValue="test" {...register("example")} />

      {/* ভ্যালিডেশন রুলস সহ রেজিস্টার */}
      <input {...register("exampleRequired", { required: true })} />
      {/* এরর দেখানো */}
      {errors.exampleRequired && <span>This field is required</span>}

      <input type="submit" />
    </form>
  );
}
```

---

## ৫. ফর্ম রেজিস্ট্রেশন (Form Registration)

`register` ফাংশনটি ইনপুট ফিল্ডকে RHF এর সাথে যুক্ত করে। এটি `onChange`, `onBlur`, `name`, এবং `ref` প্রপার্টিগুলো রিটার্ন করে যা আমরা স্প্রেড অপারেটর (`...`) দিয়ে ইনপুটে পাস করি।

```tsx
<input {...register("firstName")} />
```

### বিল্ট-ইন ভ্যালিডেশন রুলস:

```tsx
<input
  {...register("age", {
    required: "Age is required",
    min: { value: 18, message: "Must be 18+" },
    max: 99,
    pattern: {
      value: /^[0-9]+$/,
      message: "Please enter a number",
    },
  })}
/>
```

---

## ৬. ভ্যালিডেশন (Validation) - Zod (RECOMMENDED) ✅

যদিও RHF-এর বিল্ট-ইন ভ্যালিডেশন আছে, কিন্তু প্রফেশনাল প্রজেক্টে **Zod** ব্যবহার করা হয় কারণ এটি টাইপসেফ এবং স্কিমা রিইউজ করা যায়।

### Zod স্কিমা তৈরি:

```tsx
import { z } from "zod";

const signUpSchema = z.object({
  email: z.string().email("Invalid email address"),
  password: z.string().min(8, "Password must be at least 8 characters"),
  age: z.number().min(18, "You must be at least 18"),
});

// টাইপ ইনফারেন্স (Type Inference)
type SignUpFormValues = z.infer<typeof signUpSchema>;
```

### RHF এর সাথে Zod ব্যবহার:

```tsx
import { useForm } from "react-hook-form";
import { zodResolver } from "@hookform/resolvers/zod";

const App = () => {
  const {
    register,
    handleSubmit,
    formState: { errors },
  } = useForm<SignUpFormValues>({
    resolver: zodResolver(signUpSchema), // Zod Resolver কানেক্ট করা
  });

  const onSubmit = (data: SignUpFormValues) => {
    console.log(data);
  };

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <input {...register("email")} placeholder="Email" />
      {errors.email && <p>{errors.email.message}</p>}

      <input type="password" {...register("password")} placeholder="Password" />
      {errors.password && <p>{errors.password.message}</p>}

      <button type="submit">Sign Up</button>
    </form>
  );
};
```

---

## ৭. এরর হ্যান্ডলিং (Error Handling)

`formState.errors` অবজেক্টে সব ভ্যালিডেশন এরর থাকে।

```tsx
// ফিল্ড লেভেল এরর
{
  errors.firstName && (
    <span className="text-red-500">{errors.firstName.message}</span>
  );
}

// এরর মেসেজ স্টাইলিং (Tailwind CSS)
<input
  {...register("email")}
  className={`border p-2 ${
    errors.email ? "border-red-500" : "border-gray-300"
  }`}
/>;
```

---

## ৮. ফর্ম স্টেট ম্যানেজমেন্ট (Form State)

`formState` এর গুরুত্বপূর্ণ প্রপার্টিসমূহ:

- `isSubmitting`: ফর্ম সাবমিট হচ্ছে কিনা (লোডিং স্টেট দেখানোর জন্য)।
- `isDirty`: ইউজার ফর্মে কোনো পরিবর্তন করেছে কিনা।
- `isValid`: ফর্মটি ভ্যালিড কিনা।
- `dirtyFields`: কোন কোন ফিল্ড মডিফাই করা হয়েছে।

```tsx
const {
  formState: { isSubmitting, isValid },
} = useForm();

<button disabled={isSubmitting || !isValid}>
  {isSubmitting ? "Loading..." : "Submit"}
</button>;
```

---

## ৯. ইনপুট টাইপস ও প্যাটার্নস (Input Types)

### Text, Email, Password

```tsx
<input type="text" {...register("username")} />
<input type="email" {...register("email")} />
<input type="password" {...register("password")} />
```

### Checkbox

```tsx
<label>
  <input type="checkbox" {...register("terms")} />
  Accept Terms
</label>
```

### Radio Buttons

```tsx
<label><input type="radio" value="male" {...register("gender")} /> Male</label>
<label><input type="radio" value="female" {...register("gender")} /> Female</label>
```

### Select Dropdown

````tsx
<select {...register("category")}>
  <option value="">Select...</option>
  <option value="A">Category A</option>
  <option value="B">Category B</option>
</select>

### File Upload
```tsx
<input type="file" {...register("picture")} />
````

````

---

## ১০. অ্যাডভান্সড ফিচারস (Advanced Features)

### watch()

লাইভ ইনপুট ভ্যালু দেখার জন্য।

```tsx
const watchShowAge = watch("showAge");
// ...
{
  watchShowAge && <input type="number" {...register("age")} />;
}
````

### setValue()

প্রোগ্রামেটিক্যালি ভ্যালু সেট করার জন্য।

```tsx
setValue("firstName", "Omar", { shouldValidate: true });
```

### reset()

ফর্ম রিসেট করার জন্য।

```tsx
reset(); // সব ক্লিয়ার
reset({ firstName: "New Value" }); // নতুন ভ্যালু দিয়ে রিসেট
```

---

## ১১. কন্ট্রোলার কম্পোনেন্ট (Controller)

যখন আপনি **Material-UI**, **Ant Design**, বা **React Select** এর মতো থার্ড-পার্টি লাইব্রেরি ব্যবহার করবেন, তখন `Controller` ব্যবহার করতে হবে কারণ এগুলো সাধারণ `ref` সাপোর্ট করে না।

```tsx
import { Controller } from "react-hook-form";
import Select from "react-select";

<Controller
  name="city"
  control={control}
  render={({ field }) => <Select {...field} options={options} />}
/>;
```

---

## ১২. ডিফল্ট ভ্যালু (Default Values)

API থেকে ডেটা এনে ফর্ম প্রি-ফিল করার জন্য `defaultValues` ব্যবহার করুন।

```tsx
useForm({
  defaultValues: {
    firstName: "John",
    email: "john@example.com",
  },
});

// অথবা API কল এর পর reset ব্যবহার করুন
useEffect(() => {
  fetchData().then((data) => reset(data));
}, [reset]);
```

---

## ১৩. TypeScript ইন্টিগ্রেশন (TypeScript Integration)

সবসময় টাইপ ব্যবহার করবেন।

```tsx
type FormData = {
  firstName: string;
  age: number;
};

const { register } = useForm<FormData>();
```

Zod এর সাথে টাইপ ইনফারেন্স করলে আলাদা করে ইন্টারফেস লিখতে হয় না।

---

## ১৪. Zod ভ্যালিডেশন প্যাটার্নস (Critical Patterns)

```tsx
const schema = z
  .object({
    // সাধারণ স্ট্রিং
    username: z.string().min(3),

    // ইমেইল
    email: z.string().email(),

    // নাম্বার (স্ট্রিং থেকে নাম্বার কনভার্শন সহ)
    age: z.coerce.number().min(18),

    // অপশনাল ফিল্ড
    bio: z.string().optional(),

    // পাসওয়ার্ড কনফার্মেশন (Refine)
    password: z.string().min(6),
    confirmPassword: z.string().min(6),
  })
  .refine((data) => data.password === data.confirmPassword, {
    message: "Passwords don't match",
    path: ["confirmPassword"],
  });
```

---

## ১৫. React Hook Form + Next.js App Router

Next.js এ দুইভাবে ফর্ম হ্যান্ডল করা যায়:

### ১. Client Component (Standard)

```tsx
"use client";
import { useForm } from "react-hook-form";

export default function ContactForm() {
  const { register, handleSubmit } = useForm();

  const onSubmit = async (data) => {
    await fetch("/api/contact", { method: "POST", body: JSON.stringify(data) });
  };
  // ...
}
```

### ২. Server Actions (Modern)

Server Actions এর সাথে RHF ইন্টিগ্রেট করা একটু ট্রিকি কিন্তু পাওয়ারফুল।

```tsx
// actions.ts
"use server";
export async function createPost(data: any) {
  const parsed = schema.safeParse(data);
  if (!parsed.success) {
    return { success: false, errors: parsed.error.flatten().fieldErrors };
  }
  // Save to DB...
  return { success: true };
}

// FormComponent.tsx
("use client");
const { setError } = useForm();

const onSubmit = async (data: FormValues) => {
  const result = await createPost(data);
  if (!result.success && result.errors) {
    // সার্ভার সাইড এরর ফিল্ডে সেট করা
    Object.entries(result.errors).forEach(([key, value]) => {
      setError(key as keyof FormValues, {
        type: "server",
        message: value[0],
      });
    });
  }
};
```

---

## ১৬. প্রফেশনাল ফর্ম স্ট্রাকচার (Professional Structure)

একটি বড় প্রজেক্টে ফাইলগুলো এভাবে সাজাবেন:

```
/components
  /ui
    Input.tsx (Reusable RHF Input)
    Button.tsx
  /forms
    LoginForm.tsx
    RegisterForm.tsx
/lib
  /validations
    auth.ts (Zod schemas)
```

---

## ১৭. রিইউজেবল ফর্ম কম্পোনেন্ট (Reusable Components)

বারবার `input` ট্যাগ না লিখে একটি রিইউজেবল কম্পোনেন্ট তৈরি করুন।

```tsx
// components/ui/Input.tsx
import { forwardRef } from "react";

type InputProps = React.InputHTMLAttributes<HTMLInputElement> & {
  label: string;
  error?: string;
};

const Input = forwardRef<HTMLInputElement, InputProps>(
  ({ label, error, ...props }, ref) => {
    return (
      <div className="flex flex-col gap-1">
        <label className="text-sm font-medium">{label}</label>
        <input
          ref={ref}
          className={`border rounded p-2 ${
            error ? "border-red-500" : "border-gray-300"
          }`}
          {...props}
        />
        {error && <span className="text-red-500 text-xs">{error}</span>}
      </div>
    );
  }
);

Input.displayName = "Input";
export default Input;
```

ব্যবহার:

```tsx
<Input label="Email" error={errors.email?.message} {...register("email")} />
```

---

## ১৮. ফর্ম সাবমিশন প্যাটার্নস (Submission Patterns)

**Optimistic Updates:** ইউজারকে সাথে সাথে ফিডব্যাক দিন, ব্যাকগ্রাউন্ডে রিকোয়েস্ট চলুক।
**Loading State:** `isSubmitting` ব্যবহার করে বাটন ডিজেবল রাখুন।
**Toast Notification:** সফল হলে `react-hot-toast` বা `sonner` দিয়ে মেসেজ দেখান।

---

## ১৯. জটিল ফর্ম (Complex Forms) - useFieldArray

ডায়নামিক ফিল্ড (যেমন: একাধিক ফোন নাম্বার যোগ করা) এর জন্য `useFieldArray` ব্যবহার করুন।

```tsx
const { control, register } = useForm();
const { fields, append, remove } = useFieldArray({
  control,
  name: "phones",
});

return (
  <ul>
    {fields.map((item, index) => (
      <li key={item.id}>
        <input {...register(`phones.${index}.number`)} />
        <button type="button" onClick={() => remove(index)}>
          Delete
        </button>
      </li>
    ))}
    <button type="button" onClick={() => append({ number: "" })}>
      Add Phone
    </button>
  </ul>
);
```

---

### Multi-Step Form (Wizard)

মাল্টি-স্টেপ ফর্মের জন্য `trigger` ফাংশন ব্যবহার করে বর্তমান স্টেপ ভ্যালিডেট করুন।

```tsx
const { trigger } = useForm();
const [step, setStep] = useState(0);

const nextStep = async () => {
  const fieldsToValidate =
    step === 0 ? ["firstName", "lastName"] : ["email", "phone"];
  const isStepValid = await trigger(fieldsToValidate);
  if (isStepValid) setStep((prev) => prev + 1);
};
```

---

## ২০. পারফরম্যান্স অপ্টিমাইজেশন (Performance)

- **useWatch:** পুরো ফর্ম রি-রেন্ডার না করে নির্দিষ্ট ফিল্ডের ভ্যালু ট্র্যাক করতে `useWatch` ব্যবহার করুন।
- **Memoization:** বড় ফর্মের ক্ষেত্রে চাইল্ড কম্পোনেন্টগুলো `React.memo` দিয়ে র‌্যাপ করুন।

---

## ২১. অ্যাক্সেসিবিলিটি (Accessibility - A11y)

- সব ইনপুটের সাথে `label` ব্যবহার করুন (`htmlFor` দিয়ে কানেক্ট করুন)।
- এরর মেসেজের জন্য `aria-invalid` এবং `aria-describedby` ব্যবহার করুন।

```tsx
<input
  id="email"
  aria-invalid={errors.email ? "true" : "false"}
  aria-describedby="email-error"
  {...register("email")}
/>;
{
  errors.email && <span id="email-error">{errors.email.message}</span>;
}
```

---

## ২২. এরর UX প্যাটার্নস (Error UX)

- **Inline Errors:** ইনপুটের ঠিক নিচে লাল রঙের টেক্সট।
- **Focus on Error:** সাবমিট করার পর প্রথম এরর ফিল্ডে অটো ফোকাস (RHF ডিফল্টভাবে এটি করে)।
- **Disabled Button:** ফর্ম ভ্যালিড না হওয়া পর্যন্ত সাবমিট বাটন ডিজেবল রাখা (অপশনাল, তবে অনেক সময় ভালো UX)।

---

## ২৩. কমন প্যাটার্নস ও উদাহরণ (Common Patterns)

### Login Form Example

```tsx
const LoginForm = () => {
  const {
    register,
    handleSubmit,
    formState: { isSubmitting },
  } = useForm();

  const onSubmit = async (data) => {
    // login logic
  };

  return (
    <form onSubmit={handleSubmit(onSubmit)} className="space-y-4">
      <Input label="Email" type="email" {...register("email")} />
      <Input label="Password" type="password" {...register("password")} />
      <button disabled={isSubmitting} type="submit">
        {isSubmitting ? "Logging in..." : "Login"}
      </button>
    </form>
  );
};
```

---

## ২৪. UI লাইব্রেরি ইন্টিগ্রেশন (UI Libraries)

**shadcn/ui** বর্তমানে সবচেয়ে জনপ্রিয়। এটি RHF এবং Zod এর সাথে চমৎকারভাবে কাজ করে। shadcn এর `Form` কম্পোনেন্ট RHF এর `FormProvider` ব্যবহার করে।

---

## ২৫. মডার্ন প্যাটার্নস (2024-2025)

✅ **DO:** Zod ব্যবহার করুন।
✅ **DO:** Server Actions ব্যবহার করুন (Next.js)।
✅ **DO:** টাইপস্ক্রিপ্ট ব্যবহার করুন।
❌ **DON'T:** ম্যানুয়ালি `onChange` হ্যান্ডলার লিখবেন না (যদি না খুব প্রয়োজন হয়)।
❌ **DON'T:** শুধুমাত্র ক্লায়েন্ট সাইড ভ্যালিডেশনের উপর নির্ভর করবেন না।

---

## ২৬. টেস্টিং (Testing)

**React Testing Library** দিয়ে ফর্ম টেস্ট করা সহজ।

```tsx
import { render, screen, waitFor } from "@testing-library/react";
import userEvent from "@testing-library/user-event";
import LoginForm from "./LoginForm";

test("submits form with valid data", async () => {
  const mockSubmit = jest.fn();
  render(<LoginForm onSubmit={mockSubmit} />);

  // ইউজার ইন্টারঅ্যাকশন
  await userEvent.type(screen.getByLabelText(/email/i), "test@example.com");
  await userEvent.type(screen.getByLabelText(/password/i), "password123");
  await userEvent.click(screen.getByRole("button", { name: /login/i }));

  // সাবমিশন চেক করা
  await waitFor(() => {
    expect(mockSubmit).toHaveBeenCalledWith({
      email: "test@example.com",
      password: "password123",
    });
  });
});
```

---

## ২৭. কমন মিসটেকস (Common Mistakes)

1.  **Spread মিস করা:** `...register("name")` না দিলে কাজ করবে না।
2.  **নামের বানান ভুল:** `register` এর নাম এবং স্কিমার নাম মিল থাকতে হবে।
3.  **useEffect এর অপব্যবহার:** ফর্ম ভ্যালু ট্র্যাক করতে `useEffect` এর বদলে `watch` ব্যবহার করুন।

---

## ২৮. ডিবাগিং ও DevTools (Debugging)

RHF এর নিজস্ব DevTools আছে যা ডেভেলপমেন্টের সময় ফর্ম স্টেট ভিজ্যুয়ালাইজ করতে সাহায্য করে।

```bash
npm install -D @hookform/devtools
```

```tsx
import { DevTool } from "@hookform/devtools";

export default function App() {
  const { control } = useForm();

  return (
    <>
      <form>...</form>
      <DevTool control={control} /> {/* শুধুমাত্র ডেভেলপমেন্ট মোডে কাজ করবে */}
    </>
  );
}
```

---

## ২৯. রিয়েল ওয়ার্ল্ড উদাহরণ (Real-World Example)

একটি সম্পূর্ণ **Product Create Form** (Next.js + Zod + Server Action):

```tsx
"use client";

import { useForm } from "react-hook-form";
import { zodResolver } from "@hookform/resolvers/zod";
import { z } from "zod";
import { createProduct } from "@/app/actions"; // Server Action

const productSchema = z.object({
  name: z.string().min(3),
  price: z.coerce.number().positive(),
  description: z.string().optional(),
});

type ProductFormValues = z.infer<typeof productSchema>;

export default function ProductForm() {
  const {
    register,
    handleSubmit,
    formState: { errors, isSubmitting },
    reset,
  } = useForm<ProductFormValues>({
    resolver: zodResolver(productSchema),
  });

  const onSubmit = async (data: ProductFormValues) => {
    const result = await createProduct(data);
    if (result.success) {
      alert("Product created!");
      reset();
    } else {
      alert("Error creating product");
    }
  };

  return (
    <form
      onSubmit={handleSubmit(onSubmit)}
      className="flex flex-col gap-4 max-w-md mx-auto p-4 border rounded"
    >
      <div>
        <label>Name</label>
        <input {...register("name")} className="border p-2 w-full" />
        {errors.name && <p className="text-red-500">{errors.name.message}</p>}
      </div>

      <div>
        <label>Price</label>
        <input
          type="number"
          step="0.01"
          {...register("price")}
          className="border p-2 w-full"
        />
        {errors.price && <p className="text-red-500">{errors.price.message}</p>}
      </div>

      <button
        disabled={isSubmitting}
        className="bg-blue-500 text-white p-2 rounded"
      >
        {isSubmitting ? "Saving..." : "Create Product"}
      </button>
    </form>
  );
}
```

---

## ৩০. ইন্টারভিউ প্রস্তুতি (Interview Prep)

**Q: Controlled vs Uncontrolled Components এর পার্থক্য কি?**
A: Controlled কম্পোনেন্টে React state (`useState`) সোর্স অফ ট্রুথ হিসেবে কাজ করে। Uncontrolled কম্পোনেন্টে DOM নিজেই সোর্স অফ ট্রুথ (ref দিয়ে অ্যাক্সেস করা হয়)। RHF পারফরম্যান্সের জন্য Uncontrolled অ্যাপ্রোচ ব্যবহার করে।

**Q: `register` ফাংশন কি করে?**
A: এটি ইনপুট এলিমেন্টকে হুকের সাথে রেজিস্টার করে এবং ইভেন্ট হ্যান্ডলার (onChange, onBlur) ও ref ইনজেক্ট করে।

---

## ৩১. বেস্ট প্র্যাকটিস চেকলিস্ট (Best Practices Checklist)

- [ ] সব ফর্মে **Zod** স্কিমা ব্যবহার করা হয়েছে।
- [ ] **TypeScript** টাইপ সঠিকভাবে ডিফাইন করা হয়েছে।
- [ ] **Accessibility** (Labels, ARIA) নিশ্চিত করা হয়েছে।
- [ ] **Loading State** হ্যান্ডল করা হয়েছে (ডাবল সাবমিশন রোধ করতে)।
- [ ] ফর্ম সাবমিশনের পর **Reset** বা ফিডব্যাক দেওয়া হয়েছে।
- [ ] **Reusable Components** ব্যবহার করা হয়েছে কোড ডুপ্লিকেশন কমাতে।

---

### শেষ কথা

React Hook Form শেখা আপনার ক্যারিয়ারের জন্য একটি গেম-চেঞ্জার হতে পারে। এটি শুধুমাত্র আপনার কোডকে পরিষ্কার করে না, বরং অ্যাপ্লিকেশনের পারফরম্যান্সও উল্লেখযোগ্যভাবে বাড়ায়। উপরের গাইডটি অনুসরণ করে ছোট ছোট প্রজেক্ট তৈরি করুন, তাহলেই আপনি প্রোডাকশন-রেডি ফর্ম তৈরিতে দক্ষ হয়ে উঠবেন। শুভকামনা! 🎉
