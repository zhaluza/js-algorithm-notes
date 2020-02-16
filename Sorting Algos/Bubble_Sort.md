# Bubble Sort

Bubble sort actually isn’t very efficient. It isn’t very commonly used.

However, there is one use case in which it excels.

Bubble sort is a sorting algorithm in which the largest values “bubble” up to the top.

![bubble sort example](https://camo.githubusercontent.com/520469553d840a35ebff47a95ecd2bd9f9c2612b/68747470733a2f2f75706c6f61642e77696b696d656469612e6f72672f77696b6970656469612f636f6d6d6f6e732f302f30362f427562626c652d736f72742e676966)

## Swapping Values in JavaScript

There are multiple valid approaches to implement the value swap for bubble sorting in JavaScript:

```javascript
// ES5 - Colt’s favorite
function swap(arr, idx1, idx2) {
  var temp = arr[idx1];
  arr[idx1] = arr[idx2];
  arr[idx2] = temp;
}
```

```javascript
// ES6
const swap = (arr, idx1, idx2) => {
  [arr[idx1], arr[idx2]] = [arr[idx2], arr[idx1]];
};
```

#### Pseudocode:

- Start looping with a variable called i from the end of the array towards the beginning
- Start an inner loop with a variable called j from the beginning until i - 1
- If arr[j] is greater than arr[j + 1], swap those two values!
- Return the sorted array

#### Implementation:

```javascript
const bubble = array => {
  const swap = (arr, idx1, idx2) => {
    [arr[idx1], arr[idx2]] = [arr[idx2], arr[idx1]];
  };

  // first loop sets the limits of the available space
  for (let i = array.length; i >= 0; i--) {
    // swapping happens here
    for (let j = 0; j < i - 1; j++) {
      if (array[j] > array[j + 1]) {
        swap(array, j, j + 1);
      }
    }
  }
  return array;
};
```

## Optimizing Bubble Sort

When dealing with arrays that are mostly sorted or already sorted, the bubble sort algorithm above won’t treat them any differently. It’ll still go through them step by step, even when it doesn’t need to.

To solve this, we can short-circuit our code by adding some extra instructions:

- Did we make any swaps the last time through?
- If not, we can terminate the function
- We can do this by introducing a boolean variable called noSwaps into our algorithm

```javascript
const bubble = array => {
  let noSwaps;
  const swap = (arr, idx1, idx2) => {
    [arr[idx1], arr[idx2]] = [arr[idx2], arr[idx1]];
  };
  // first loop sets the limits of the available space
  for (let i = array.length; i >= 0; i--) {
    noSwaps = true;
    // swapping happens here
    for (let j = 0; j < i - 1; j++) {
      if (array[j] > array[j + 1]) {
        swap(array, j, j + 1);
        noSwaps = false;
      }
    }
    if (noSwaps) break;
  }
  return array;
};
```

## Big O Complexity of Bubble Sort

Bubble sort’s Big O complexity is typically n².
However, if the data is nearly sorted and the “noSwaps” technique (above) is applied, the complexity is linear, or O(n).
