# MinStack

```java
//Implement a stack with min() function, which will return the smallest number in the stack.

//It should support push, pop and min operation all in O(1) cost.
public class MinStack {

    private Stack<Integer> stack = new Stack<Integer>();
    private Stack<Integer> minStack = new Stack<Integer>();
    
    public void push(int i) {
        stack.push(i);
        if (minStack.isEmpty()) {
            minStack.push(i);
        }
        if (i <= minStack.peek()) {
            minStack.push(i);
        }
    }
    
    public int pop() {
        if (minStack.peek() == stack.peek()) {
            minStack.pop();
        }
        return stack.pop();
    }
    
    public int min() {
        return minStack.peek();
    }
    
    public static void main(String[] args) {
        // TODO Auto-generated method stub
        MinStack minStack = new MinStack();
        minStack.push(1);
        minStack.push(2);
        minStack.push(3);
        minStack.push(0);

        System.out.println(minStack.min());
        minStack.pop();
        System.out.println(minStack.min());


    }

}
```