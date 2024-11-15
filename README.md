In Kotlin, you can implement a **LinkedList** as a custom data structure, or you can use the built-in `LinkedList` from the Java standard library, which is part of the `java.util` package. However, if you want to learn how to implement a custom linked list in Kotlin, I’ll guide you through creating a simple **Singly LinkedList** implementation. 

### 1. **Singly LinkedList Implementation** in Kotlin

A **singly linked list** is a linear data structure where each element (node) contains a data value and a reference (link) to the next node in the sequence. The list is traversed starting from the head node and ends when we reach a node that has no next node (i.e., the last node points to `null`).

#### Basic Components:
- **Node**: A single unit containing data and a reference (link) to the next node.
- **LinkedList**: A container for managing nodes, supporting operations like adding, removing, and traversing nodes.

### Step-by-Step Implementation

#### 1. Define the Node class
Each node in the linked list holds a `data` value and a reference (`next`) to the next node.

```kotlin
// Node class for a singly linked list
data class Node<T>(var data: T, var next: Node<T>? = null)
```

- `data`: Stores the value of the node.
- `next`: Points to the next node in the list. It's nullable because the last node will point to `null`.

#### 2. Define the LinkedList class
The `LinkedList` class manages the nodes and offers operations like adding, removing, and displaying elements.

```kotlin
// LinkedList class with basic operations
class LinkedList<T> {
    private var head: Node<T>? = null  // The head of the list

    // Add a new node to the end of the list
    fun add(data: T) {
        val newNode = Node(data)

        // If the list is empty, set the new node as the head
        if (head == null) {
            head = newNode
        } else {
            var current = head
            // Traverse to the last node
            while (current?.next != null) {
                current = current.next
            }
            // Set the last node's next reference to the new node
            current?.next = newNode
        }
    }

    // Remove the first occurrence of a node with the given data
    fun remove(data: T) {
        if (head == null) return  // If the list is empty, do nothing

        // If the head node contains the data, remove it
        if (head?.data == data) {
            head = head?.next
            return
        }

        var current = head
        // Traverse the list to find the node to remove
        while (current?.next != null) {
            if (current.next?.data == data) {
                // Remove the node by bypassing it
                current.next = current.next?.next
                return
            }
            current = current.next
        }
    }

    // Print all elements in the list
    fun printList() {
        var current = head
        while (current != null) {
            print("${current.data} -> ")
            current = current.next
        }
        println("null")
    }

    // Check if the list contains a specific value
    fun contains(data: T): Boolean {
        var current = head
        while (current != null) {
            if (current.data == data) {
                return true
            }
            current = current.next
        }
        return false
    }

    // Get the size of the linked list
    fun size(): Int {
        var current = head
        var count = 0
        while (current != null) {
            count++
            current = current.next
        }
        return count
    }
}
```

#### Key Operations:
1. **Add**: Adds a new element at the end of the list.
2. **Remove**: Removes the first occurrence of the specified data.
3. **Print**: Prints all elements in the list in a readable format.
4. **Contains**: Checks if the list contains a specific element.
5. **Size**: Returns the size (number of elements) in the linked list.

### 3. Example Usage of the LinkedList

Now that we've defined the `LinkedList` class, let’s see how we can use it in a program:

```kotlin
fun main() {
    val linkedList = LinkedList<Int>()

    // Add elements to the linked list
    linkedList.add(1)
    linkedList.add(2)
    linkedList.add(3)
    linkedList.add(4)

    println("Original List:")
    linkedList.printList()  // Output: 1 -> 2 -> 3 -> 4 -> null

    // Remove an element
    linkedList.remove(3)
    println("After removing 3:")
    linkedList.printList()  // Output: 1 -> 2 -> 4 -> null

    // Check if an element exists
    println("List contains 2: ${linkedList.contains(2)}")  // Output: true
    println("List contains 3: ${linkedList.contains(3)}")  // Output: false

    // Get the size of the list
    println("Size of the list: ${linkedList.size()}")  // Output: 3
}
```

### 4. Explanation of Key Methods:
- **add(data: T)**: Adds a new node to the end of the linked list. It first checks if the list is empty (if `head` is `null`), and if so, it sets the new node as the head. Otherwise, it traverses to the last node and sets its `next` reference to the new node.
  
- **remove(data: T)**: Removes the first occurrence of the node with the specified `data`. If the data is in the head node, it simply updates the `head`. Otherwise, it traverses the list to find and remove the node.
  
- **printList()**: Traverses the list starting from the head and prints each node’s `data` followed by an arrow (`->`), and finally prints `null` to signify the end of the list.
  
- **contains(data: T)**: Traverses the list to check if any node contains the specified `data`. Returns `true` if found, otherwise `false`.
  
- **size()**: Counts the number of nodes in the list by traversing from the head and incrementing a counter until the end of the list.

### 5. Doubly Linked List (Optional Extension)

A **doubly linked list** is another variant where each node contains references to both the next and the previous node. This allows traversal in both directions.

Here's a basic structure for a **doubly linked list**:

```kotlin
// Node class for a doubly linked list
data class DoublyNode<T>(
    var data: T,
    var next: DoublyNode<T>? = null,
    var prev: DoublyNode<T>? = null
)

// Doubly LinkedList class with basic operations
class DoublyLinkedList<T> {
    private var head: DoublyNode<T>? = null
    private var tail: DoublyNode<T>? = null

    // Add element to the end
    fun add(data: T) {
        val newNode = DoublyNode(data)
        if (tail == null) {
            head = newNode
            tail = newNode
        } else {
            tail?.next = newNode
            newNode.prev = tail
            tail = newNode
        }
    }

    // Print list from head to tail
    fun printList() {
        var current = head
        while (current != null) {
            print("${current.data} <-> ")
            current = current.next
        }
        println("null")
    }

    // Print list from tail to head
    fun printReverse() {
        var current = tail
        while (current != null) {
            print("${current.data} <-> ")
            current = current.prev
        }
        println("null")
    }
}
```

### Conclusion:
- **Singly Linked List**: Each node contains data and a reference to the next node.
- **Doubly Linked List**: Each node contains data and references to both the next and previous nodes, making it easier to traverse in both directions.

Both implementations allow you to perform various operations like adding elements, removing elements, and traversing the list. Depending on your requirements, you may choose a singly or doubly linked list.
