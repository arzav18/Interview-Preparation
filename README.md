Here are **working** coding examples for all the requested topics:  

---

## **1. Debouncing**  
### **What is it?**  
Debouncing ensures that a function is **executed only after a delay** from the last time it was invoked. Useful for search inputs, window resizing, and button clicks.

### **Code Example**
```js
function debounce(func, delay) {
  let timer;
  return function (...args) {  // 'args' represents function arguments
    clearTimeout(timer);
    timer = setTimeout(() => func.apply(this, args), delay);
  };
}

// Example: Debounced Search
function fetchResults(query) {
  console.log(`Fetching results for: ${query}`);
}

const debouncedSearch = debounce(fetchResults, 500);

// Simulate typing in a search bar
debouncedSearch("React");
debouncedSearch("React Hooks");
debouncedSearch("React Hooks Tutorial");  // Only this will execute after 500ms
```
🛠 **Explanation:**  
- `debounce` waits for **500ms** after the last keystroke before executing `fetchResults`.  
- Helps optimize **API calls** and prevents unnecessary executions.  

---

## **2. API Fetching**  
### **What is it?**  
Fetching data from an API using the `fetch` method.

### **Code Example**
```js
function fetchUserData() {
  fetch("https://jsonplaceholder.typicode.com/users/1")
    .then(response => response.json())
    .then(data => console.log("User Data:", data))
    .catch(error => console.error("Error fetching data:", error));
}

fetchUserData();
```
🛠 **Explanation:**  
- `fetch` makes an HTTP request to an API.  
- `.then(response => response.json())` converts response to JSON.  
- `.catch()` handles errors.  

---

## **3. Throttling**  
### **What is it?**  
Throttling ensures that a function **runs at most once per given time interval**, useful for scroll events and resizing.

### **Code Example**
```js
function throttle(func, delay) {
  let lastCall = 0;
  return function (...args) {
    const now = new Date().getTime();
    if (now - lastCall >= delay) {
      func.apply(this, args);
      lastCall = now;
    }
  };
}

// Example: Logging scroll event every 1 second
function logScroll() {
  console.log("User scrolled", new Date().toLocaleTimeString());
}

window.addEventListener("scroll", throttle(logScroll, 1000));
```
🛠 **Explanation:**  
- Ensures that `logScroll` executes **once per second** even if the scroll event fires multiple times.  

---

## **4. Closures**  
### **What is it?**  
A closure is a function that **remembers its lexical scope** even when executed outside that scope.

### **Code Example**
```js
function outerFunction(outerVariable) {
  return function innerFunction(innerVariable) {
    console.log(`Outer: ${outerVariable}, Inner: ${innerVariable}`);
  };
}

const newFunc = outerFunction("Hello");
newFunc("World");  // Output: Outer: Hello, Inner: World
```
🛠 **Explanation:**  
- `innerFunction` **remembers** `outerVariable` even after `outerFunction` has finished executing.  
- Useful for **data encapsulation** and **event handlers**.  

---

## **5. Currying**  
### **What is it?**  
Currying transforms a function into a **sequence of functions**, each accepting **one argument**.

### **Code Example**
```js
function curry(fn) {
  return function curried(...args) {
    if (args.length >= fn.length) {
      return fn.apply(this, args);
    } else {
      return (...nextArgs) => curried.apply(this, [...args, ...nextArgs]);
    }
  };
}

// Example: Curried Addition
function add(a, b, c) {
  return a + b + c;
}

const curriedAdd = curry(add);
console.log(curriedAdd(2)(3)(5)); // Output: 10
```
🛠 **Explanation:**  
- `curriedAdd(2)(3)(5)` invokes `add(2,3,5)`.  
- Useful in **functional programming**.  

---

## **6. Promises**  
### **What is it?**  
A `Promise` represents a **future value** and is used for **asynchronous operations**.

### **Code Example**
```js
function fetchData() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve("Data Fetched!");
    }, 2000);
  });
}

fetchData()
  .then(response => console.log(response))  // Output: "Data Fetched!" after 2 seconds
  .catch(error => console.log(error));
```
🛠 **Explanation:**  
- `resolve` is called after **2 seconds** to simulate an API call.  
- `.then()` handles success; `.catch()` handles errors.  

---

## **7. Async/Await**  
### **What is it?**  
`async/await` makes asynchronous code **look synchronous**.

### **Code Example**
```js
async function fetchUser() {
  try {
    const response = await fetch("https://jsonplaceholder.typicode.com/users/1");
    const data = await response.json();
    console.log("User Data:", data);
  } catch (error) {
    console.log("Error:", error);
  }
}

fetchUser();
```
🛠 **Explanation:**  
- `await` pauses execution until `fetch` completes.  
- **Better readability** than `.then()`.  

---

## **What is `args`?**  
### **Definition:**  
- `args` is used in **rest parameters** (`...args`).  
- It **collects function arguments** into an array.

### **Example:**  
```js
function sum(...args) {
  return args.reduce((total, num) => total + num, 0);
}

console.log(sum(1, 2, 3, 4, 5));  // Output: 15
```
🛠 **Explanation:**  
- `...args` gathers all arguments into an array.  
- `reduce()` sums all elements.  

---

## **Final Thoughts**  
These **working code examples** cover the most commonly asked **frontend JavaScript** concepts. Let me know if you need **React examples** or **mock interview questions**! 🚀


<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Random User API</title>
</head>
<body>
  <h2>Random User</h2>
  <div id="user-info">
    <p>Loading...</p>
  </div>
  <button id="fetch-user">Fetch New User</button>

  <script>
    const userInfoDiv = document.getElementById("user-info");
    const fetchUserButton = document.getElementById("fetch-user");

    // Function to fetch random user data
    const fetchRandomUser = async () => {
      userInfoDiv.innerHTML = "<p>Loading...</p>";  // Show loading message
      try {
        const response = await fetch("https://randomuser.me/api/");
        const data = await response.json();
        const user = data.results[0];

        // Update the user info in the HTML
        userInfoDiv.innerHTML = `
          <p>Name: ${user.name.first} ${user.name.last}</p>
          <p>Email: ${user.email}</p>
          <img src="${user.picture.medium}" alt="User" />
        `;
      } catch (error) {
        userInfoDiv.innerHTML = "<p>Failed to load user.</p>";
        console.error("Error fetching user:", error);
      }
    };

    // Fetch new user when button is clicked
    fetchUserButton.addEventListener("click", fetchRandomUser);

    // Fetch a random user when the page loads
    fetchRandomUser();
  </script>
</body>
</html>
