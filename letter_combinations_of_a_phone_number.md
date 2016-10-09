# Letter Combinations of a Phone Number
https://leetcode.com/problems/letter-combinations-of-a-phone-number/

O(3^m)  3是每个数字有三个字母 m是有几个数字

prefix + letters.charAt(i)就不用最后remove一下了
```java
    public List<String> letterCombinations(String digits) {
        List<String> res = new ArrayList<>();
        if (digits == null || digits.length() == 0) return res;
        String[] table = new String[]{"","","abc","def","ghi","jkl","mno","pqrs","tuv","wxyz"};
        
        dfs(table, res, digits, "", 0);
        return res;
    }
    
    private void dfs(String[] table, List<String> res, String digits, String tmp, int len) {
        if (len == digits.length()) {
            res.add(tmp);
            return;
        }
        String letters = table[digits.charAt(len) - '0'];
        for (int i = 0; i < letters.length(); i++) {
            // String newTmp = tmp + letters.charAt(i);
            // dfs(table, res, digits, newTmp, len + 1);
            // //这里要修改newTmp
            // tmp = newTmp.substring(0, newTmp.length() - 1);
            
            dfs(table, res, digits, tmp + letters.charAt(i), len + 1);
        }
    }
```