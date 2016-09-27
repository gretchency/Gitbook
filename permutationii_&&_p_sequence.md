# Permutationii && P Sequence

```java
public class Permutation {
    //PermutationII
    public List<List<Integer>> permuteUnique(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        
        if (nums == null || nums.length == 0) return res;
        
        List<Integer> list = new ArrayList<>();
        boolean[] visited = new boolean[nums.length];
    
        //****Sort first!!!
        Arrays.sort(nums);
        dfs(nums, list, res, visited);
        
        return res;
    }
    
    private void dfs(int[] nums, List<Integer> list, List<List<Integer>> res, boolean[] visited) {
        if (list.size() == nums.length) {
            res.add(new ArrayList<Integer>(list));
            return;
        }
        
        for (int i = 0; i < nums.length; i++) {
            if (visited[i]) continue;
            if (i > 0 && nums[i - 1] == nums[i] && !visited[i - 1]) continue;
            
            list.add(nums[i]);
            visited[i] = true;
            dfs(nums, list, res, visited);
            list.remove(list.size() - 1);
            visited[i] = false;
        }
    }
    
    //Permutation Sequence
    //http://blog.csdn.net/u013027996/article/details/18405735
    static char[] dic = {'1','2','3','4','5','6','7','8','9'};
    static int count = 0;
    static String res;
    public static String getPermutation(int n, int k) {
        StringBuilder sb = new StringBuilder();
        boolean[] visited = new boolean[n];
        
        dfs(n, k, sb, 0, visited);
        return res;
    }
    
    private static void dfs(int n, int k, StringBuilder sb, int deep, boolean[] visited) {
        if (deep == n) {
            count++;
            if (count == k) {
                
                res = sb.toString();
                return;
            }
        }
        
        for (int i = 0; i < n; i++) {
            if(visited[i]) continue;
            sb.append(dic[i]);
            
            visited[i] = true;
            dfs(n, k, sb, deep + 1, visited);
            
            sb.deleteCharAt(sb.length() - 1);
            visited[i] = false;

        }
    }
    
    public static void main(String[] args) {
        System.out.println(getPermutation(3,4));
    }
}
```