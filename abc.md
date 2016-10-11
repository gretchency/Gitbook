# ABC

What happend after URL

Map function

传入一个Method要求对collection的所有元素执行该method

* 非递归秒了
* 要求写递归，写递归的时候没传入index，这样没法对list取值


```java
public class ABC {
    public List<Integer> map(List<Integer> list, Method function) {
        List<Integer> newList = new ArrayList<>();
        // for (int num: list) {
        //     int newNum = function(num);
        //     newList.add(newNum);
        // }
        // return newList;

        helper(list, newList, function, 0);

        return newList;
    }

    private void helper(List<Integer> list, List<Integer> newList, Method function, int index) {
        if (index == list.size()) {
            return;
        }  

        newList.add(list.get(index));
        helper(list, newList, function, index + 1);
    }
    
    private int function(int a) {
        return a + 1;
    }

    public static void main(String[] args) {
        // TODO Auto-generated method stub

    }

}
```