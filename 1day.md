🔥 10 Practical JavaScript Questions with Answers
Level: Intermediate to Advanced | Topics: Arrays, Objects, Promises, async/await, real-world logic

✅ 1. Flatten a Deeply Nested Array
Question:


const arr = [1, [2, [3, [4, 5]]]];
// Output: [1, 2, 3, 4, 5]
Answer:


const flattenDeepArray = (arr) => arr.flat(Infinity);

console.log(flattenDeepArray([1, [2, [3, [4, 5]]])); // [1, 2, 3, 4, 5]

✅ 2. Flatten a Nested Object
Question:

const obj = {
  a: 1,
  b: {
    c: 2,
    d: {
      e: 3
    }
  }
};
Answer:

const flattenObject = (obj, prefix = '', res = {}) => {
  for (let key in obj) {
    const value = obj[key];
    const newKey = prefix ? `${prefix}.${key}` : key;

    if (typeof value === 'object' && value !== null && !Array.isArray(value)) {
      flattenObject(value, newKey, res);
    } else {
      res[newKey] = value;
    }
  }
  return res;
};

console.log(flattenObject(obj));
// { "a": 1, "b.c": 2, "b.d.e": 3 }


✅ 3. Flatten Array, Remove Duplicates, Sort
Question:


const input = [1, [2, [3, 2], 4], 5, [3, [6]]];
// Output: [1, 2, 3, 4, 5, 6]
Answer:


const processArray = (arr) => {
  return [...new Set(arr.flat(Infinity))].sort((a, b) => a - b);
};

console.log(processArray([1, [2, [3, 2], 4], 5, [3, [6]]]));


✅ 4. Fetch Multiple Users in Parallel
Question:


function fetchUserData(id) {
  return new Promise((res) => setTimeout(() => res({ id, name: "User " + id }), 1000));
}
// Fetch users 1, 2, 3 in parallel
Answer:


const getUsers = async () => {
  const ids = [1, 2, 3];
  const results = await Promise.all(ids.map(fetchUserData));
  console.log(results.map(u => u.name)); // ['User 1', 'User 2', 'User 3']
};

getUsers();


✅ 5. Retry Failing API Call
Question:


// Simulate an API that fails first 2 times and succeeds 3rd time
Answer:


let failCount = 0;

const unstableAPI = () => {
  return new Promise((resolve, reject) => {
    failCount++;
    failCount < 3 ? reject("Fail") : resolve("Success");
  });
};

const retry = async (fn, retries = 3) => {
  for (let i = 0; i < retries; i++) {
    try {
      const res = await fn();
      return res;
    } catch (err) {
      if (i === retries - 1) throw err;
    }
  }
};

retry(unstableAPI).then(console.log).catch(console.error);



✅ 6. Flatten Array Containing Promises
Question:


const arr = [1, Promise.resolve(2), [3, Promise.resolve([4, 5])]];
// Output: [1, 2, 3, 4, 5]
Answer:


const deepResolve = async (arr) => {
  const flat = await Promise.all(arr.flat(Infinity));
  return flat.flat(Infinity);
};

deepResolve([1, Promise.resolve(2), [3, Promise.resolve([4, 5])]])
  .then(console.log); // [1, 2, 3, 4, 5]
✅ 7. Remove Duplicate Objects by Key
Question:


const users = [
  { id: 1, name: 'A' },
  { id: 2, name: 'B' },
  { id: 1, name: 'A' }
];
Answer:


const uniqueUsers = (arr) => {
  const map = new Map();
  arr.forEach(user => map.set(user.id, user));
  return [...map.values()];
};

console.log(uniqueUsers(users));


✅ 8. Implement Custom Promise.all
Question:


// Create customPromiseAll(promises)
Answer:


function customPromiseAll(promises) {
  return new Promise((resolve, reject) => {
    let results = [], completed = 0;
    promises.forEach((p, i) => {
      Promise.resolve(p).then(res => {
        results[i] = res;
        completed++;
        if (completed === promises.length) resolve(results);
      }).catch(reject);
    });
  });
}

// Example:
customPromiseAll([Promise.resolve(1), Promise.resolve(2)])
  .then(console.log); // [1, 2]


✅ 9. Print 1–5 with 1 Second Delay Each
Question:


// Print numbers 1 to 5 with 1s delay each using async/await
Answer:


const delay = (ms) => new Promise(res => setTimeout(res, ms));

const printNumbers = async () => {
  for (let i = 1; i <= 5; i++) {
    await delay(1000);
    console.log(i);
  }
};

printNumbers();


✅ 10. Flatten and Resolve Nested Object Values
Question:


const data = [
  { id: 1, name: "Alice", meta: Promise.resolve({ age: 25 }) },
  { id: 2, name: "Bob", meta: Promise.resolve({ age: 30 }) }
];
Answer:


const flattenData = async (arr) => {
  return Promise.all(
    arr.map(async item => {
      const meta = await item.meta;
      return { ...item, ...meta };
    })
  );
};

flattenData(data).then(console.log);
/*
[
  { id: 1, name: "Alice", age: 25 },
  { id: 2, name: "Bob", age: 30 }
]
*/