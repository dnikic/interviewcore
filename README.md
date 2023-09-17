# Interview Core
Core algorithms explained for everyone feeling the imposer syndrome.


TODO

- Add theory for all concepts
- Add and am example leetcode problem that is done using the mentioned concept.

Bing question:
- Whats the most common letcode problem that can be solved with recursion?

OpenAi question:
- Explain recursion in javascript and show an explained example of its ussagee to solve the reverse linked list letcode problem.

## Overview

6 coding interview concepts
- Hash map
- Recursion
- BFS
  DFS
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


## BFS (Breadth-first search)

Breadth-First Search (BFS) is a traversal algorithm used to explore or search through data structures, such as trees and graphs, in a breadthward motion. In the context of binary trees, BFS explores the nodes level by level, starting from the root and moving to the next level only after all nodes at the current level have been visited.

Here's a high-level explanation of how BFS works:

- Begin at the root node of the tree (or the starting point in a graph).
- Visit the current node.
- Enqueue (add to a queue) all the children (or neighbors) of the current node.
- Dequeue the current node (remove it from the queue).
- Repeat steps 2-4 until the queue is empty, which indicates that all nodes have been visited.

BFS is typically implemented using a queue data structure to keep track of the nodes to be visited. It ensures that nodes at the same level are visited before moving on to the next level, making it suitable for tasks like level order traversal.

Now, let's solve the "Binary Tree Level Order Traversal" problem on LeetCode using BFS:

Problem: Binary Tree Level Order Traversal

Given a binary tree, return its level order traversal as a 2D array.

Here's a JavaScript solution using BFS:

```javascript
class TreeNode {
  constructor(val) {
    this.val = val;
    this.left = null;
    this.right = null;
  }
}

function levelOrder(root) {
  if (!root) {
    return [];
  }

  const result = [];
  const queue = [root];

  while (queue.length > 0) {
    const levelSize = queue.length;
    const currentLevel = [];

    for (let i = 0; i < levelSize; i++) {
      const currentNode = queue.shift();
      currentLevel.push(currentNode.val);

      if (currentNode.left) {
        queue.push(currentNode.left);
      }

      if (currentNode.right) {
        queue.push(currentNode.right);
      }
    }

    result.push(currentLevel);
  }

  return result;
}

```

Explanation:
- We define a TreeNode class to represent the nodes of a binary tree. Each node has a val, left, and right property.
- The levelOrder function takes the root of the binary tree as input.
- We initialize an empty array result to store the level order traversal and a queue queue to perform BFS.
- We check if the root is null. If the tree is empty, we return an empty array.
- We enter a while loop that continues until the queue is empty. Inside the loop:
  - We get the size of the current level by checking the length of the queue (levelSize).
  - We create an empty array currentLevel to store the values of nodes at the current level.
  - We iterate through the nodes at the current level by dequeuing levelSize nodes from the front of the queue. For each dequeued node:
    - We add its value to currentLevel.
    - If the node has a left child, we enqueue it.
    - If the node has a right child, we enqueue it.
  - After processing all nodes at the current level, we push currentLevel into the result array.
- Finally, we return the result array, which contains the level order traversal of the binary tree.

Here's an example of how to use this function to perform level order traversal on a binary tree:
 
```javascript
const root = new TreeNode(3);
root.left = new TreeNode(9);
root.right = new TreeNode(20);
root.right.left = new TreeNode(15);
root.right.right = new TreeNode(7);

const result = levelOrder(root);
console.log(result);

```
The output will be a 2D array representing the level order traversal:

```javascript
[
  [3],
  [9, 20],
  [15, 7]
]

```
This output indicates that the nodes at each level of the binary tree have been traversed in order.



## DFS (Depth first search)

Depth-First Search (DFS) is a traversal algorithm used to explore or search through data structures, such as trees and graphs, by going as deeply as possible along each branch before backtracking. In the context of trees, DFS starts at the root and explores as far down one branch as possible before backtracking to explore other branches. There are two main variants of DFS: pre-order and post-order traversal.


In pre-order DFS, you visit the current node before visiting its children. In post-order DFS, you visit the children before visiting the current node.

Here's a high-level explanation of how pre-order DFS works:
- Start at the root node (or the starting point in a graph).
- Visit the current node.
- Recursively apply the DFS algorithm to each unvisited child node.
- Backtrack to the parent node and repeat steps 2-3 for other unvisited children.

DFS can be implemented using recursion or an explicit stack data structure. In JavaScript, recursion is often used for its simplicity.

Now, let's solve the "Sum of Distances in Tree" problem on LeetCode using DFS:

Problem: Sum of Distances in Tree

You are given an undirected tree with n nodes labeled from 0 to n - 1 and an array edges, where edges[i] = [a, b] indicates that there is an edge between nodes a and b in the tree. Return an array ans of length n where ans[i] is the sum of the distances between the ith node in the tree and all other nodes.

Here's a JavaScript solution using DFS:

```javascript
function sumOfDistancesInTree(n, edges) {
  const tree = new Map(); // Create an adjacency list to represent the tree
  const count = Array(n).fill(1); // To keep track of the number of nodes in each subtree
  const ans = Array(n).fill(0); // To store the sum of distances for each node

  // Create the adjacency list
  for (const [u, v] of edges) {
    if (!tree.has(u)) tree.set(u, []);
    if (!tree.has(v)) tree.set(v, []);
    tree.get(u).push(v);
    tree.get(v).push(u);
  }

  // DFS to calculate count and ans
  function dfs(node, parent) {
    for (const child of tree.get(node)) {
      if (child !== parent) {
        dfs(child, node);
        count[node] += count[child];
        ans[node] += ans[child] + count[child];
      }
    }
  }

  // DFS to update ans for all nodes
  function dfsUpdate(node, parent) {
    for (const child of tree.get(node)) {
      if (child !== parent) {
        ans[child] = ans[node] - count[child] + (n - count[child]);
        dfsUpdate(child, node);
      }
    }
  }

  dfs(0, -1); // Start DFS from the root (node 0)
  dfsUpdate(0, -1);

  return ans;
}

```

Explanation:
- We start by creating an adjacency list tree to represent the tree, where each node maps to its neighboring nodes. We also initialize two arrays: count to keep track of the number of nodes in each subtree and ans to store the sum of distances for each node.
- We iterate through the edges array and build the adjacency list.
- We define two DFS functions: dfs and dfsUpdate.
- The dfs function calculates the count and ans arrays for each node by recursively visiting all its children. It uses a parent parameter to avoid revisiting the parent node.
- The dfsUpdate function updates the ans array for all nodes based on the results obtained in the first DFS traversal.
- We start the DFS traversal from the root node (node 0) by calling dfs(0, -1).
- After the DFS traversal, we call dfsUpdate(0, -1) to update the ans array for all nodes.
- Finally, we return the ans array, which contains the sum of distances for each node.

Here's an example of how to use this function:

```javascript
const n = 6;
const edges = [[0, 1], [0, 2], [2, 3], [2, 4], [2, 5]];

const result = sumOfDistancesInTree(n, edges);
console.log(result);
```
The output will be an array containing the sum of distances for each node:

```javascript
[8, 12, 6, 10, 10, 10]

```
This output represents the sum of distances between each node and all other nodes in the tree.


