# Restore IP Addresses

Given a string containing only digits, restore it by returning all possible valid IP address combinations.

For example:
Given "25525511135",

return ["255.255.11.135", "255.255.111.35"]. (Order does not matter)

```java
public List<String> restoreIpAddresses(String s) {
        List<String> res = new ArrayList<>();
        
        if (s == null || s.length() == 0) return res;
        
        if (s.length() < 4 || s.length() > 12) return res;
        
        dfs(s, res, "", 0);
        
        return res;
    }
    
    private void dfs (String s, List<String> res, String prefix, int count) {
        if (count == 3 && isValid(s)) {
            res.add(prefix + s);
            return;
        }
        
        //最多取三个字符 i从1开始，到3结束， 同时保证i < s.length,不能等于（1111）
        for (int i = 1; i < 4 & i < s.length(); i++) {
            String sub = s.substring(0, i);
            if (isValid(sub)) {
                //注意这里不断缩小s，增加prefix长度
                dfs(s.substring(i), res, prefix + sub + ".", count + 1);
            }
        }
    }
    
    private boolean isValid(String s) {
        if (s.charAt(0) == '0') return (s.equals("0"));
        
        int num = Integer.parseInt(s);
        if (num > 0 && num <= 255) return true;
        return false;
    }
```