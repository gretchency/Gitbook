# Permutation BFS

http://www.lintcode.com/en/problem/permutations/

![](Screen Shot 2016-09-09 at 11.29.34 AM.png)

results.add(new ArrayList<Integer>(list))

http://www.jiuzhang.com/qa/663/

```java
    public List<List<Integer>> permute(int[] nums) {
        ArrayList<List<Integer>> res = new ArrayList<List<Integer>>();
        
        
        if (nums == null) {
            return res;
        }
        
        if (nums.length == 0) {
            res.add(new ArrayList<Integer>());
            return res;
        }
        
        ArrayList<Integer> list = new ArrayList<Integer>();
        
        helper(res, list, nums);
        
        return res;
    }
    
    private void helper(ArrayList<List<Integer>> res, ArrayList<Integer> list, int[] nums) {
        //base case
        if (list.size() == nums.length) {
            
            //注意这里要new新的 否则只add了reference
            res.add(new ArrayList<Integer>(list));
            return;
        }
        
        for (int i = 0; i < nums.length; i++) {
            //不要重复加
            if (list.contains(nums[i])) {
                continue;
            }
            
            list.add(nums[i]);
            helper(res, list, nums);
            
            //往回走
            list.remove(list.size() - 1);
        }
    }
```