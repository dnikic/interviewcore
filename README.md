# Interview Core
Core algorithms explained for everyone feeling the imposer syndrome.


TODO

- Add theory for all concepts
- Add and am example leetcode problem that is done using the mentioned concept.

Bing question:
- Whats the most common letcode problem that can be solved with recursion?

OpenAi question:
- Explain recursion in javascript and show an explained example of its ussagee to solve the reverse linked list letcode problem.

Explain algorith complexity and it's types, how to determine complexity and give an explained JavaScript example of an algorithm analysis .

## Overview

Algorithm complexity

6 coding interview concepts
- Hash map
- Recursion
- BFS
  DFS
- Binary search
- Sliding window
- Heap
- Quick sort and difference between sorting algorithms (when to use which)


OOP in javasscript

SOLID principles from interviewbit

OOP vs Functional javascript principles

8 desigh patterns
- Factory
- Builder
- Singleton
- Observer
- Iterator
- Strategy
- Adapter
- Facade

20 System design concepts
- see the youtube videofrom NetCode


## Algorith complexity

Algorithm complexity, often referred to as algorithmic complexity or computational complexity, is a measure of the amount of computational resources (such as time and space) required by an algorithm to solve a specific problem. It provides insight into how the algorithm's performance scales with input size. The two main types of algorithm complexity are time complexity and space complexity.

### Time Complexity 
Time complexity describes how the execution time of an algorithm increases as the size of the input grows. It quantifies the number of basic operations an algorithm performs in relation to the size of the input. Time complexity is often expressed using Big O notation, which provides an upper bound on the growth rate of the running time.

Common time complexities include:

- O(1) - Constant Time: The algorithm's runtime is constant, meaning it takes the same amount of time regardless of the input size.
- O(log n) - Logarithmic Time: The runtime grows logarithmically with the input size.
- O(n) - Linear Time: The runtime grows linearly with the input size.
- O(n log n) - Linearithmic Time: The runtime grows in proportion to n times the logarithm of n.
- O(n^2) - Quadratic Time: The runtime grows with the square of the input size.
- O(2^n) - Exponential Time: The runtime grows exponentially with the input size.

### Space Complexity

Space complexity quantifies the amount of memory space an algorithm uses in relation to the input size. It is often measured in terms of auxiliary space, which excludes the input space.

Common space complexities include:

- O(1) - Constant Space: The algorithm uses a fixed amount of memory space regardless of the input size.
- O(n) - Linear Space: The algorithm's space usage grows linearly with the input size.
- O(n^2) - Quadratic Space: The algorithm's space usage grows with the square of the input size.



### Algorithm complexity analysis with a simple JavaScript example

Determining the complexity of an algorithm involves analyzing its code and understanding how the number of operations or memory usage changes as the input size increases. Key steps in determining algorithm complexity include:

- Identify the Input Size: Determine what parameter(s) represent the size of the input to your algorithm. This could be a single variable, an array, or a combination of variables.
- Count Basic Operations: Analyze your algorithm and count the number of basic operations it performs as a function of the input size. This typically includes arithmetic operations, comparisons, and assignments.
- Express Complexity: Use appropriate notation (such as Big O notation) to express the algorithm's time and space complexity based on the analysis. Big O notation provides a concise way to describe the upper bounds of complexity.

Problem: Find the Maximum Element in an Array

```javascript
function findMax(arr) {
  let max = arr[0]; // Initialize max to the first element of the array

  for (let i = 1; i < arr.length; i++) {
    if (arr[i] > max) {
      max = arr[i]; // Update max if the current element is larger
    }
  }

  return max;
}


```

Complexity Analysis:

- Input Size: In this example, the input size is the length of the array, denoted as n.
- Count Basic Operations:
  - Initializing max takes a constant amount of time, O(1).
  - The for loop iterates over the elements of the array once, performing one comparison and one assignment for each element. In the worst case, it performs n - 1 comparisons and assignments.
  - Returning the max value takes a constant amount of time, O(1).
- Express Complexity:
  - The dominant factor in this algorithm is the loop, which performs n - 1 comparisons and assignments. Therefore, the time complexity is O(n).
  - The algorithm uses a constant amount of additional memory space (for max and loop variables), so the space complexity is O(1).


So, the time complexity of the findMax algorithm is O(n), indicating that the number of operations grows linearly with the size of the input array. The space complexity is O(1), indicating constant space usage regardless of the input size.


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

### Recursion

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


### BFS (Breadth-first search)

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



### DFS (Depth first search)

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

### Binary search

Binary search is a search algorithm used to find a specific target value within a sorted collection, such as an array. It operates by repeatedly dividing the search interval in half until the target value is found or it's determined that the value doesn't exist in the collection. Binary search is efficient and typically much faster than linear search for large sorted datasets.

Here's the basic idea behind binary search:
- Start with the entire sorted collection.
- Calculate the midpoint of the current interval.
- Compare the target value with the value at the midpoint.
  - If the target is equal to the midpoint value, the search is successful, and you've found the target.
  - If the target is less than the midpoint value, update the search interval to the left half of the current interval and repeat the process.
  - If the target is greater than the midpoint value, update the search interval to the right half of the current interval and repeat the process.
- Repeat steps 2-3 until the target is found or the search interval becomes empty.

  Binary search can be implemented using a loop or recursion, and it has a time complexity of O(log n), making it very efficient for large datasets.

Now, let's see how binary search can be used to solve the "Find Median Sorted Arrays" problem on LeetCode:

Problem: Find Median Sorted Arrays

Given two sorted arrays nums1 and nums2 of size m and n respectively, find the median of the two sorted arrays.

Here's a JavaScript solution using binary search:

```javascript
function findMedianSortedArrays(nums1, nums2) {
  // Ensure nums1 is the smaller array or of equal size
  if (nums1.length > nums2.length) {
    [nums1, nums2] = [nums2, nums1];
  }

  const m = nums1.length;
  const n = nums2.length;
  const halfLen = Math.floor((m + n + 1) / 2);

  let left = 0;
  let right = m;

  while (left <= right) {
    const partitionX = Math.floor((left + right) / 2);
    const partitionY = halfLen - partitionX;

    const maxX = partitionX === 0 ? Number.NEGATIVE_INFINITY : nums1[partitionX - 1];
    const maxY = partitionY === 0 ? Number.NEGATIVE_INFINITY : nums2[partitionY - 1];

    const minX = partitionX === m ? Number.POSITIVE_INFINITY : nums1[partitionX];
    const minY = partitionY === n ? Number.POSITIVE_INFINITY : nums2[partitionY];

    if (maxX <= minY && maxY <= minX) {
      if ((m + n) % 2 === 0) {
        return (Math.max(maxX, maxY) + Math.min(minX, minY)) / 2;
      } else {
        return Math.max(maxX, maxY);
      }
    } else if (maxX > minY) {
      right = partitionX - 1;
    } else {
      left = partitionX + 1;
    }
  }

  throw new Error("Input arrays are not sorted.");
}

```

Explanation:

- To find the median of two sorted arrays, we ensure that nums1 is the smaller array (or of equal size) by swapping them if necessary. This simplifies the binary search implementation.
- We calculate the length of the combined arrays (m + n) and the half length (halfLen). The half length represents the index where the median(s) would be if the arrays were merged.
- We initialize two pointers, left and right, for binary search. left starts at 0, and right starts at the length of nums1.
- In the binary search loop, we calculate partitionX as the midpoint between left and right. partitionY is calculated based on halfLen and partitionX.
- We then calculate the maximum and minimum values on the left (maxX and minX) and right (maxY and minY) sides of the partitions.
- We compare these values to determine if we have found the correct partitions. If maxX <= minY and maxY <= minX, it means we have found the correct partitions, and we can compute the median accordingly.
- If maxX is greater than minY, we need to move partitionX to the left to reduce maxX. If maxY is greater than minX, we need to move partitionX to the right to increase maxY.
- We repeat the binary search until we find the correct partitions that satisfy the conditions for finding the median.
- If the loop finishes without finding the correct partitions, it means the input arrays are not sorted, so we throw an error.

Here's an example of how to use this function:

```javascript
const nums1 = [1, 3];
const nums2 = [2];

const median = findMedianSortedArrays(nums1, nums2);
console.log(median); // Output: 2.0

```
In this example, we find the median of the sorted arrays [1, 3] and [2], which is 2.0.


### Sliding window

Sliding window is a common algorithmic technique used to efficiently process and analyze arrays or strings. It involves maintaining a "window" (usually a subarray or substring) of elements within the larger data structure and "slides" it through the data to perform some operation. Sliding window is particularly useful for solving problems that involve finding subarrays or substrings with specific characteristics.

Here's the basic idea of the sliding window technique:

- Initialize two pointers, typically named left and right, to define the window. These pointers represent the start and end of the window, respectively.
- Expand the window by moving the right pointer to the right (or incrementing it) while a certain condition is met. This condition depends on the problem's requirements.
- Once the condition is no longer satisfied, start contracting the window by moving the left pointer to the right (or incrementing it) until the condition is satisfied again.
- Keep track of the optimal solution or perform required operations during the process.
- Repeat steps 2-4 until the right pointer reaches the end of the data structure.

Sliding window is especially useful for problems that involve finding the longest or shortest subarray/substring, subarrays/substrings with a specific sum, subarrays/substrings with distinct elements, etc.

Now, let's illustrate the sliding window technique by solving the "Longest Substring Without Repeating Characters" problem on LeetCode:

Problem: Longest Substring Without Repeating Characters

Given a string s, find the length of the longest substring without repeating characters.

Here's a JavaScript solution using the sliding window technique:

```javascript
function lengthOfLongestSubstring(s) {
  const charSet = new Set(); // To store unique characters in the current window
  let maxLength = 0;
  let left = 0; // Start of the current substring

  for (let right = 0; right < s.length; right++) {
    const char = s[right];

    // If the character is already in the current window, move the left pointer
    while (charSet.has(char)) {
      charSet.delete(s[left]);
      left++;
    }

    // Add the current character to the window
    charSet.add(char);

    // Update maxLength if the current substring is longer
    maxLength = Math.max(maxLength, right - left + 1);
  }

  return maxLength;
}

```

Explanation:

- We initialize a Set called charSet to keep track of the unique characters within the current window.
- We also initialize maxLength to store the length of the longest substring and left to represent the start of the current substring.
- We iterate through the string s using a sliding window defined by the left and right pointers.
- At each step, we check if the current character char is already in the charSet. If it is, it means we've encountered a repeating character, so we need to move the left pointer to the right to exclude the repeating character from the window.
- We keep moving the left pointer until the repeating character is removed from the window, and we update the charSet accordingly.
- We add the current character char to the window by adding it to the charSet.
- We update maxLength by comparing it with the length of the current substring (right - left + 1) and taking the maximum value.
- After processing the entire string, we return maxLength, which represents the length of the longest substring without repeating characters.

Here's an example of how to use this function:

```javascript
const input = "abcabcbb";
const length = lengthOfLongestSubstring(input);
console.log(length); // Output: 3 (The longest substring without repeating characters is "abc.")

```

In this example, the input string "abcabcbb" has the longest substring without repeating characters as "abc," which has a length of 3, so the function returns 3.


### Heap

A heap is a specialized tree-based data structure that satisfies the heap property. In a max heap, for example, every parent node has a value greater than or equal to the values of its children nodes. Conversely, in a min heap, every parent node has a value less than or equal to the values of its children nodes. Heaps are often used to efficiently find and remove the maximum (in a max heap) or minimum (in a min heap) element from a collection.

In JavaScript, you can implement a heap using an array. The root of the heap is typically the first element (index 0) in the array. The parent-child relationships are defined by the indices. For a node at index i, its left child is at index 2i + 1, and its right child is at index 2i + 2. Conversely, for a child node at index j, its parent is at index (j - 1) / 2.

Here's a basic example of a max heap implemented as an array:

```javascript
const maxHeap = [10, 7, 5, 3, 6, 1, 4];

```

In this max heap, the root (index 0) contains the maximum element, which is 10, and each parent node has a value greater than or equal to its children nodes.

Now, let's use a max heap to solve the "Kth Largest Element in an Array" problem:

Problem: Kth Largest Element in an Array

Given an integer array nums and an integer k, return the kth largest element in the array.

Here's a JavaScript solution using a max heap:

```javascript
class MaxHeap {
  constructor() {
    this.heap = [];
    this.size = 0;
  }

  insert(val) {
    this.heap.push(val);
    this.size++;
    this.heapifyUp();
  }

  extractMax() {
    if (this.size === 0) {
      return null;
    }
    if (this.size === 1) {
      this.size--;
      return this.heap.pop();
    }

    const max = this.heap[0];
    this.heap[0] = this.heap.pop();
    this.size--;
    this.heapifyDown();
    return max;
  }

  heapifyUp() {
    let currentIdx = this.size - 1;
    while (currentIdx > 0) {
      const parentIdx = Math.floor((currentIdx - 1) / 2);
      if (this.heap[currentIdx] > this.heap[parentIdx]) {
        [this.heap[currentIdx], this.heap[parentIdx]] = [this.heap[parentIdx], this.heap[currentIdx]];
        currentIdx = parentIdx;
      } else {
        break;
      }
    }
  }

  heapifyDown() {
    let currentIdx = 0;
    while (true) {
      const leftChildIdx = 2 * currentIdx + 1;
      const rightChildIdx = 2 * currentIdx + 2;
      let maxChildIdx = null;

      if (leftChildIdx < this.size) {
        maxChildIdx = leftChildIdx;
        if (rightChildIdx < this.size && this.heap[rightChildIdx] > this.heap[leftChildIdx]) {
          maxChildIdx = rightChildIdx;
        }
      }

      if (maxChildIdx === null || this.heap[currentIdx] >= this.heap[maxChildIdx]) {
        break;
      }

      [this.heap[currentIdx], this.heap[maxChildIdx]] = [this.heap[maxChildIdx], this.heap[currentIdx]];
      currentIdx = maxChildIdx;
    }
  }
}

function findKthLargest(nums, k) {
  const maxHeap = new MaxHeap();

  for (const num of nums) {
    maxHeap.insert(num);
    if (maxHeap.size > k) {
      maxHeap.extractMax();
    }
  }

  return maxHeap.extractMax();
}

```

Explanation:

- We define a MaxHeap class that implements the max heap data structure. It provides methods for inserting elements (insert), extracting the maximum element (extractMax), and maintaining the heap property (heapifyUp and heapifyDown).
- The findKthLargest function initializes a max heap and inserts elements from the nums array one by one. If the heap size exceeds k, we extract the maximum element to maintain a heap of size k. Eventually, the kth largest element will be at the root of the max heap.
- We return the maximum element in the max heap, which is the kth largest element in the nums array.

  Here's an example of how to use this function:
  
```javascript

const nums = [3, 2, 1, 5, 6, 4];
const k = 2;
const kthLargest = findKthLargest(nums, k);
console.log(kthLargest); // Output: 5 (The 2nd largest element in the array is 5)


```

In this example, we find the 2nd largest element in the nums array, which is 5.


## Sorting algorithms

You should have an understanding when to use which sorting algorithm, and how they work, but it is not necessary to implement them every time on your own because they are included as method in most programming languages.

### Sorting Algorithms Usage Table

| Use Case    | Recommended Sorting Algorithm |
| -------- | ------- |
| Small dataset or nearly sorted data  | Bubble Sort, Insertion Sort    |
| Medium-sized dataset    | Merge Sort, Quick Sort    |
| Large dataset where worst-case matters    | Merge Sort, Heap Sort    |
| Large dataset with many duplicate values    | Quick Sort (with optimization)    |



| Sorting Algorithm    | Best-Case Time Complexity | Average-Case Time Complexity | Worst-Case Time Complexity | Space Complexity | Stable? |
| -------- | ------- | ------- | ------- | ------- | ------- |
| Bubble Sort  | O(n)    | O(n^2)    | O(n^2)    | O(1)    | Yes    |
| Selection Sort  | O(n^2)    | O(n^2)    | O(n^2)    | O(1)    | No    |
| Insertion Sort  | O(n)    | O(n^2)    | O(n^2)    | O(1)    | Yes    |
| Merge Sort  | O(n log n)    | O(n log n)    | O(n log n)    | O(n)    | Yes    |
| Quick Sort  | O(n log n)    | O(n log n)    | O(n^2)    | O(log n)    | No    |
| Heap Sort  | O(n log n)    | O(n log n)    | O(n log n)    | O(1)    | No    |

Here's a brief explanation of each column:

- Sorting Algorithm: The name of the sorting algorithm.
- Best-Case Time Complexity: The minimum number of basic operations required in the best-case scenario (e.g., when the input is already sorted).
- Average-Case Time Complexity: The expected number of basic operations required on average, assuming random input data.
- Worst-Case Time Complexity: The maximum number of basic operations required in the worst-case scenario (e.g., when the input is sorted in reverse order).
- Space Complexity: The amount of additional memory space required by the algorithm, excluding the input data.
- Stable?: Indicates whether the sorting algorithm preserves the relative order of equal elements. If "Yes," it means that equal elements will maintain their relative order in the sorted output.

### Solving 3Sum Problem Using Sorting

Now, let's use one of these sorting algorithms, such as Quick Sort, to solve the "3Sum" problem on LeetCode.

Problem: 3Sum

Given an array nums of n integers, find all unique triplets in the array that add up to a target sum.

Here's a JavaScript solution using Quick Sort:

```javascript
function threeSum(nums) {
  const result = [];
  nums.sort((a, b) => a - b);

  for (let i = 0; i < nums.length - 2; i++) {
    if (i === 0 || (i > 0 && nums[i] !== nums[i - 1])) {
      let lo = i + 1;
      let hi = nums.length - 1;
      const target = -nums[i];

      while (lo < hi) {
        if (nums[lo] + nums[hi] === target) {
          result.push([nums[i], nums[lo], nums[hi]]);
          while (lo < hi && nums[lo] === nums[lo + 1]) lo++;
          while (lo < hi && nums[hi] === nums[hi - 1]) hi--;
          lo++;
          hi--;
        } else if (nums[lo] + nums[hi] < target) {
          lo++;
        } else {
          hi--;
        }
      }
    }
  }

  return result;
}

```

In this solution, we first sort the input array nums using Quick Sort. Then, we iterate through the sorted array while using two pointers (lo and hi) to find pairs of elements that sum up to the target value. This algorithm takes advantage of the sorted order to efficiently find triplets that add up to zero.

Now you can use the threeSum function to find all unique triplets in an array that sum up to a target value.

### Sorting algorithms javascript implementation

#### Quick Sort

Quick Sort is another divide-and-conquer sorting algorithm. It selects a "pivot" element and partitions the array into two subarrays: one with elements less than the pivot and one with elements greater than the pivot. It then recursively sorts the subarrays.

```javascript
function quickSort(arr) {
  if (arr.length <= 1) {
    return arr;
  }

  const pivot = arr[arr.length - 1];
  const left = [];
  const right = [];

  for (let i = 0; i < arr.length - 1; i++) {
    if (arr[i] < pivot) {
      left.push(arr[i]);
    } else {
      right.push(arr[i]);
    }
  }

  return [...quickSort(left), pivot, ...quickSort(right)];
}

```

### Merge Sort

Merge Sort is a divide-and-conquer sorting algorithm that divides the input into smaller parts, sorts them, and then merges the sorted parts back together.

```javascript
function mergeSort(arr) {
  if (arr.length <= 1) {
    return arr;
  }

  const mid = Math.floor(arr.length / 2);
  const left = arr.slice(0, mid);
  const right = arr.slice(mid);

  return merge(mergeSort(left), mergeSort(right));
}

function merge(left, right) {
  const result = [];
  let leftIndex = 0;
  let rightIndex = 0;

  while (leftIndex < left.length && rightIndex < right.length) {
    if (left[leftIndex] < right[rightIndex]) {
      result.push(left[leftIndex]);
      leftIndex++;
    } else {
      result.push(right[rightIndex]);
      rightIndex++;
    }
  }

  return result.concat(left.slice(leftIndex)).concat(right.slice(rightIndex));
}


```

#### Bubble Sort

Bubble Sort is a simple sorting algorithm that repeatedly steps through the list, compares adjacent elements, and swaps them if they are in the wrong order. It continues to do this until no more swaps are needed, indicating that the list is sorted.


```javascript
function bubbleSort(arr) {
  const n = arr.length;
  let swapped;
  do {
    swapped = false;
    for (let i = 0; i < n - 1; i++) {
      if (arr[i] > arr[i + 1]) {
        [arr[i], arr[i + 1]] = [arr[i + 1], arr[i]]; // Swap elements
        swapped = true;
      }
    }
  } while (swapped);
  return arr;
}

````

## Object oriented principles (OOP)
  TODO

## SOLID principles in javascript

The SOLID principles are a set of five design principles in object-oriented programming that aim to create more maintainable, flexible, and understandable software. These principles were introduced by Robert C. Martin and are often used as guidelines for writing clean and maintainable code. 

- 1. Single Responsibility Principle (SRP)
- 2. Open/Closed Principle (OCP)
- 3. Liskov Substitution Principle (LSP)
- 4. Interface Segregation Principle (ISP)
- 5. Dependency Inversion Principle (DIP)


Let's explore each of the SOLID principles using JavaScript examples:

### 1. Single Responsibility Principle (SRP):

This principle states that a class should have only one reason to change, meaning it should have only one responsibility or job.

Example in JavaScript:

```javascript

// Not following SRP
class Employee {
  constructor(name, salary) {
    this.name = name;
    this.salary = salary;
  }

  calculateSalary() {
    // Calculate employee's salary
  }

  saveToDatabase() {
    // Save employee data to the database
  }
}

// Following SRP
class Employee {
  constructor(name, salary) {
    this.name = name;
    this.salary = salary;
  }

  calculateSalary() {
    // Calculate employee's salary
  }
}

class DatabaseHandler {
  saveToDatabase(employee) {
    // Save employee data to the database
  }
}


```

### 2. Open/Closed Principle (OCP):

This principle suggests that software entities (e.g., classes, modules, functions) should be open for extension but closed for modification. In other words, you should be able to add new functionality without changing existing code.

Example in JavaScript:

```javascript
// Not following OCP
class Rectangle {
  constructor(width, height) {
    this.width = width;
    this.height = height;
  }
}

class AreaCalculator {
  calculateArea(rectangle) {
    return rectangle.width * rectangle.height;
  }
}

// To add support for circles, you'd have to modify AreaCalculator.


```

```javascript
// Following OCP
class Shape {
  area() {}
}

class Rectangle extends Shape {
  constructor(width, height) {
    super();
    this.width = width;
    this.height = height;
  }

  area() {
    return this.width * this.height;
  }
}

class Circle extends Shape {
  constructor(radius) {
    super();
    this.radius = radius;
  }

  area() {
    return Math.PI * this.radius ** 2;
  }
}


```
### 3. Liskov Substitution Principle (LSP):

This principle states that objects of a superclass should be replaceable with objects of a subclass without affecting the correctness of the program.

Example in JavaScript:

```javascript
// Not following LSP
class Bird {
  fly() {}
}

class Ostrich extends Bird {
  // Ostriches can't fly, so this method is inappropriate.
  fly() {
    throw new Error("Ostriches can't fly");
  }
}

// Following LSP
class Bird {
  move() {}
}

class Sparrow extends Bird {
  move() {
    // Implement flying behavior
  }
}

class Ostrich extends Bird {
  move() {
    // Implement walking behavior
  }
}


```
### 4 Interface Segregation Principle (ISP):
This principle suggests that a class should not be forced to implement interfaces it doesn't use. It encourages the creation of smaller, more focused interfaces.

Example in JavaScript:

```javascript
// Not following ISP
class Worker {
  work() {}
  eat() {}
}

// A manager doesn't need to implement the "work" method.
class Manager extends Worker {
  eat() {}
}

// Following ISP
class Workable {
  work() {}
}

class Eatable {
  eat() {}
}

class Worker implements Workable, Eatable {
  work() {
    // Implement work behavior
  }

  eat() {
    // Implement eat behavior
  }
}

class Manager implements Eatable {
  eat() {
    // Implement eat behavior
  }
}


```
### 5.Dependency Inversion Principle (DIP):

This principle states that high-level modules should not depend on low-level modules. Both should depend on abstractions. Additionally, abstractions should not depend on details; details should depend on abstractions.

Example in JavaScript:

```javascript
// Not following DIP
class LightBulb {
  turnOn() {}
  turnOff() {}
}

class Switch {
  constructor(bulb) {
    this.bulb = bulb;
  }

  operate() {
    // Operate the bulb
  }
}

// Following DIP
class Switchable {
  turnOn() {}
  turnOff() {}
}

class LightBulb implements Switchable {
  turnOn() {
    // Implement turning on behavior
  }

  turnOff() {
    // Implement turning off behavior
  }
}

class Switch {
  constructor(device) {
    this.device = device;
  }

  operate() {
    this.device.turnOn();
    this.device.turnOff();
  }
}


```





## 8 desigh patterns
- Factory
- Builder
- Singleton
- Observer
- Iterator
- Strategy
- Adapter
- Facade
TODO


## 20 System design concepts

Watch: [20 System Design Concepts Explained in 10 Minutes by NetCode](https://www.youtube.com/watch?v=i53Gi_K3o7I)

- Vertical Scaling
- Horizontal Scaling
- Load Balancers
- Content Delivery Networks
- Caching
- IP Address
- TCP / IP
- IP Address
- Domain Name System
- HTTP
- REST
- GraphQL
- gRPC
- WebSockets
- SQL
- ACID
- NoSQL
- Sharding
- Replication
- CAP Theorem
- Message Queues

### Using Software developers System Design knowledge write a system design for creating Word Online as a softwaree as a service?


1. Frontend (Client-Side):
   - Web Application: Built using modern JavaScript frameworks like React.js or Vue.js. This will be the user interface where users can create, edit, and view documents.
   - Real-Time Updates: Use WebSockets for real-time updates and collaboration between multiple users on the same document.
   - Offline Support: Implement Service Workers for offline support and document editing.

2. Backend (Server-Side):
   - RESTful API: Develop a RESTful API using Node.js/Express.js or Django/Flask for handling client requests.
   - Authentication & Authorization: Implement OAuth for user authentication and JWT (JSON Web Tokens) for secure information exchange.
   - Real-Time Collaboration: Use Operational Transformation or Conflict-free Replicated Data Types (CRDTs) algorithms to handle real-time collaboration.

3. Database:
   - Document Storage: Store the documents in a NoSQL database like MongoDB or CouchDB due to their flexible schema and scalability.
   - User Data: Store user data in a SQL database like PostgreSQL or MySQL.

4. Storage:
   - Use cloud storage services like AWS S3 or Azure Blob Storage for storing media files, document exports, etc.

5. Search:
   - Implement ElasticSearch for providing efficient full-text search functionality across documents.

6. Microservices:
   - Consider a microservices architecture for independent scaling of different functionalities like user management, document management, collaboration service, etc.

7. Deployment & Scaling:
   - Use Docker for containerization and Kubernetes for orchestration to ensure the application is scalable and resilient.
   - Deploy the application on a cloud platform like AWS, Google Cloud, or Azure.

8. Security:
   - Ensure all data is encrypted at rest and in transit.
   - Regularly update and patch systems to protect against known vulnerabilities.


### How would you design a distributed cache?

1. **Cache Nodes:**
   - The cache is divided into multiple nodes, each responsible for storing a portion of the cache data.
   - Each node can be a separate machine or process.

2. **Data Distribution:**
   - Use consistent hashing to distribute data across different nodes. This minimizes re-distribution of data when nodes are added or removed.

3. **Data Replication:**
   - To ensure high availability and fault tolerance, replicate each data item on multiple cache nodes.
   - Use strategies like Read-Repair or Anti-Entropy to keep the replicas synchronized.

4. **Cache Eviction Policy:**
   - Implement an eviction policy like LRU (Least Recently Used) or LFU (Least Frequently Used) to decide which items to remove when the cache is full.

5. **Cache Coherency:**
   - If the cache is a write-through cache, ensure that writes to the cache are immediately written to the backing store.
   - If the cache is a write-back cache, use a strategy like periodic write-back or write-back on eviction.

6. **Partition Tolerance:**
   - The system should be able to function even if some of the nodes are down or slow. This can be achieved by using techniques like consistent hashing and data replication.

7. **Concurrency Control:**
   - Use locks or optimistic concurrency control mechanisms to handle concurrent reads and writes to the same data item.

8. **Monitoring and Auto-Recovery:**
   - Monitor the health of cache nodes and implement auto-recovery mechanisms to handle node failures.

### Using Software developers System Design knowledge write a system design for creating a tic tac toe game?

1. **Game Logic:**
   - Implement the game logic using a 3x3 matrix to represent the game board. Each cell in the matrix can be empty, 'X', or 'O'.
   - The game starts with an empty board and the 'X' player.
   - Players take turns to place their symbol ('X' or 'O') in an empty cell.
   - The game ends when one player has three of their symbols in a row, column, or diagonal, or when all cells are filled (draw).

2. **User Interface (UI):**
   - Create a simple UI using HTML/CSS/JavaScript to display the game board and get user inputs.
   - The UI should update in real-time as players make their moves.

3. **Backend Server:**
   - If it's a multiplayer game over the network, you'll need a backend server.
   - The server can be implemented using Node.js/Express.js or other backend technologies.
   - The server receives move updates from each client and broadcasts them to all other clients.

4. **Networking:**
   - Use WebSockets for real-time bidirectional communication between the clients and the server.

5. **Game State Management:**
   - The game state includes the current board state and the next player.
   - In a single-player game, this can be managed on the client-side.
   - In a multiplayer networked game, this can be managed on the server-side and synchronized with all clients.

6. **AI Player (Optional):**
   - If it's a single-player game against the computer, implement an AI player.
   - The AI can be as simple as choosing random empty cells, or as complex as using Minimax algorithm for perfect play.

7. **Testing:**
   - Unit tests should be written to test the game logic.


