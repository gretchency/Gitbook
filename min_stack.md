# Min Stack
http://www.lintcode.com/en/problem/min-stack/

Implement a stack with min() function, which will return the smallest number in the stack.

It should support push, pop and min operation all in O(1) cost.

维护一个minStack 在push第一个stack的时候把他的大小关系存进minStack 最小的放最上面

二刷
* minStack记录每层stack的最小值， 同时pop()出去

```java
public class MinStack {

    Stack<Integer> stack = new Stack<>();
    Stack<Integer> minStack = new Stack<>();
    
    /** initialize your data structure here. */
    public MinStack() {
        
    }
    
    public void push(int x) {
        stack.push(x);
        if (minStack.isEmpty()) {
            minStack.push(x);
        } else {
            if (minStack.peek() < x) {
                minStack.push(minStack.peek());
            } else {
                minStack.push(x);
            }
        }
    }
    
    public void pop() {
        stack.pop();
        minStack.pop();
    }
    
    public int top() {
        return stack.peek();
    }
    
    public int getMin() {
        return minStack.peek();
    }
}
```
```java
public class MinStack {
    
    private Stack<Integer> stack;
    private Stack<Integer> minStack;
    
    public MinStack() {
        // do initialize if necessary
        stack = new Stack<Integer>();
        minStack = new Stack<Integer>();
        
    }

    public void push(int number) {
        // 维护一个最小的在最上面的minStack
        stack.push(number);
        if (minStack.empty()) {
            minStack.push(number);
        //****注意这里：相同的最小值也应该放进minStack
        } else if (minStack.peek() >= number) {
            minStack.push(number);
        }
    }

    public int pop() {
        // 如果一样，minStack的也要扔掉
        //**要用equals 因为要考虑null的比较
        if (stack.peek().equals(minStack.peek())) {
            minStack.pop();
        }
        
        return stack.pop();
    }

    public int min() {
        return minStack.peek();
    }
}

```


Related Problem:

http://www.lintcode.com/en/problem/implement-queue-by-two-stacks/#
