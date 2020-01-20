# Big O Notation

## Definition of Big O _(Time Complexity)_

We say that an algorithm is **O(f(n))** if the number of simple operations needed is eventually less than a constant times **f(n)**, as **n** increases.

For example:

- **f(n) = n**: _Linear_
- **(f(n) = n<sup>2</sup>)**: _Quadratic_
- **(f(n) = 1)**: _Constant_
- Etc.

This refers to the **worst-case scenario**: the **upper bound **for runtime.

### Types of Time Complexity (from fast to slow)

![Big O Chart](https://external-content.duckduckgo.com/iu/?u=http%3A%2F%2Fmattjmatthias.co%2Fcontent%2Fimages%2Fbig-o-chart.png&f=1&nofb=1)

- **Constant** - O(1)
- **Logarithmic** - O(log n)
- **Linear** - O(n)
- **Quadratic** - O(n<sup>2</sup>)

### Examples

```javascript
function addUpTo(n) {
  return (n * (n + 1)) / 2;
}
```

**Constant: O(1)**
Three operations will always be performed, regardless of the value of `n`.

---

```javascript
function addUpToFirst(n) {
  let total = 0;
  for (let i = 0; i <= n; i++) {
    total += i;
  }
  return total;
}
```

**Linear: O(n)**
Number of operations is bounded by a multiple of `n`

---

```javascript
function countUpAndDown(n) {
  console.log('Going up!');
  for (let i = 0; i < n; i++) {
    console.log(i);
  }
  console.log('At the top!\nGoing down...');
  for (let j = n - 1; j >= 0; j--) {
    console.log(j);
  }
  console.log('Back down. Bye!');
}
```

**Linear: O(n)**
Even though both `for` loops have a time complexity of **2n**, the overall Big O of this algorithm can still be simplified to **O(n)**.

---

```javascript
function printAllPairs(n) {
  for (let i = 0; i < n; i++) {
    for (let j = 0; j < n; j++) {
      console.log(i, j);
    }
  }
}
```

**Quadratic: O(n<sup>2</sup>)**
When an O(n) operation occurs within another O(n) operation — (e.g. a `for` loop nested inside another `for` loop), the overall time complexity is increased to O(n<sup>2</sup>).

---

## Simplifying Big O Expressions

Some easy rules of thumb for simplifying Big O expressions:

#### Constants Don't Matter

- If an algorithm contains two adjacent **O(n)** expressions, we ignore the constant in **O(2n)** and reduce it to **O(n)**.
- Likewise, a constant Big O of **O(500)** can be simplified to **O(1)**
- Same applies to quadratic Big O: **O(13n<sup>2</sup>)** = **O(n<sup>2</sup>)**

#### Smaller Terms Don't Matter

- We can ignore constants or linear numbers, as long as our Big O notation contains a greater type of value:
  - O(n + 10) = **O(n)**
  - O(1000n + 50) = **O(n)**
  - O(n<sup>2</sup> + 5n + 8) = **O(n<sup>2</sup>)**

---

### Big O Shorthand

1. Arithmetic operations: **Constant**
2. Variable assignment: **Constant**
3. Accessing elements in an array (by _index_) or object (by _key_) is **constant**.
4. In a _loop_, the complexity is the length of the loop multiplied by the complexity of whatever happens inside the loop (e.g. a nested loop: **n \* n = n<sup>2</sup>**)

---

## Big O & Space Complexity

Everything above this section refers to **time complexity**: how long it takes for an algorithm to run (aka the **runtime**).

The term **auxiliary space complexity** refers to space required by the algorithms — not including space taken up by the inputs. This is what we're talking about when we refer to "space complexity."

### Rules of Thumb for Space Complexity

- Most **primitives** (booleans, numbers, `undefined`, `null`) are **constant** space
- Strings require **O(n)** space (where _n_ is the string length)
- Reference types are generally O(n), where _n_ is the length (for arrays) or the number of keys (for objects)

### Examples

```javascript
function sum(arr) {
  let total = 0;
  for (let i = 0; i < arr.length; i++) {
    total += arr[i];
  }
  return total;
}
```

This algorithm has **O(1)** (**constant**) space — both variables are assigned numbers as variables.

---

```javascript
function double(arr) {
  let newArr = [];
  for (let i = 0; i < arr.length; i++) {
    newArr.push(2 * arr[i]);
  }
  return newArr;
}
```

**O(n)** (**linear**) space complexity — the number of entries stored in the new array will depend on the size of the array entered into the argument.

---

## Logarithmic Complexity

Logarithmic complexity — **O(log _n_)**, equivalent to **O(log<sub>2</sub> n)** — appears in certain cases.

- Certain **searching algorithms** have logarithmic time complexity
- Efficient **sorting algorithms** involve logarithms
- **Recursion** sometimes involves logarithmic space complexity

---

## Big O of Objects

### When to Use Objects

- When you don't need order
- When you need fast access/insertion and removal

**Time Complexity:**
Insertion, removal, access: O(1)
Searching: O(n)

Insertion, removal, and access are handled through a process known as **hashing** (using a data structure called a **hash map**).

### Big O of Object Methods

- `Object.keys`: O(n)
- `Object.values`: O(n)
- `Object.entries`: O(n)
- `hasOwnProperty`: O(1)

---

## Big O of Arrays

- **Insertion** & **removal**: depends
  - Working with the **end** of an array (`push`, `pop`) uses **constant** time - **O(1)**
  - However, manipulating the **beginning** (`unshift`, `shift`) means that all the other indices need to be adjusted. Therefore, it's **linear** - **O(n)**
- **Searching**: O(n)
  - Searching is **constant** since we'll potentially have to go through each element in the array
- **Access**: O(1)
  - If you try to access a value by a valid index, JS will go directly to that value (it doesn't need to go through every index preceding it), hence the _constant_ Big O

### When to Use Arrays

- When you need **order**
  - If order _isn't_ a priority, there are other options
  - Singly and doubly linked lists also provide order as well as better performance
- When you need fast access/insertion & removal (with a catch...)

### Big O of Array Methods

**Rule of thumb:** Everything is linear, except for manipulating the **end** of the array (`push`, `pop`) or **sorting**.

- `push`: O(1)
- `pop`: O(1)
- `shift`: O(n)
- `unshift`: O(n)
- `concat`: O(n)
  - Technically **O(n + m)** since you're merging two arrays with unique lengths, but still linear
- `slice`: O(n)
- `splice`: O(n)
- `sort`: O(n \* log n)
- `forEach`/`map`/`filter`/`reduce` etc.: O(n)
