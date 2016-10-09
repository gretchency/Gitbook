# Palindrome Partitioning I

Given a string s, partition s such that every substring of the partition is a palindrome.

Return all possible palindrome partitioning of s.

For example, given s = "aab",
Return

[
  ["aa","b"],
  ["a","a","b"]
]


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