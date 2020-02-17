# Insertion Sort

Insertion sort creates a growing left portion of the array that’s always sorted.
![Insertion Sort](https://camo.githubusercontent.com/890cae00ee39ecea48c4bc5f64182afc2530eb5c/68747470733a2f2f75706c6f61642e77696b696d656469612e6f72672f77696b6970656469612f636f6d6d6f6e732f392f39632f496e73657274696f6e2d736f72742d6578616d706c652e676966)

As the algorithm loops through the array, it takes each value and inserts it into the left portion.

## Insertion Sort Pseudocode

- Start by picking the second element in the array
- Now compare the second element with the one before it and swap if necessary
- Continue to the next element. If it’s in the incorrect order, iterate through the sorted portion (i.e. the left side) to place the element in the correct place
- Repeat until the array is sorted

```javascript
function insertionSort(arr) {
  for (var i = 1; i < arr.length; i++) {
    var currentVal = arr[i];
    for (var j = i - 1; j >= 0 && arr[j] > currentVal; j--) {
      arr[j + 1] = arr[j];
    }
    arr[j + 1] = currentVal;
  }
  return arr;
}
```

## Big O Complexity of Insertion Sort

Insertion sort’s Big O complexity is n². (worst-case scenario)

Ideal situation for insertion sort:

- Online algorithm: an algorithm that works as it receives data — doesn’t need to have the whole algorithm at once
  - Insertion sort works in this situation because it can handle each new piece of data at a time
  - It’s not a common situation, but it’s probably good to be aware of
