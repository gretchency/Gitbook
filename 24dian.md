# 24点

数建list,每次拿两个加减乘除，结果放入res list, 删掉那两数，把res依次加入试是不是24点，都不是就把两数放回，换其他两数

```java
public class TwentyFourPoint {
    public static boolean game(List<Integer> nums) {
        if (nums == null || nums.size() == 0) return false;
        
        return search(nums);
    }
    
    private static boolean search(List<Integer> nums) {
        if(nums.size() == 1) {
            if (nums.get(0) == 24) return true;
            return false;
        }
        
        for(int i = 0; i < nums.size() - 1; i++) {
            for (int j = i + 1; j < nums.size(); j++) {
                int num1 = nums.get(i);
                int num2 = nums.get(j);
                List<Integer> res = new ArrayList<>();
                res.add(num1 + num2);
                res.add(num1 - num2);
                res.add(num2 - num1);
                res.add(num1 * num2);
                if (num1 != 0) res.add(num2 / num1);
                if (num2 != 0) res.add(num1 / num2);
                
                //注意先remove后面的 不然index会变
                nums.remove(j);
                nums.remove(i);
                for (int k = 0; k < res.size(); k++) {
                    nums.add(res.get(k));
                    if(search(nums)) return true;
                    nums.remove(nums.size() - 1);
                }
                nums.add(i, num1);
                nums.add(j, num2);
            }
        }
        
        return false;
    }

    public static void main(String[] args) {
        List<Integer> test = new ArrayList<>(Arrays.asList(9, 9, 9 ,9));
        System.out.println(game(test));
    }

}
```
