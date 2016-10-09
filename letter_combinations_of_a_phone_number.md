# Letter Combinations of a Phone Number
https://leetcode.com/problems/letter-combinations-of-a-phone-number/

题解
* 根据数字index建立String数组存放对应字母
* 用len记录数字位置，然后根据len取得对应数字的字母
* 递归取得字母组合
* prefix + letters.charAt(i)就不用最后remove一下了

O(3^m)  3是每个数字有三个字母 m是有几个数字


```java
    public List<String> letterCombinations(String digits) {
        List<String> res = new ArrayList<>();
        if (digits == null || digits.length() == 0) return res;
        String[] table = new String[]{"","","abc","def","ghi","jkl","mno","pqrs","tuv","wxyz"};
        
        dfs(table, res, digits, "", 0);
        return res;
    }
    
    private void dfs(String[] table, List<String> res, String digits, String prefix, int len) {
        if (len == digits.length()) {
            res.add(prefix);
            return;
        }
        String letters = table[digits.charAt(len) - '0'];
        for (int i = 0; i < letters.length(); i++) {
            // String newPrefix = prefix + letters.charAt(i);
            // dfs(table, res, digits, newPrefix, len + 1);
            // //这里要修改newPrefix，而不是prefix
            // prefix = newPrefix.substring(0, newPrefix.length() - 1);
            
            dfs(table, res, digits, prefix + letters.charAt(i), len + 1);
        }
    }
```