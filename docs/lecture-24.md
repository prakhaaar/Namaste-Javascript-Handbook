# 🎬 Episode 5 - Promise APIs + Interview Questions 🔥

---

## 🔹 Promise APIs Overview

JavaScript provides several built-in **Promise APIs** to handle multiple asynchronous operations efficiently.

---

### 1️⃣ `Promise.all()`

- Runs multiple promises **in parallel**.
- Waits until **all promises are resolved**.
- If **any promise fails**, the entire `Promise.all` **rejects immediately** (fail-fast behavior).

```js
// Create a Promise p1 that resolves after 3 seconds
const p1 = new Promise((resolve) =>
  setTimeout(() => resolve("p1 success"), 3000)
);

// Create a Promise p2 that resolves after 2 seconds
const p2 = new Promise((resolve) =>
  setTimeout(() => resolve("p2 success"), 2000)
);

// Create a Promise p3 that rejects after 1 second
const p3 = new Promise((_, reject) =>
  setTimeout(() => reject("p3 failed"), 1000)
);

// -------------------------------
// 🔹 Promise.all()
// -------------------------------
// ✅ Executes all promises in parallel.
// ✅ Resolves when ALL promises resolve.
// ❌ Rejects immediately if ANY promise rejects.

Promise.all([p1, p2, p3])
  // If all promises resolve, this .then() runs with an array of results
  .then((res) => console.log("Promise.all results:", res))
  // If any promise rejects, this .catch() runs with the rejection reason
  .catch((err) => console.log("Promise.all error:", err));

/*
⚡ Output after 1 second:
Promise.all error: p3 failed

Explanation:
- p3 rejects after 1 second.
- Since Promise.all() fails fast, it immediately rejects
  and ignores results from p1 and p2 (even though they are still running).
*/
```

Promise.all error: p3 failed

```

---
```

### 2️⃣ `Promise.allSettled()`

- Runs multiple promises **in parallel**.
- Waits for **all promises to settle**, regardless of success or failure.
- Returns an **array of objects** describing the outcome of each promise.

````js
Promise.allSettled([p1, p2, p3]).then((results) =>
  console.log("Promise.allSettled results:", results)
);


⚡ **Output after 3 seconds:**

```json
[
  { "status": "fulfilled", "value": "p1 success" },
  { "status": "fulfilled", "value": "p2 success" },
  { "status": "rejected", "reason": "p3 failed" }
]
````

---

```

```

### 3️⃣ `Promise.race()`

- Returns the **first settled promise** (resolved or rejected).
- Ignores the rest of the promises after the first settles.

```js
Promise.race([p1, p2, p3])
  .then((res) => console.log("Promise.race result:", res))
  .catch((err) => console.log("Promise.race error:", err));
```

⚡ **Output after 1 second:**

```
Promise.race error: p3 failed
```

---

### 4️⃣ `Promise.any()`

- Returns the **first fulfilled promise**.
- Ignores rejected promises unless **all promises are rejected** (then it throws an `AggregateError`).

```js
Promise.any([p1, p2, p3])
  .then((res) => console.log("Promise.any result:", res))
  .catch((err) => console.log("Promise.any error:", err));
```

⚡ **Output after 2 seconds:**

```
Promise.any result: p2 success
```

---

## 💡 Interview Insights: Promise APIs

| API                      | Description                     | Key Behavior                                            |
| ------------------------ | ------------------------------- | ------------------------------------------------------- |
| **Promise.all()**        | Runs promises in parallel       | Fails fast on first error                               |
| **Promise.allSettled()** | Returns results of all          | Never fails; returns status + value/reason              |
| **Promise.race()**       | First settled promise wins      | Can be success or failure                               |
| **Promise.any()**        | First _successful_ promise wins | Ignores rejections, throws `AggregateError` if all fail |

---

### 🌐 Pro Tips

- ✅ Use **`Promise.allSettled()`** for API calls where you want all responses, even if some fail.
- ⚡ Use **`Promise.race()`** or **`Promise.any()`** for **fastest response selection** or **timeouts**.

---

## 📺 Watch Live On YouTube

<a href="https://www.youtube.com/watch?v=DlTVt1rZjIo&list=PLxnjbfm5MCHFbRlyVCAqpJFdIzPN_IPID" target="_blank">
  <img src="https://img.youtube.com/vi/DlTVt1rZjIo/maxresdefault.jpg" width="750" alt="Namaste JS Episode 5 Thumbnail" />
</a>
