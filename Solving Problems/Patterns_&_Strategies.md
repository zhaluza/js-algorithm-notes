# Problem Solving Patterns

There are many different patterns, or strategies, that can be used to tackle specific types of algorithm problems.

Some examples:

- Frequency counter
- Multiple pointers
- Sliding window
- Divide & conquer
- Dynamic programming
- Greedy algorithms
- Backtracking
- etc.

## Patterns

### Frequency Counter

This pattern uses objects or sets to collect values & frequencies of values. It’s usually O(N) time. This can often avoid the need for nested loops or O(N²) operations with arrays/strings.

Used to compare:

- Compare pieces of data
- Compare multiple inputs
  …to see if:
- They consist of similar values
- They’re anagrams of one another
- A value of one is contained inside another
- Frequencies of certain items occur

Example 1

Given two strings, write a function to determine if the second is an anagram of the first.

```javascript
validAnagram('', ''); // true
validAnagram('cinema', 'iceman'); // true
validAnagram('anagram', 'nagaram'); // true
validAnagram('car', 'atomic'); // false

const validAnagram = (str1, str2) => {
  if (str1.length !== str2.length) {
    return false;
  }

  let lookup = {};
  for (let i = 0; i < str1.length; i++) {
    let letter = str1[i];
    lookup[letter] ? (lookup[letter] += 1) : (lookup[letter] = 1);
  }

  for (let i = 0; i < str2.length; i++) {
    let letter = str2[i];
    if (!lookup[letter]) {
      return false;
    } else {
      lookup[letter] -= 1;
    }
  }
  return true;
};
```

### Multiple Pointers

This method creates pointers or values that correspond to an index or position and move toward the beginning, end, or middle based on a certain position.

Very efficient for solving problems, with minimal space complexity as well.

Note: This solution is only really effective when dealing with sorted inputs.

#### Example 1: sumZero

Write a function called sumZero, which accepts a sorted array of integers. The function should find the first pair where the sum is 0.

```javascript
const sumZero = arr => {
  // Set up left and right pointers
  // Left pointer starts at beginning: 0
  // Right starts at right: arr.length-1
  // Set up a while loop: while left pointer < right pointer (so they don't meet)
  //    Base: return left and right values if sum is 0
  //    If sum is greater than 0: move right pointer down
  //    Else (if sum < 0): move left pointer up
  // Will return undefined by default if not solved in the loop

  let left = 0;
  let right = arr.length - 1;

  while (left < right) {
    let sum = arr[left] + arr[right];
    if (sum === 0) {
      return [arr[left], arr[right]];
    }
    if (sum > 0) {
      left++;
    } else {
      right--;
    }
  }
};

const testzero1 = sumZero([-3, -2, -1, 0, 1, 2, 3]); // [-3,3]
const testzero2 = sumZero([-2, 0, 1, 3]); // undefined
const testzero3 = sumZero([1, 2, 3]); // undefined

console.log(testzero1);
console.log(testzero2);
console.log(testzero3);
```

#### Example 2: Count Unique Values

Implement a function called countUniqueValues, which accepts a sorted array, and counts the unique values in the array. There can be negative numbers in the array, but it will always be sorted.

**SOLUTION (variant of the Colt Steele way)**

```javascript
// Create a new array with all unique values, then return the length (more widely applicable to different problems, and unlike Colt's original solution, doesn't mutate the original input)
const countUniqueValues1 = arr => {
  // Create a copy of the input array (newArr)
  // Create two pointers:
  //    left: starts at 0
  //    right: starts at 1
  // Create a while loop - while right pointer < newArr.length
  //    if newArr[right] is the same as newArr[left], increment right
  //    if the array values are different, increment left. The value of newArr[left] becomes the value of newArr[right]. Increment right.
  // Return the value of left + 1
  if (arr.length === 0) {
    return 0;
  }
  let newArr = [...arr];
  let left = 0;
  let right = 1;
  while (right < newArr.length) {
    if (newArr[right] === newArr[left]) {
      right++;
    } else if (newArr[right] !== newArr[left]) {
      left++;
      newArr[left] = newArr[right];
      right++;
    }
  }
  return left + 1;

  // newArr.splice(left+1)
  // return newArr.length;
};
const testUnique1 = countUniqueValues1([1, 1, 1, 1, 1, 2]); // 2
const testUnique2 = countUniqueValues1([1, 2, 3, 4, 4, 4, 7, 7, 12, 12, 13]); // 7
const testUnique3 = countUniqueValues1([]); // 0
const testUnique4 = countUniqueValues1([-2, -1, -1, 0, 1]); // 4

console.log(testUnique1);
console.log(testUnique2);
console.log(testUnique3);
console.log(testUnique4);
```

---

#### Sliding Window

This pattern involves creating a window, which can either be an array or number spanning from one position to another.

Depending on a certain condition, the window either widens or closes (and a new window is created).

Useful for keeping track of a subset of data in an array or string.

#### Example: maxSubarraySum:

Write a function called maxSubarraySum, which accepts an array of integers and a number called `n`. The function should calculate the maximum sum of `n` consecutive elements in the array.

```javascript
const maxSubarraySum = (arr, num) => {
  // Create the 'window' by adding together the first n elements of the array
  // Next, 'slide' the window to the right by subtracting the value of the first element in the window and adding the value of the next element

  // Create a variable called maxSum - 0
  // Create a variable called tempSum - 0
  // Account for the edge case: if the array is shorter than the target number (or empty) return null
  // Create a 'for' loop: start at the beginning and loop through the first 'num' elements
  // Assign the resulting value to maxSum
  // Assign tempSum the value of maxSum
  // Create another 'for' loop, this one starting at arr[num] and looping through the whole array
  // Subtract the value of the first element in the window and add the value of the next (from maxSum)
  // Assign this value to tempSum
  // Use Math.max() to see whether val. of maxSum or tempSum is higher, and assign the result to maxSum
  // Return maxSum

  let maxSum = 0;
  let tempSum = 0;

  if (arr.length < num) return null;

  for (let i = 0; i < num; i++) {
    maxSum += arr[i];
  }
  tempSum = maxSum;
  for (let i = num; i < arr.length; i++) {
    tempSum = tempSum - arr[i - num] + arr[i];
    maxSum = Math.max(tempSum, maxSum);
  }
  return maxSum;
};

const test1 = maxSubarraySum([1, 2, 5, 2, 8, 1, 5], 2); // 10
const test2 = maxSubarraySum([1, 2, 5, 2, 8, 1, 5], 4); // 17
const test3 = maxSubarraySum([4, 2, 1, 6], 1); // 6
const test4 = maxSubarraySum([4, 2, 1, 6, 2], 4); // 13
const test5 = maxSubarraySum([], 4); // null

console.log(test1);
console.log(test2);
console.log(test3);
console.log(test4);
console.log(test5);
```

Divide & Conquer

This pattern involves dividing a data set into smaller chunks and then repeating a process with a subset of data.

This pattern can tremendously decrease time complexity.

Quite a few D&C algorithms are used in this course.

- One is a searching algorithm (binary search).
- Two of them are sorting algorithms (quick sort & merge sort).

Example

Naive Solution (linear search)
Time Complexity O(N)

Refactored Solution
Time Complexity Log(N) (Binary Search!)
