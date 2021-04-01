# LinkedList

```swift

import UIKit

public class Node<T> {
  var value: T
  var next: Node?
  weak var previous: Node?

  public init(value: T) {
    self.value = value
  }
}


class LinkedList<T> {
    
    private var head: Node<T>?
    
    public var isEmpty: Bool {
        return head == nil
    }
    
    public var first: Node<T>? {
      return head
    }
    
    public var last: Node<T>? {
        guard var node = head else {
            return nil
        }
        
        while let next = node.next {
            node = next
        }
        return node
    }
    
    // How to append node in linked list
    public func append(data: T) {
        let newNode = Node(value: data)
        if let lastNode = last {
            newNode.previous = lastNode
            lastNode.next = newNode
        } else {
            head = newNode
        }
    }
    
    // count total node in linked list
    public var count: Int {
        guard var node = head else {
            return 0
        }
        
        var counter = 1
        while let next = node.next {
            node = next
            counter += 1
        }
        return counter
    }
    
    // print linkedList
    public var print: String {
        var s = "["
        var node = head
        while node != nil {
            s += "\(node!.value)"
            node = node?.next
            if node != nil {
                s += ", "
            }
        }
        
        return s + "]"
        
    }
    
    // get node from slected index
    public func node(atIndex index: Int) -> Node<T> {
        if index == 0 {
            return head!
        } else {
            var node = head!.next
            for _ in 1..<index {
                node = node?.next
                if node == nil {
                    break
                }
            }
            return node!
        }
    }
    
    // insert node at give index
    func insert(at index: Int, value: T) {
        let newNode = Node(value: value)
        
        if index == 0 {
            newNode.next = head
            head?.previous = newNode
            head = newNode
        } else {
            let previousNode = self.node(atIndex: index - 1)
            let nextNode = previousNode.next
            newNode.previous = previousNode
            newNode.next = nextNode
            previousNode.next = newNode
            nextNode?.previous = newNode
        }
    }
    
    // remove give node
    public func remove(node: Node<T>) -> T {
        
        let previousNode = node.previous
        let nextNode = node.next
        
        if let previousNode = previousNode {
            previousNode.next = nextNode
            
        } else {
            head = nextNode
        }
        
        nextNode?.previous = previousNode
        node.previous = nil
        node.next = nil
        return node.value
        
    }
    
    // remove node from given index
    public func remove(at index: Int) -> T {
        let node = self.node(atIndex: index)
        return remove(node: node)
    }
    
    // Finding middle node in a Linked List in O(N) time and Single Pass
    public func middleNode() -> Node<T>? {
        var fastPointer: Node? = head
        var slowPointer: Node? = head
        
        while fastPointer != nil && fastPointer?.next != nil {
            slowPointer = slowPointer?.next
            fastPointer = fastPointer?.next?.next
        }
        
        return slowPointer
    }
}


let list = LinkedList<String>()
list.isEmpty
list.count
list.append(data: "Hello")
list.isEmpty
list.append(data: "Hi")
list.append(data: "How")
list.count
list.print
list.node(atIndex: 2).value
list.insert(at: 1, value: "Pushpank")
list.print
list.remove(at: 2)
list.append(data: "j")
list.append(data: "k")
list.append(data: "l")

list.print
list.print
list.count
list.middleNode()?.value

```
