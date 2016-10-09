# Palindrome Partitioning I

Given a string s, partition s such that every substring of the partition is a palindrome.

Return all possible palindrome partitioning of s.

For example, given s = "aab",
Return

[
  ["aa","b"],
  ["a","a","b"]
]

二刷
* 类比Restore IP Address,我们可以选1个字母，2个字母，直到字符串长度的字母
* 一个字符串，可以本身substring来缩短s长度，s为0时候就return
* substring(beginindex)里beiginindex可以为自身长度，此时返回""

```java
    public List<List<String>> partition(String s) {
        List<List<String>> res = new ArrayList<>();
        if (s == null || s.length() == 0) return res;
        List<String> list = new ArrayList<>();
        
        dfs (s, list, res);
        return res;
    }
    
    private void dfs (String s, List<String> list, List<List<String>> res) {
        if (s.length() == 0) {
            res.add(new ArrayList<String>(list));
            return;
        }
        
        //****注意这里一定要遍历到等于length才是完整的一条字符串
        for (int i = 1; i <= s.length(); i++) {
            String prefix = s.substring(0, i);
            if (isPal(prefix)) {
                list.add(prefix);
                //这里用substring缩短长度
                dfs(s.substring(i), list, res);
                list.remove(list.size() - 1);
            }
        }
        
    }
    
    private boolean isPal(String s) {
        int start = 0;
        int end = s.length() - 1;
        while (start < end) {
            if (s.charAt(start) == s.charAt(end)) {
                start++; 
                end--;
                continue;
            } else {
                return false;
            }
        }
        
        return true;
    }
```



```java
    public List<List<String>> partition(String s) {
        List<List<String>> res = new ArrayList<>();
        if (s == null || s.length() == 0) return res;
        List<String> list = new ArrayList<>();
        
        dfs (s, list, res, 0);
        return res;
    }
    
    private void dfs (String s, List<String> list, List<List<String>> res, int pos) {
        //***substring [) 所以可以==
        if (pos == s.length()) {
            res.add(new ArrayList<String>(list));
            return;
        }
        
        //这里要pos + 1 来提取substing
        for (int i = pos + 1; i <= s.length(); i++) {
            String prefix = s.substring(pos,i);
            if (!isPal(prefix)) continue;
            list.add(prefix);
            //这里不用i + 1 因为for loop 已加
            dfs(s, list, res, i);
            list.remove(list.size() - 1);
        }
    }
    
    private boolean isPal(String s) {
        int start = 0;
        int end = s.length() - 1;
        while (start < end) {
            if (s.charAt(start) == s.charAt(end)) {
                start++; 
                end--;
                continue;
            } else {
                return false;
            }
        }
        
        return true;
    }
```