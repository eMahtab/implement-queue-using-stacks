# Implement Queue using Stacks
## https://leetcode.com/problems/implement-queue-using-stacks


## Implementation : 2 Stacks

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
## Implementation : 2 Stacks (Improvements)
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
