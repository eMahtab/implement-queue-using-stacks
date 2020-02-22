# Implement Queue using Stacks
## https://leetcode.com/problems/implement-queue-using-stacks

Implement the following operations of a queue using stacks.

1. push(x) -- Push element x to the back of queue.
2. pop() -- Removes the element from in front of queue.
3. peek() -- Get the front element.
4. empty() -- Return whether the queue is empty.

```
Example:

MyQueue queue = new MyQueue();

queue.push(1);
queue.push(2);  
queue.peek();  // returns 1
queue.pop();   // returns 1
queue.empty(); // returns false
```
**Notes:**

1. You must use only standard operations of a stack -- which means only push to top, peek/pop from top, size, and is empty operations are valid.
2. Depending on your language, stack may not be supported natively. You may simulate a stack by using a list or deque (double-ended queue), as long as you use only standard operations of a stack.
3. You may assume that all operations are valid (for example, no pop or peek operations will be called on an empty queue).

## Implementation 1 : 2 Stacks

```java
class MyQueue {

    /** Initialize your data structure here. */
    private Stack<Integer> stack = new Stack<>();
   
    /** Push element x to the back of queue. */
    public void push(int x) {
        stack.push(x);
    }
    
    /** Removes the element from in front of queue and returns that element. */
    public int pop() {
        Stack<Integer> temp = new Stack<>();
        while(!stack.isEmpty()){
            temp.push(stack.pop());
        }
        int top = temp.pop();
        while(!temp.isEmpty()){
            stack.push(temp.pop());
        }
        return top;
    }
    
    /** Get the front element. */
    public int peek() {
        Stack<Integer> temp = new Stack<>();
        while(!stack.isEmpty()){
            temp.push(stack.pop());
        }
        int top = temp.peek();
        while(!temp.isEmpty()){
            stack.push(temp.pop());
        }
        return top;
    }
    
    /** Returns whether the queue is empty. */
    public boolean empty() {
        return stack.isEmpty();
    }
}
```
## Implementation 1 : 2 Stacks (Improvements)
```java
class MyQueue {

    /** Initialize your data structure here. */
    private Stack<Integer> stack = new Stack<>();
    private Stack<Integer> auxiliaryStack = new Stack<>();
    private int front;
    
    /** Push element x to the back of queue. */
    public void push(int x) {
        if(stack.isEmpty())
            front = x;
        stack.push(x);
    }
    
    /** Removes the element from in front of queue and returns that element. */
    public int pop() {
        while(!stack.isEmpty()){
            auxiliaryStack.push(stack.pop());
        }
        int top = auxiliaryStack.pop();
        while(!auxiliaryStack.isEmpty()){ 
            if(stack.isEmpty())
                front = auxiliaryStack.peek();
            stack.push(auxiliaryStack.pop());
        }
        return top;
    }
    
    /** Get the front element. */
    public int peek() {
       return front;
    }
    
    /** Returns whether the queue is empty. */
    public boolean empty() {
        return stack.isEmpty();
    }
}
```

## Implementation 2 : 2 Stacks (Much better approach)
```java
class MyQueue {

    /** Initialize your data structure here. */
    private Stack<Integer> stack = new Stack<>();
    private Stack<Integer> auxiliaryStack = new Stack<>();
    private int front;
    
    /** Push element x to the back of queue. */
    public void push(int x) {
        if(stack.isEmpty())
            front = x;
        stack.push(x);
    }
    
    /** Removes the element from in front of queue and returns that element. */
    public int pop() {
        if (auxiliaryStack.isEmpty()) {
            while (!stack.isEmpty())
              auxiliaryStack.push(stack.pop());
        }
        return auxiliaryStack.pop();  
    }
    
    /** Get the front element. */
    public int peek() {
       if (!auxiliaryStack.isEmpty()) {
            return auxiliaryStack.peek();
        }
       return front;
    }
    
    /** Returns whether the queue is empty. */
    public boolean empty() {
        return stack.isEmpty() && auxiliaryStack.isEmpty();
    }
}

```

# References :
1. https://www.youtube.com/watch?v=Wg8IiY1LbII
2. https://leetcode.com/articles/implement-queue-using-stacks

