# Merge Sort

- Merge sort is a combination of two things:
  - Merging & sorting
- Actually, you could also say that it combines splitting up, merging, & sorting
- It exploits the fact that arrays of 0 or 1 element are already sorted
- It works by decomposing an array into smaller arrays of 0 or 1 elements, then building up a newly sorted array

![Merge Sort](https://camo.githubusercontent.com/64ba2bcbd5c11779657e40a1d03d0ea691f6fa57/68747470733a2f2f75706c6f61642e77696b696d656469612e6f72672f77696b6970656469612f636f6d6d6f6e732f632f63632f4d657267652d736f72742d6578616d706c652d33303070782e676966)

## Merging Arrays

- To implement merge sort, it’s useful to first implement a function responsible for merging two sorted arrays
- Given two arrays which are sorted, this helper function should create a new array which is also sorted and consists of all of the elements in the two input arrays
- This function should run in O(n + m) time and O(n + m) space and should not modify the parameters passed to it.
  - What O(n + m) means:
    - We now have two inputs in our function: n & m
    - If n grows super-large but m doesn’t grow very large, we get O(n + m)
    - In merge sort, they’re usually the same size or different by one element
- Each item is visited once

## Pseudocode

- Create an empty array.
  - Take a look at the smallest values in each input array
  - Use while loops, and start with two values (i & j) that start at 0
- While there are still values we haven’t looked at (while i & j haven’t hit the end of their respective arrays)
  - If the value in the first array is smaller than the value in the second array, push the value in the first array into our results and move on to the next value in the first array.
  - If the value in the first array is larger than the value in the second array, push the value in the second array into our results and move on to the next value in the second array.
  - Once we exhaust one array, push in all remaining values from the other array

## Execution

```javascript
const merge = (arr1, arr2) => {
  let result = [];
  let i = 0;
  let j = 0;

  while (i < arr1.length && j < arr2.length) {
    if (arr1[i] < arr2[j]) {
      result.push(arr1[i]);
      i++;
    } else if (arr1[i] > arr2[j]) {
      result.push(arr2[j]);
      j++;
    } else if (arr1[i] === arr2[j]) {
      result.push(arr1[i]);
      result.push(arr2[j]);
      i++;
      j++;
    }
  }

  while (i < arr1.length) {
    result.push(arr1[i]);
    i++;
  }
  while (j < arr2.length) {
    result.push(arr2[j]);
    j++;
  }
  return result;
};
```

## Merge Sort Pseudocode

Now that we have the _merging_ taken care of, let's figure out the whole picture.

- Break up the array into halves until you have arrays that are empty or have one element
  - Use array.slice( ) to do this.
  - Go from [0] to the middle of the array, and then from the middle to [0] (use Math.floor( ) when calculating the middle)
  - Keep doing this recursively
    - Base case: When arrays are <= 1
- Once you have smaller sorted arrays, merge those arrays with other sorted arrays until you’re back at the full length of the array
  - Use the merge algorithm we’ve already written
- Once the array has been merged back together, return the merged (and sorted!) array

```javascript
function mergeSort(arr) {
  if (arr.length <= 1) return arr;
  let mid = Math.floor(arr.length / 2);
  let left = mergeSort(arr.slice(0, mid));
  let right = mergeSort(arr.slice(mid));
  return merge(left, right);
}
const test = mergeSort([10, 82, 24, 2, 76, 73]);
console.log(test);
```

```javascript
function merge(arr1, arr2) {
  let result = [];
  let i = 0;
  let j = 0;
  while (i < arr1.length && j < arr2.length) {
    if (arr1[i] < arr2[j]) {
      result.push(arr1[i]);
      i++;
    } else if (arr1[i] > arr2[j]) {
      result.push(arr2[j]);
      j++;
    } else if (arr1[i] === arr2[j]) {
      result.push(arr1[i]);
      result.push(arr2[j]);
      i++;
      j++;
    }
  }
  while (i < arr1.length) {
    result.push(arr1[i]);
    i++;
  }
  while (j < arr2.length) {
    result.push(arr2[j]);
    j++;
  }
  return result;
}
```

---

## Big O of Merge Sort

- Time complexity is always **O(n log n)**
- Space complexity is always **O(n)**
  Merge sort doesn’t care what the data looks like, e.g. whether it’s sorted. It’ll approach the data the same way regardless.
