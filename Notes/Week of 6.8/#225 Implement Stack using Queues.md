# #225 Implement Stack using Queues

## Please check the problem description [here](https://leetcode.com/problems/path-sum/).

## First Impressions
> 1. Using only 1 queue, for pop, dequeue every element ahead of the tail and add them back, and dequeue the first element

## One Queue (Push: $\mathcal{O}(1)$, Pop: $\mathcal{O}(n)$)

```Java
    class MyStack {
    Queue<Integer> queue;

    /** Initialize your data structure here. */
    public MyStack() {
        this.queue = new LinkedList<Integer>();
        
    }
    
    /** Push element x onto stack. */
    public void push(int x) {
        this.queue.add(x);
    }
    
    /** Removes the element on top of the stack and returns that element. */
    public int pop() {
        for(int i = 0; i < this.queue.size()-1; i++){
            int elt = this.queue.poll();
            this.queue.add(elt);
        }
        return this.queue.poll();
    }
    
    /** Get the top element. */
    public int top() {
        for(int i = 0; i < this.queue.size()-1; i++){
            int elt = this.queue.poll();
            this.queue.add(elt);
        }
        int result = this.queue.poll();
        this.queue.add(result);
        return result;
    }
    
    /** Returns whether the stack is empty. */
    public boolean empty() {
        return (this.queue.size() == 0);
    }
}

/**
 * Your MyStack object will be instantiated and called as such:
 * MyStack obj = new MyStack();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.top();
 * boolean param_4 = obj.empty();
 */
```
`Queue<>()` interface of Java:  

Implementation: 
* __LinkedList__
* __ArrayBlockingQueue__
* __PriorityQueue__

Methods:
* `add()`: add the element to the tail
* `poll()`: dequeuing the head element, return `null` if empty
* `peek()`: returning the head element, return `null` if empty
* `element()`: same as `peek()`, raise `NoSuchElementException` if empty.
* `size()`: returning the no. of elements
* `remove()`: dequeuing the head element, raise `NoSuchElementException` if empty

## Two Queues (Push: $\mathcal{O}(1)$, Pop: $\mathcal{O}(n)$)

```Java
    class MyStack {
    private Queue<Integer> q1;
    private Queue<Integer> q2;
    private int top;

    /** Initialize your data structure here. */
    public MyStack() {
        this.q1 = new LinkedList<>();
        this.q2 = new LinkedList<>();
    }
    
    /** Push element x onto stack. */
    public void push(int x) {
        q1.add(x);
        top = x;
    }
    
    /** Removes the element on top of the stack and returns that element. */
    public int pop() {
        while(this.q1.size()>1){
            top = q1.remove();
            q2.add(top);
        }
        int result = this.q1.remove();
        Queue<Integer> temp = this.q1;
        this.q1 = this.q2;
        this.q2 = temp;
        return result;
    }
    
    /** Get the top element. */
    public int top() {
        return top;
    }
    
    /** Returns whether the stack is empty. */
    public boolean empty() {
        return this.q1.isEmpty();
    }
}

/**
 * Your MyStack object will be instantiated and called as such:
 * MyStack obj = new MyStack();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.top();
 * boolean param_4 = obj.empty();
 */
```

Use two queues, one main `q1` for representation, `q2` for storing elements before top elements.

> Use a top variable to store top after push.