# Frontend Testing Mastery Guide (Bangla) 🧪

"It works on my machine" - এই কথাটি রিমোট জবে চলবে না। আপনার কোড যে প্রোডাকশনে গিয়ে ফাটবে না, তার গ্যারান্টি হলো **Testing**। ইউরোপ/আমেরিকার কোম্পানিগুলো টেস্টিং ছাড়া কোনো কোড মার্জ করে না।

---

## ১. টেস্টিং কেন শিখব? (Why Testing?)

1.  **Confidence:** কোড চেঞ্জ করলে পুরনো ফিচার ভাঙল কিনা তা ম্যানুয়ালি চেক করতে হয় না।
2.  **Refactoring:** নির্ভয়ে কোড রিফ্যাক্টর করা যায়।
3.  **Documentation:** টেস্ট কেসগুলোই আপনার কোডের ডকুমেন্টেশন হিসেবে কাজ করে।
4.  **Job Requirement:** জুনিয়র হিসেবে টেস্টিং জানা আপনাকে অন্যদের চেয়ে ১০ গুণ এগিয়ে রাখবে।

---

## ২. টেস্টিং পিরামিড (Testing Pyramid)

আমরা মূলত ৩ ধরণের টেস্ট করি:

1.  **Unit Testing:** ছোট ছোট ফাংশন বা লজিক টেস্ট করা (যেমন: `add(2, 3)` ফাংশন ৫ রিটার্ন করে কিনা)।
2.  **Integration/Component Testing:** কম্পোনেন্টগুলো ঠিকমতো রেন্ডার হচ্ছে কিনা এবং ইন্টারেকশন কাজ করছে কিনা (যেমন: বাটনে ক্লিক করলে ফর্ম সাবমিট হয় কিনা)।
3.  **End-to-End (E2E) Testing:** পুরো অ্যাপটি একজন ইউজারের মতো চালিয়ে দেখা (যেমন: লগিন করে ড্যাশবোর্ডে যাওয়া)।

---

## ৩. টুলস পরিচিতি (Tools)

- **Vitest / Jest:** টেস্ট রানার (Unit Testing এর জন্য)। বর্তমানে Vite প্রজেক্টে **Vitest** বেশি জনপ্রিয়।
- **React Testing Library (RTL):** React কম্পোনেন্ট রেন্ডার এবং ইন্টারেক্ট করার জন্য।
- **Playwright / Cypress:** E2E টেস্টিংয়ের জন্য।

---

## ৪. প্রজেক্ট সেটআপ (Vitest & RTL)

Vite প্রজেক্টে সেটআপ করা খুব সহজ।

```bash
npm install -D vitest jsdom @testing-library/react @testing-library/jest-dom @testing-library/user-event
```

`vite.config.js` এ কনফিগারেশন:

```javascript
/// <reference types="vitest" />
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";

export default defineConfig({
  plugins: [react()],
  test: {
    environment: "jsdom",
    setupFiles: "./src/setupTests.js",
    globals: true, // describe, it, expect গ্লোবালি পাওয়ার জন্য
  },
});
```

`src/setupTests.js` ফাইল:

```javascript
import "@testing-library/jest-dom";
```

---

## ৫. Unit Testing (লজিক টেস্ট করা)

ধরুন আমাদের একটি ফাংশন আছে `utils/math.js`:

```javascript
export const add = (a, b) => a + b;
```

এর টেস্ট ফাইল `utils/math.test.js`:

```javascript
import { describe, it, expect } from "vitest";
import { add } from "./math";

describe("Math Utils", () => {
  it("should add two numbers correctly", () => {
    const result = add(2, 3);
    expect(result).toBe(5);
  });

  it("should handle negative numbers", () => {
    expect(add(-2, -3)).toBe(-5);
  });
});
```

---

## ৬. Component Testing (React Testing Library)

এটিই সবচেয়ে গুরুত্বপূর্ণ পার্ট। আমরা দেখব কম্পোনেন্ট রেন্ডার হচ্ছে কিনা এবং ইউজার ইন্টারেকশন কাজ করছে কিনা।

**Example Component (`Counter.jsx`):**

```jsx
import { useState } from "react";

export default function Counter() {
  const [count, setCount] = useState(0);
  return (
    <div>
      <h1>Count: {count}</h1>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}
```

**Test File (`Counter.test.jsx`):**

```jsx
import { render, screen } from "@testing-library/react";
import userEvent from "@testing-library/user-event";
import Counter from "./Counter";

describe("Counter Component", () => {
  it("renders correctly with initial count 0", () => {
    render(<Counter />);
    // স্ক্রিনে টেক্সট আছে কিনা চেক করা
    expect(screen.getByText("Count: 0")).toBeInTheDocument();
    expect(
      screen.getByRole("button", { name: /increment/i })
    ).toBeInTheDocument();
  });

  it("increments count when button is clicked", async () => {
    const user = userEvent.setup();
    render(<Counter />);

    const button = screen.getByRole("button", { name: /increment/i });

    // বাটনে ক্লিক করা
    await user.click(button);

    // কাউন্ট আপডেট হয়েছে কিনা চেক করা
    expect(screen.getByText("Count: 1")).toBeInTheDocument();
  });
});
```

### RTL এর গোল্ডেন রুল:

টেস্ট করার সময় `data-testid` বা `class` বা `id` দিয়ে এলিমেন্ট খুঁজবেন না। ইউজার যেভাবে দেখে সেভাবে খুঁজুন:

- `getByRole` (button, heading, link) - **Best** ✅
- `getByLabelText` (form inputs)
- `getByText` (non-interactive elements)
- `getByPlaceholderText`

---

## ৭. API Mocking (MSW - Mock Service Worker)

টেস্টের সময় আমরা রিয়েল API কল করি না (স্লো এবং আনরিলায়বল)। আমরা API কল **Mock** (নকল) করি।

```jsx
// UserList.test.jsx
import { render, screen, waitFor } from "@testing-library/react";
import UserList from "./UserList";
import { vi } from "vitest";

// fetch কে মক করা (সহজ পদ্ধতি)
global.fetch = vi.fn();

function createFetchResponse(data) {
  return { json: () => new Promise((resolve) => resolve(data)) };
}

it("renders user list from api", async () => {
  const mockUsers = [{ id: 1, name: "Omar" }];
  fetch.mockResolvedValue(createFetchResponse(mockUsers));

  render(<UserList />);

  // লোডিং স্টেট চেক
  expect(screen.getByText(/loading/i)).toBeInTheDocument();

  // ডাটা আসার পর চেক (Async)
  await waitFor(() => {
    expect(screen.getByText("Omar")).toBeInTheDocument();
  });
});
```

---

## ৮. E2E Testing (Playwright) - Brief Intro

Playwright পুরো ব্রাউজার ওপেন করে টেস্ট করে।

```javascript
// tests/example.spec.js
import { test, expect } from "@playwright/test";

test("has title", async ({ page }) => {
  await page.goto("https://my-app.com");
  await expect(page).toHaveTitle(/My App/);
});

test("login flow", async ({ page }) => {
  await page.goto("https://my-app.com/login");
  await page.getByLabel("Email").fill("user@example.com");
  await page.getByLabel("Password").fill("password");
  await page.getByRole("button", { name: "Sign in" }).click();

  await expect(page).toHaveURL(/dashboard/);
});
```

---

## ৯. চেকলিস্ট (Job Ready Checklist)

- [ ] আমি `vitest` দিয়ে সাধারণ লজিক টেস্ট করতে পারি।
- [ ] আমি `React Testing Library` দিয়ে কম্পোনেন্ট রেন্ডার এবং বাটন ক্লিক টেস্ট করতে পারি।
- [ ] আমি `getByRole` এবং `getByText` এর ব্যবহার বুঝি।
- [ ] আমি `async/await` এবং `waitFor` ব্যবহার করে অ্যাসিঙ্ক্রোনাস কোড টেস্ট করতে পারি।
- [ ] আমি API কল মক (Mock) করতে পারি।

---

## ১০. রিসোর্স

- [React Testing Library Docs](https://testing-library.com/docs/react-testing-library/intro/)
- [Vitest Docs](https://vitest.dev/)

টেস্টিং শুরুতে কঠিন মনে হতে পারে, কিন্তু একবার অভ্যাস হয়ে গেলে এটি ছাড়া কোড লিখতে ভয় লাগবে! শুভকামনা। 🧪
