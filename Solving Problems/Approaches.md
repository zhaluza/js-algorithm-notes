# Problem Solving Approaches

## What Is an Algorithm?

An algorithm is a process or set of steps to accomplish a certain task.

## How Do You Get Better At Solving Problems?

- Devise a plan for solving problems
  - How to approach a problem
  - Strategies for breaking it down
- Master common problem-solving patterns
  - A lot of interview algorithms fall under different categories
  - If you can identify the category, it’s easier to come up with a solution

## Basic Steps to Solving Problems

Each step will be explained in more detail below:

- Understand the Problem
- Explore Concrete Examples
- Break It Down
- Solve/Simplify
- Look Back & Refactor
  **1) Understand the Problem**
  Before you start typing, whiteboarding, etc… take a minute to look at the problem and understand it.

Ask yourself these questions (or ask the interviewer if something's unclear):

1. _Can I restate the problem in my own words?_
2. _What are the inputs that go into the problem?_
3. _What are the outputs that should come from the solution to the problem?_
4. _Can the outputs be determined from the inputs? In other words, do I have enough information to solve the problem?_
   (Might not be able to answer this question until you start solving the problem)
5. _How should I label the important pieces of data that are a part of the problem?_

**Example**
Write a function that takes two numbers and returns their sum.

1. Can I restate the problem in my own words?
   - Write a function that adds two number together
2. What are the inputs that go into the problem?
   - The two numbers being added together (num1, num2). Type: number
3. What are the outputs that should come from the solution to the problem?
   - Single output: sum (number).
4. Can the outputs be determined from the inputs? In other words, do I have enough information to solve the problem?
   - Probably, yes. But...
   - What happens if only one number is input? No numbers?
5. How should I label the important pieces of data that are a part of the problem?
   - num1, num2, sum

**2) Explore Examples**
Coming up with concrete examples can help you understand the problem better.

Examples also provide sanity checks that your eventual solution works as it should.

- e.g...
  - User stories
  - Unit testing

Steps for exploring examples

1. Start with simple examples
2. Progress to more complex examples
3. Explore examples with empty inputs (edge cases)
4. Explore examples with invalid inputs (edge cases)

**Example**
Write a function which takes in a string and returns counts of each character in the string.

Start with simple examples

```javascript
charCount(‘aaaa’); // {a:4}
charCount(‘hello’) // {h:1, e:1, l:2, o:1}
```

Question: Should the object be blank when the function begins running? Or should it be pre-filled for each letter, which is set to 0?

For example:

```javascript
charCount(‘aaaa’); // {a:4, b:0, c:0, d:0...}
```

You could clarify this with the interviewer to make sure you’re going about the question the right way.

More complex examples
Input:
“my phone number is 98237"
Should this function account for spaces? Numbers?

“Hello hi"
What about capital and lowercase letters? Should they be tracked differently? Or do they count as instances of the same character?

(The edge cases below aren’t that important for interviews, but they’re important to consider in real-life situations.)

Empty inputs
charCount(“”)
What should this return? An empty object? “null”? “undefined”? “false”? “error”?

Invalid inputs
What if someone passes in an object? Or “null”?

**3) Break It Down**
Break a problem down into its actual steps and write them down. Can be simple comments — doesn’t have to be full pseudo-code or valid syntax.

Explicitly write out the steps you need to take.
This forces you to think about the code you’ll write before you write it, and it helps you catch any lingering conceptual issues or misunderstandings before you dive in and have to worry about details (e.g. language syntax) as well.

For example, you could write the following notes for the “charCount” problem above:

Writing down these steps can make a huge difference if you run out of time during an interview — it can show the interviewer that you know what you’re doing, even if you haven’t finished writing the function.

**4) Solve Or Simplify**

If you can… Solve the problem.
If you can’t… Solve a simpler problem!

In other words, ignore the part that’s giving you trouble so that you can focus on everything else.

**Simplify**

- Find the core difficulty in what you’re trying to do
- Temporarily ignore that difficulty
- Write a simplified solution
- Then incorporate that difficulty back into the problem

**5) Look Back & Refactor**
Yes, you’ve solved it… But you’re not done!

Questions you can ask yourself now:

- Can you check the result? (i.e. does your code work?)
- Can you derive the result differently?
- Can you understand it at a glance? (how intuitive is your solution?)
- Can you use the result or method for some other problem?
- Can you improve the performance of your solution?
- Can you think of other ways to refactor?
- How have other people solved this problem?

Initial solution to the charCount function:

```javascript
charCount = str => {
  let obj = {};
  for (let i = 0; i < str.length; i++) {
    let char = str[i].toLowerCase();
    if (/[a-z0-9]/.test(char)) {
      if (obj[char] > 0) {
        obj[char]++;
      } else {
        obj[char] = 1;
      }
    }
  }
  return obj;
};
```

Potential fixes/refactoring:

```javascript
charCount = str => {
  let obj = {};
  // use a for/of loop instead
  for (let char of str) {
    // can remove the “let” and “str[i]” here
    char = char.toLowerCase();
    //replace regex with faster function
    if (isAlphaNumeric(char)) {
      // simplify the original if/else statement
      obj[char] = ++obj[char] || 1;
      };
    }
  }
  return obj;
}

// use this function to replace original regex
// much faster performance than regex!
isAlphaNumeric = char => {
  let code = char.charCodeAt(0);
  if (!(code > 47 && code < 58) && // numeric (0-9)
      !(code > 64 && code < 91) && // upper alpha (A-Z)
      !(code > 96 && code < 123)) { // lower alpha (a-z)
    return false;
  }
  return true;
}

```
