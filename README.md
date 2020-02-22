# Implement Queue using Stacks
## https://leetcode.com/problems/implement-queue-using-stacks


## Implementation :

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

