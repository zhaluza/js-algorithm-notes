# A Guide to Algorithms in JavaScript

## What This Is

The markdown files in this repo are a general guide to JavaScript algorithms. Much of this content originated as notes for Colt Steele's [Algorithm & Data Structures Bootcamp course](https://www.udemy.com/course/js-algorithms-and-data-structures-masterclass/) on Udemy.

## Links to Code Examples (on Repl.it)

#### [Main Folder: Colt Steele Algos](https://repl.it/repls/folder/Colt%20Steele%20Algos)

**[Problem-Solving Patterns](https://repl.it/repls/folder/Colt%20Steele%20Algos%2FProblem%20Solving%20Patterns)**

- [Frequency Counter](https://repl.it/@zhaluza/Frequency-Counter)
  - Creates separate objects to count the frequency of individual elements in separate arguments.
- [Pointers](https://repl.it/@zhaluza/Pointers)
  - This technique creates pointers that correspond to an index or position and move towards the beginning, end, or middle based on a certain condition.
- [Sliding Window](https://repl.it/@zhaluza/Sliding-Window)
  - This pattern involves creating a window, which can either be an array or number spanning from one position to another.
  - Depending on a certain condition, the window either widens or closes (and a new window is created).
  - Useful for keeping track of a subset of data in an array or string.

* [Divide and Conquer](https://repl.it/@zhaluza/Divide-and-Conquer)
  - This pattern involves dividing a data set into smaller chunks and then repeating a process with a subset of data. It's used in certain **searching** and **sorting** algorithms.
  - This pattern can tremendously decrease time complexity.

**[Optional Challenges](https://repl.it/repls/folder/Colt%20Steele%20Algos%2FOptional%20Challenges)**

- [sameFrequency](https://repl.it/@zhaluza/sameFrequency)
  - Write a function called sameFrequency. Given two positive integers, find out if the two numbers have the same frequency of digits.
    - **Strategy:** Frequency Counter
- [areThereDuplicates](https://repl.it/@zhaluza/areThereDuplicates)
  - Implement a function called areThereDuplicates, which accepts a variable number of arguments and checks whether there are any duplicates among the arguments passed in.
    - **Strategies:** Frequency Counter & Pointers
- [averagePair](https://repl.it/@zhaluza/averagePair)
  - Given a sorted array integers and a target average, determine if there is a pair of values in the array where the average of the pair equals the target average. There may be more than one pair that matches the average target.
    - **Strategy:** Multiple Pointers

* [isSubsequence](https://repl.it/@zhaluza/isSubsequence)
  - Write a function called isSubsequence which takes in two strings and checks whether the characters in the first string form a subsequence of the characters in the second string. In other words, the function should check whether the characters in the first string appear somewhere in the second string — without their order changing.
    - **Strategy:** Multiple Pointers
