# Permutation BFS

http://www.lintcode.com/en/problem/permutations/

![](Screen Shot 2016-09-09 at 11.29.34 AM.png)

把1开头的list全加进去，然后remove[1],把2开头的list加进去，以此类推


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

Related Problem

Subsets

```java
    public ArrayList<ArrayList<Integer>> subsets(int[] nums) {
        // write your code here
        if (nums == null || nums.length == 0) {
            return null;
        }
        
        ArrayList<ArrayList<Integer>> result = new ArrayList<ArrayList<Integer>>();
        ArrayList<Integer> list = new ArrayList<Integer>();
        Arrays.sort(nums);
        subsetsHelper(result, list, nums, 0);
        
        return result;
    }
    
    public void subsetsHelper(ArrayList<ArrayList<Integer>> result, ArrayList<Integer> list, int[] nums, int pos) {
        result.add(new ArrayList<Integer>(list));
        
        for (int i = pos; i < nums.length; i++) {
            list.add(nums[i]);
            subsetsHelper(result, list, nums, i + 1);
            //回溯
            list.remove(list.size() - 1);
        }
    }
```