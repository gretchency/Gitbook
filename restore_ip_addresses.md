# Restore IP Addresses

Given a string containing only digits, restore it by returning all possible valid IP address combinations.

For example:
Given "25525511135",

return ["255.255.11.135", "255.255.111.35"]. (Order does not matter)

* 可以一个字符两个字符三个字符的按规定排列组合，所以递归
* 每取一个字符短要判断是不是valid，所以需要一个valid函数
* 递归的return条件：count为3时直接判断最后剩余长度是否valid
* 如果valid s取substring, prefix增加长度，count++,


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