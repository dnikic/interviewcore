# Interview Core
Core algorithms explained for everyone feeling the imposer syndrome.


TODO

- Add theory for all concepts
- Add and am example leetcode problem that is done using the mentioned concept.

Bing question:
- Whats the most common letcode problem that can be solved with recursion?

OpenAi question:
- Explain recursion in javascript and show an explained example of reverse linked list letcode problem.

## Overview

6 coding interview concepts
- Hash map
- Recursion
- BFS DFS
- Binary search
- Sliding window
- Heap
- Quick sort and difference between sorting algorithms (when to use which)

20 System design concepts
- see the youtube videofrom NetCode

8 desigh patterns
- Factory
- Builder
- Singleton
- Observer
- Iterator
- Strategy
- Adapter
- Facade

SOLID principles from interviewbit

OOP from interviewbit

## 6 coding interview concepts

### Hash map (object dictionary)
In JavaScript, a hash map (also known as an object or dictionary) is a data structure that allows you to store and retrieve values based on keys. It uses a hash function to map keys to specific locations (buckets) within the data structure, making it efficient to insert, delete, and retrieve values. Hash maps are often used to store key-value pairs, where each key is unique within the map.

Here's a basic example of a hash map in JavaScript:


```javascript
const hashMap = {
  key1: 'value1',
  key2: 'value2',
  key3: 'value3'
};
```
You can access values in a hash map using their keys like this:

```javascript
console.log(hashMap.key1); // Output: 'value1'
```
Problem: Longest Substring Without Repeating Characters
Given a string, find the length of the longest substring without repeating characters.
Here's a solution to this problem using a hash map:

```javascript
function lengthOfLongestSubstring(s) {
  const charMap = {}; // Hash map to store characters and their indices
  let maxLength = 0;
  let start = 0; // Start of the current substring

  for (let end = 0; end < s.length; end++) {
    const char = s[end];

    if (charMap[char] !== undefined && charMap[char] >= start) {
      // If the character is already in the substring, update the starting position
      start = charMap[char] + 1;
    }

    // Store the index of the current character in the hash map
    charMap[char] = end;

    // Calculate the length of the current substring
    const currentLength = end - start + 1;

    // Update maxLength if the current substring is longer
    if (currentLength > maxLength) {
      maxLength = currentLength;
    }
  }

  return maxLength;
}

// Example usage
const input = "abcabcbb";
console.log(lengthOfLongestSubstring(input)); // Output: 3 (The longest substring without repeating characters is "abc.")
```

Explanation:

- We use a charMap hash map to store characters from the string s as keys and their indices as values.
- We initialize start to 0, which represents the start of the current substring without repeating characters.
- We iterate through the string s using a sliding window approach, represented by the start and end pointers.
- When we encounter a character that is already in the substring, we update the start pointer to the next position after the last occurrence of that character.
- We update the charMap with the current character's index.
- We calculate the length of the current substring and update maxLength if the current length is greater than the previous maximum length.
- Finally, we return maxLength, which represents the length of the longest substring without repeating characters.

 In the example usage, the input string "abcabcbb" has the longest substring without repeating characters as "abc," which has a length of 3, so the function returns 3.

Notice
Try to do the "TwoSum" problem as well.

## Recursion

Recursion is a programming technique where a function calls itself in order to solve a problem. In JavaScript, recursion is a powerful and elegant way to solve complex problems by breaking them down into simpler, similar subproblems. It's important to have base cases or termination conditions in recursive functions to avoid infinite recursion.

Here's the basic structure of a recursive function in JavaScript:

```javascript
function recursiveFunction(params) {
  // Base case: check if the recursion should stop
  if (/* base case condition */) {
    // Return a value or perform an action
    return /* some value or action */;
  }

  // Recursive case: call the function with modified parameters
  return recursiveFunction(/* modified parameters */);
}

```

Now, let's explore a LeetCode problem that involves reversing a linked list using recursion:

Problem: Reverse Linked List

Given the head of a singly linked list, reverse the list and return its head.

Here's a solution to this problem using recursion:

```javascript
class ListNode {
  constructor(val) {
    this.val = val;
    this.next = null;
  }
}

function reverseLinkedList(head) {
  // Base case: if the list is empty or has only one node, return the head
  if (!head || !head.next) {
    return head;
  }

  // Recursive case: reverse the rest of the list and attach the current node at the end
  const reversedHead = reverseLinkedList(head.next);

  // Update the next pointer of the current node to point to its previous node
  head.next.next = head;
  head.next = null;

  return reversedHead;
}

```

Explanation:

- We define a ListNode class to represent the nodes of a singly linked list. Each node has a value (val) and a next pointer that points to the next node in the list.
- The reverseLinkedList function takes the head of a linked list as its input.
- In the base case, we check if the list is empty or has only one node. If either condition is met, we return the head as it is already reversed or there is nothing to reverse.
- In the recursive case, we call the reverseLinkedList function on the rest of the list (i.e., head.next). This recursive call will reverse the remaining part of the list and return the new head of the reversed list.
- After getting the reversed head, we update the next pointer of the current node (head.next.next) to point to its previous node (head). This effectively reverses the direction of the next pointer for the current node.
- Finally, we set the next pointer of the current node (head.next) to null to make it the last node in the reversed list and return the reversedHead.

In this way, the linked list is reversed recursively, and the new head of the reversed list is returned.

Here's an example of how to use this function to reverse a linked list:

```javascript
const head = new ListNode(1);
head.next = new ListNode(2);
head.next.next = new ListNode(3);
head.next.next.next = new ListNode(4);
head.next.next.next.next = new ListNode(5);

const reversedHead = reverseLinkedList(head);

// Printing the reversed list
let current = reversedHead;
while (current !== null) {
  console.log(current.val);
  current = current.next;
}

// Output:
// 5
// 4
// 3
// 2
// 1
```

In this example, we create a linked list with values 1, 2, 3, 4, and 5, and then use the reverseLinkedList function to reverse it. The reversed list is printed in reverse order: 5, 4, 3, 2, 1.







