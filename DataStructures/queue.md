## Queue

![Alt text](queue1.png)
Being an interface the queue needs a concrete class for the declaration and the most common classes are the **PriorityQueue** and **LinkedList** in Java. Note that neither of these implementations is thread-safe. **PriorityBlockingQueue** is one alternative implementation if the thread-safe implementation is needed.

```java
public interface Queue extends Collection

Queue<T> queue = new PriorityQueue<T>();

Queue<T> queue = new LinkedList<>();

// add element at rear of the queue. If the queue is full, it throws an exception.
queue.add(obj);

// add element at rear of the queue. If the queue is full, it returns false.
queue.offer(obj);

// remove and retrieve front element from the queue. If the queue is empty, it throws an exception.
queue.remove();

// remove and retrieve front element from the queue. If the queue is empty, it returns null.
queue.poll();

// retrieve element at the front of the queue without removing it. If the queue is empty, it throws an exception.
queue.element();

// retrieve element at the front of the queue without removing it. If the queue is empty, it returns null.
queue.peek();
```

**The Queue interface is implemented by several classes in Java, including LinkedList, ArrayDeque, and PriorityQueue. Each of these classes provides different implementations of the queue interface, with different performance characteristics and features.**
