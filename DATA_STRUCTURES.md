# Data Structure Interview Questions

1. **Arrays and Strings:**
   - Implement an algorithm to find the first non-repeated character in a string.
   - How would you reverse an array in place?
   - Given two strings, write a method to decide if one is a permutation of the other.

2. **Linked Lists:**
   - Implement an algorithm to find the kth element from the end of a singly linked list.
   - Write code to remove duplicates from an unsorted linked list.
   - How would you detect if a linked list has a cycle? How would you remove the cycle?

3. **Stacks and Queues:**
   - Implement a stack that supports push, pop, peek, and retrieving the minimum element in constant time.
   - Implement a queue using two stacks.
   - Design a data structure that supports push, pop, top, and retrieving the minimum element in constant time.

4. **Trees and Graphs:**
   - Implement a binary search tree and write functions for insertion, deletion, and searching.
   - Write an algorithm to find the lowest common ancestor of two nodes in a binary tree.
   - Implement depth-first search (DFS) and breadth-first search (BFS) for a graph.

5. **Hash Tables:**
   - Design and implement a hash map from scratch.
   - Given an array of integers, return indices of the two numbers such that they add up to a specific target.
   - How would you find all pairs in an array that sum up to a specific value?

6. **Sorting and Searching:**
   - Implement quicksort and explain its algorithmic complexity.
   - Describe the difference between linear search and binary search. When would you use each?

7. **Dynamic Programming:**
   - Implement the Fibonacci sequence using dynamic programming.
   - Solve the "knapsack problem" using dynamic programming.
   - Write a function to compute the longest common subsequence of two strings.




# Some of Solved Examples

### 1. Arrays and Strings

#### Example 1: Finding the First Non-Repeated Character

**Problem Statement:** Implement an algorithm to find the first non-repeated character in a string.

**PHP Example:**
```php
function firstNonRepeatedChar($str) {
    $charCount = [];
    
    // Count occurrences of each character
    for ($i = 0; $i < strlen($str); $i++) {
        $char = $str[$i];
        if (isset($charCount[$char])) {
            $charCount[$char]++;
        } else {
            $charCount[$char] = 1;
        }
    }
    
    // Find the first character with count 1
    for ($i = 0; $i < strlen($str); $i++) {
        $char = $str[$i];
        if ($charCount[$char] === 1) {
            return $char;
        }
    }
    
    return null; // No non-repeated character found
}

// Example usage:
$str = "aabbcdeeff";
echo "First non-repeated character: " . firstNonRepeatedChar($str); // Output: "c"
```

**Python Example:**
```python
def first_non_repeated_char(string):
    char_count = {}
    
    # Count occurrences of each character
    for char in string:
        if char in char_count:
            char_count[char] += 1
        else:
            char_count[char] = 1
    
    # Find the first character with count 1
    for char in string:
        if char_count[char] == 1:
            return char
    
    return None  # No non-repeated character found

# Example usage:
string = "aabbcdeeff"
print("First non-repeated character:", first_non_repeated_char(string))  # Output: "c"
```

#### Example 2: Reversing an Array In-Place

**Problem Statement:** Write a function to reverse an array in place.

**PHP Example:**
```php
function reverseArray(&$arr) {
    $left = 0;
    $right = count($arr) - 1;
    
    while ($left < $right) {
        // Swap elements at $left and $right
        $temp = $arr[$left];
        $arr[$left] = $arr[$right];
        $arr[$right] = $temp;
        
        $left++;
        $right--;
    }
}

// Example usage:
$arr = [1, 2, 3, 4, 5];
reverseArray($arr);
print_r($arr);  // Output: [5, 4, 3, 2, 1]
```

**Python Example:**
```python
def reverse_array(arr):
    left, right = 0, len(arr) - 1
    
    while left < right:
        # Swap elements at left and right indices
        arr[left], arr[right] = arr[right], arr[left]
        left += 1
        right -= 1

# Example usage:
arr = [1, 2, 3, 4, 5]
reverse_array(arr)
print(arr)  # Output: [5, 4, 3, 2, 1]
```

### 2. Linked Lists

#### Example 1: Finding the Kth Element from the End of a Singly Linked List

**Problem Statement:** Implement an algorithm to find the kth element from the end of a singly linked list.

**PHP Example:**
```php
class ListNode {
    public $val;
    public $next;

    function __construct($val = 0, $next = null) {
        $this->val = $val;
        $this->next = $next;
    }
}

function kthFromEnd($head, $k) {
    $slow = $head;
    $fast = $head;
    
    // Move fast pointer k steps ahead
    for ($i = 0; $i < $k; $i++) {
        if ($fast === null) {
            return null;  // List length is less than k
        }
        $fast = $fast->next;
    }
    
    // Move both pointers until fast reaches end
    while ($fast !== null) {
        $slow = $slow->next;
        $fast = $fast->next;
    }
    
    return $slow->val;
}

// Example usage:
$list = new ListNode(1);
$list->next = new ListNode(2);
$list->next->next = new ListNode(3);
$list->next->next->next = new ListNode(4);
$list->next->next->next->next = new ListNode(5);

$k = 2;
echo "Value at $k th from end: " . kthFromEnd($list, $k);  // Output: 4
```

**Python Example:**
```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

def kth_from_end(head, k):
    slow = head
    fast = head
    
    # Move fast pointer k steps ahead
    for _ in range(k):
        if not fast:
            return None  # List length is less than k
        fast = fast.next
    
    # Move both pointers until fast reaches end
    while fast:
        slow = slow.next
        fast = fast.next
    
    return slow.val

# Example usage:
list = ListNode(1, ListNode(2, ListNode(3, ListNode(4, ListNode(5)))))
k = 2
print(f"Value at {k}th from end:", kth_from_end(list, k))  # Output: 4
```

### 3. Stacks and Queues

#### Example 1: Implementing a Stack with Min Operation

**Problem Statement:** Implement a stack that supports push, pop, peek, and retrieving the minimum element in constant time.

**PHP Example:**
```php
class MinStack {
    private $stack;
    private $minStack;
    
    function __construct() {
        $this->stack = [];
        $this->minStack = [];
    }
    
    function push($val) {
        array_push($this->stack, $val);
        
        if (empty($this->minStack) || $val <= end($this->minStack)) {
            array_push($this->minStack, $val);
        }
    }
    
    function pop() {
        $val = array_pop($this->stack);
        
        if ($val === end($this->minStack)) {
            array_pop($this->minStack);
        }
        
        return $val;
    }
    
    function top() {
        return end($this->stack);
    }
    
    function getMin() {
        return end($this->minStack);
    }
}

// Example usage:
$stack = new MinStack();
$stack->push(3);
$stack->push(5);
$stack->push(2);
echo "Min element: " . $stack->getMin() . "\n";  // Output: 2
$stack->pop();
echo "Top element: " . $stack->top() . "\n";      // Output: 5
echo "Min element: " . $stack->getMin() . "\n";  // Output: 3
```

**Python Example:**
```python
class MinStack:
    def __init__(self):
        self.stack = []
        self.min_stack = []
    
    def push(self, val):
        self.stack.append(val)
        
        if not self.min_stack or val <= self.min_stack[-1]:
            self.min_stack.append(val)
    
    def pop(self):
        val = self.stack.pop()
        
        if val == self.min_stack[-1]:
            self.min_stack.pop()
        
        return val
    
    def top(self):
        return self.stack[-1]
    
    def get_min(self):
        return self.min_stack[-1]

# Example usage:
stack = MinStack()
stack.push(3)
stack.push(5)
stack.push(2)
print("Min element:", stack.get_min())  # Output: 2
stack.pop()
print("Top element:", stack.top())      # Output: 5
print("Min element:", stack.get_min())  # Output: 3
```

### 4. Trees and Graphs

#### Example 1: Implementing a Binary Search Tree

**Problem Statement:** Implement a binary search tree (BST) and write functions for insertion, deletion, and searching.

**PHP Example:**
```php
class TreeNode {
    public $val;
    public $left;
    public $right;

    function __construct($val = 0, $left = null, $right = null) {
        $this->val = $val;
        $this->left = $left;
        $this->right = $right;
    }
}

class BST {
    private $root;
    
    function __construct() {
        $this->root = null;
    }
    
    function insert($val) {
        $newNode = new TreeNode($val);
        
        if ($this->root === null) {
            $this->root = $newNode;
            return;
        }
        
        $current = $this->root;
        
        while (true) {
            if ($val < $current->val) {
                if ($current->left === null) {


                    $current->left = $newNode;
                    break;
                } else {
                    $current = $current->left;
                }
            } else {
                if ($current->right === null) {
                    $current->right = $newNode;
                    break;
                } else {
                    $current = $current->right;
                }
            }
        }
    }
    
    function search($val) {
        $current = $this->root;
        
        while ($current !== null) {
            if ($val === $current->val) {
                return true;
            } elseif ($val < $current->val) {
                $current = $current->left;
            } else {
                $current = $current->right;
            }
        }
        
        return false;
    }
    
    function delete($val) {
        $this->root = $this->deleteNode($this->root, $val);
    }
    
    private function deleteNode($root, $val) {
        if ($root === null) {
            return $root;
        }
        
        if ($val < $root->val) {
            $root->left = $this->deleteNode($root->left, $val);
        } elseif ($val > $root->val) {
            $root->right = $this->deleteNode($root->right, $val);
        } else {
            // Case 1: No child or only one child
            if ($root->left === null) {
                return $root->right;
            } elseif ($root->right === null) {
                return $root->left;
            }
            
            // Case 2: Node with two children
            $root->val = $this->minValue($root->right);
            $root->right = $this->deleteNode($root->right, $root->val);
        }
        
        return $root;
    }
    
    private function minValue($node) {
        $minVal = $node->val;
        
        while ($node->left !== null) {
            $minVal = $node->left->val;
            $node = $node->left;
        }
        
        return $minVal;
    }
}

// Example usage:
$bst = new BST();
$bst->insert(5);
$bst->insert(3);
$bst->insert(7);
$bst->insert(2);
$bst->insert(4);
$bst->insert(6);
$bst->insert(8);

echo "Search for 4: " . ($bst->search(4) ? "Found\n" : "Not Found\n");  // Output: Found
$bst->delete(3);
echo "Search for 3: " . ($bst->search(3) ? "Found\n" : "Not Found\n");  // Output: Not Found
```

**Python Example:**
```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class BST:
    def __init__(self):
        self.root = None
    
    def insert(self, val):
        new_node = TreeNode(val)
        
        if not self.root:
            self.root = new_node
            return
        
        current = self.root
        
        while True:
            if val < current.val:
                if not current.left:
                    current.left = new_node
                    break
                else:
                    current = current.left
            else:
                if not current.right:
                    current.right = new_node
                    break
                else:
                    current = current.right
    
    def search(self, val):
        current = self.root
        
        while current:
            if val == current.val:
                return True
            elif val < current.val:
                current = current.left
            else:
                current = current.right
        
        return False
    
    def delete(self, val):
        self.root = self._delete_node(self.root, val)
    
    def _delete_node(self, root, val):
        if not root:
            return root
        
        if val < root.val:
            root.left = self._delete_node(root.left, val)
        elif val > root.val:
            root.right = self._delete_node(root.right, val)
        else:
            # Case 1: No child or only one child
            if not root.left:
                return root.right
            elif not root.right:
                return root.left
            
            # Case 2: Node with two children
            root.val = self._min_value(root.right)
            root.right = self._delete_node(root.right, root.val)
        
        return root
    
    def _min_value(self, node):
        min_val = node.val
        
        while node.left:
            min_val = node.left.val
            node = node.left
        
        return min_val

# Example usage:
bst = BST()
bst.insert(5)
bst.insert(3)
bst.insert(7)
bst.insert(2)
bst.insert(4)
bst.insert(6)
bst.insert(8)

print("Search for 4:", "Found" if bst.search(4) else "Not Found")  # Output: Found
bst.delete(3)
print("Search for 3:", "Found" if bst.search(3) else "Not Found")  # Output: Not Found
```

### 5. Hash Tables

#### Example 1: Designing a Hash Map

**Problem Statement:** Design and implement a hash map from scratch.

**PHP Example:**
```php
class MyHashMap {
    private $data;
    
    function __construct() {
        $this->data = [];
    }
    
    function put($key, $value) {
        $this->data[$key] = $value;
    }
    
    function get($key) {
        return isset($this->data[$key]) ? $this->data[$key] : -1;
    }
    
    function remove($key) {
        unset($this->data[$key]);
    }
}

// Example usage:
$map = new MyHashMap();
$map->put(1, "A");
$map->put(2, "B");
echo "Value at key 1: " . $map->get(1) . "\n";  // Output: "A"
$map->remove(2);
echo "Value at key 2: " . $map->get(2) . "\n";  // Output: -1 (not found)
```

**Python Example:**
```python
class MyHashMap:
    def __init__(self):
        self.data = {}
    
    def put(self, key, value):
        self.data[key] = value
    
    def get(self, key):
        return self.data.get(key, -1)
    
    def remove(self, key):
        if key in self.data:
            del self.data[key]

# Example usage:
map = MyHashMap()
map.put(1, "A")
map.put(2, "B")
print("Value at key 1:", map.get(1))  # Output: "A"
map.remove(2)
print("Value at key 2:", map.get(2))  # Output: -1 (not found)
```

### 6. Sorting and Searching

#### Example 1: Implementing Quicksort

**Problem Statement:** Implement quicksort and explain its algorithmic complexity.

**PHP Example:**
```php
function quicksort(&$arr, $left, $right) {
    if ($left < $right) {
        $pivot = partition($arr, $left, $right);
        
        quicksort($arr, $left, $pivot - 1);
        quicksort($arr, $pivot + 1, $right);
    }
}

function partition(&$arr, $left, $right) {
    $pivot = $arr[$right];
    $i = $left - 1;
    
    for ($j = $left; $j < $right; $j++) {
        if ($arr[$j] < $pivot) {
            $i++;
            // Swap arr[$i] and arr[$j]
            $temp = $arr[$i];
            $arr[$i] = $arr[$j];
            $arr[$j] = $temp;
        }
    }
    
    // Swap arr[$i + 1] and arr[$right] (pivot)
    $temp = $arr[$i + 1];
    $arr[$i + 1] = $arr[$right];
    $arr[$right] = $temp;
    
    return $i + 1;
}

// Example usage:
$arr = [3, 0, 2, 5, -1, 4, 1];
quicksort($arr, 0, count($arr) - 1);
print_r($arr);  // Output: [-1, 0, 1, 2, 3, 4, 5]
```

**Python Example:**
```python
def quicksort(arr, left, right):
    if left < right:
        pivot = partition(arr, left, right)
        
        quicksort(arr, left, pivot - 1)
        quicksort(arr, pivot + 1, right)

def partition(arr, left, right):
    pivot = arr[right]
    i = left - 1
    
    for j in range(left, right):
        if arr[j] < pivot:
            i += 1
            # Swap arr[i] and arr[j]
            arr[i], arr[j] = arr[j], arr[i]
    
    # Swap arr[i + 1] and arr[right] (pivot)
    arr[i + 1], arr[right] = arr[right], arr[i + 1]
    
    return i + 1

#

 Example usage:
arr = [3, 0, 2, 5, -1, 4, 1]
quicksort(arr, 0, len(arr) - 1)
print(arr)  # Output: [-1, 0, 1, 2, 3, 4, 5]
```

### 7. Dynamic Programming

#### Example 1: Fibonacci Sequence Using Dynamic Programming

**Problem Statement:** Implement the Fibonacci sequence using dynamic programming.

**PHP Example:**
```php
function fibonacci($n) {
    $dp = [];
    $dp[0] = 0;
    $dp[1] = 1;
    
    for ($i = 2; $i <= $n; $i++) {
        $dp[$i] = $dp[$i - 1] + $dp[$i - 2];
    }
    
    return $dp[$n];
}

// Example usage:
$n = 6;
echo "Fibonacci of $n: " . fibonacci($n);  // Output: 8 (fibonacci sequence: 0, 1, 1, 2, 3, 5, 8)
```

**Python Example:**
```python
def fibonacci(n):
    dp = [0] * (n + 1)
    dp[0] = 0
    dp[1] = 1
    
    for i in range(2, n + 1):
        dp[i] = dp[i - 1] + dp[i - 2]
    
    return dp[n]

# Example usage:
n = 6
print(f"Fibonacci of {n}: {fibonacci(n)}")  # Output: 8 (fibonacci sequence: 0, 1, 1, 2, 3, 5, 8)
```

These examples cover a range of data structures and algorithms commonly asked about in technical interviews. Each example demonstrates the implementation details and usage in both PHP and Python, providing a solid foundation for understanding and practicing these concepts.
