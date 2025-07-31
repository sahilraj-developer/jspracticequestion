# 📘 JavaScript Interview Prep – Day 2 / 10

10 Practical JavaScript Questions with Answers  
Focused on real-world interview concepts – closures, functional programming, async patterns, data manipulation, and more.

---

## ✅ 1. Deep Clone Without JSON

**Question:** Clone a nested object that includes arrays, dates, and functions — without using `JSON.stringify`.

```js
function deepClone(obj) {
  if (obj === null || typeof obj !== 'object') return obj;

  if (obj instanceof Date) return new Date(obj);
  if (obj instanceof Array) return obj.map(deepClone);

  const cloned = {};
  for (let key in obj) {
    cloned[key] = deepClone(obj[key]);
  }
  return cloned;
}

// Example
const original = { a: 1, b: { c: 2, d: new Date() } };
const copy = deepClone(original);



✅ 2. Group By Key in Array of Objects
Question: Group an array of objects by a specific key.


function groupBy(arr, key) {
  return arr.reduce((acc, item) => {
    const group = item[key];
    acc[group] = acc[group] || [];
    acc[group].push(item.name);
    return acc;
  }, {});
}

// Example
const data = [
  { type: 'fruit', name: 'apple' },
  { type: 'veg', name: 'carrot' },
  { type: 'fruit', name: 'banana' }
];

console.log(groupBy(data, 'type'));





✅ 3. Sleep Function with async/await
Question: Simulate a pause/delay using async/await.


function sleep(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}

async function run() {
  console.log('Start');
  await sleep(2000);
  console.log('End after 2 seconds');
}
run();



✅ 4. Compose Functions
Question: Compose multiple functions from right to left.


function compose(...fns) {
  return (x) => fns.reduceRight((val, fn) => fn(val), x);
}

const double = x => x * 2;
const square = x => x * x;

const composed = compose(square, double);
console.log(composed(2)); // 16





✅ 5. Memoize a Function
Question: Cache function results to avoid redundant computation.


function memoize(fn) {
  const cache = {};
  return function (x) {
    if (x in cache) return cache[x];
    cache[x] = fn(x);
    return cache[x];
  };
}

const fib = memoize(function(n) {
  if (n < 2) return n;
  return fib(n - 1) + fib(n - 2);
});

console.log(fib(40)); // Faster than normal recursion






✅ 6. Throttle Function
Question: Ensure a function runs at most once every limit ms.


function throttle(func, limit) {
  let lastCall = 0;
  return function (...args) {
    const now = Date.now();
    if (now - lastCall >= limit) {
      lastCall = now;
      func.apply(this, args);
    }
  };
}

// Example
window.addEventListener('scroll', throttle(() => {
  console.log('Scrolling...');
}, 2000));





✅ 7. Safely Access Deep Properties
Question: Avoid crashes when accessing deeply nested properties.


function get(obj, path, defaultValue = undefined) {
  return path.split('.').reduce((acc, key) => {
    return acc && acc[key] !== undefined ? acc[key] : defaultValue;
  }, obj);
}

const user = { address: { city: { name: "Delhi" } } };
console.log(get(user, "address.city.name")); // Delhi
console.log(get(user, "address.pincode", "N/A")); // N/A



✅ 8. Custom Array.prototype.map
Question: Recreate the built-in map method.


Array.prototype.myMap = function (callback) {
  const result = [];
  for (let i = 0; i < this.length; i++) {
    result.push(callback(this[i], i, this));
  }
  return result;
};

const arr = [1, 2, 3];
console.log(arr.myMap(x => x * 2)); // [2, 4, 6]





✅ 9. Find Duplicates Without Set
Question: Return duplicate elements using plain JS.


function findDuplicates(arr) {
  const seen = {};
  const dupes = [];

  for (let num of arr) {
    if (seen[num]) {
      if (!dupes.includes(num)) dupes.push(num);
    } else {
      seen[num] = true;
    }
  }
  return dupes;
}

console.log(findDuplicates([1, 2, 3, 2, 4, 1, 5])); // [2, 1]




✅ 10. Chainable Function Calls
Question: Support chaining with a .get() to return total.



function add(x) {
  let sum = x;

  const inner = (y) => {
    sum += y;
    return inner;
  };

  inner.get = () => sum;
  return inner;
}

console.log(add(5)(3)(2).get()); // 10
