# WordBreak

```java
//http://www.cnblogs.com/yuzhangcmu/p/4037299.html
//O(2^n)
public class WordBreakMoose {
    
    public String wordBreak(String s, Set<String> wordDict) {
        //注意这里return "", return null无法递归
        if (s == null || s.length() == 0) return "";
        for (int i = 0; i < s.length(); i++) {
            String prefix = s.substring(0, i + 1);
            if (wordDict.contains(prefix)) {
                String subfix = wordBreak(s.substring(i + 1), wordDict);
                
                if (subfix != null) {
                    if (subfix.isEmpty()) {
                        return prefix;
                    } else {
                        return prefix + " " + subfix;
                    }
                }
            }  
        }
        return null;
    }
    
    /**
    在本题的DFS中，我们这样定义：
    用刀在字符串中切一刀。左边是i个字符，右边是len-i个字符。
    i: 1- len
    如果： 左边是字典里的词，右边是可以wordbreak的，那么把左边的字符串加到右边算出来的List中，生成新的list返回。
    1. Base case:
    当输入字符串为空的时候，应该给出一个空解。这个很重要，否则这个递归是不能运行的。
    2. 递归的时候，i应该从1开始递归，因为我们要把这个问题分解为2个部分，如果你左边给0，那就是死循环。

    记忆：
    为了加快DFS的速度，我们应该添加记忆，也就是说，算过的字符串不要再重复计算。举例子：
    apple n feng
    app len feng
    如果存在以上2种划分，那么feng这个字符串会被反复计算，在这里至少计算了2次。我们使用一个Hashmap把对应字符串的解记下来，这样就能避免重复的计算。 否则这一道题目会超时。
    **/
    
    public List<String> wordBreak2(String s, Set<String> dict) {
        HashMap<String, List<String>> map = new HashMap<String, List<String>>();
        
        if (s == null || s.length() == 0 || dict.isEmpty()) {
            return null;
        }
        
        return dfs(s, dict, map);
    }
    
    private List<String> dfs(String s, Set<String> dict, HashMap<String, List<String>> map) {
        List<String> res = new ArrayList<>();
        
        if (map.containsKey(s)) {
            return map.get(s);
        }
        
        int len = s.length();
        
        if (len == 0) {
            res.add("");
        } else {
            for (int i = 0; i < len; i++) {
                String prefix = s.substring(0, i + 1);
                if (dict.contains(prefix)) {
                    List<String> subfix = dfs(s.substring(i + 1, len), dict, map);
                    
                    if (subfix.isEmpty()) {
                        continue;
                    }   
                    
                    
                    for(String r: subfix) {
                        StringBuilder sb = new StringBuilder();
                        sb.append(prefix);
                        if (i != 0 && i + 1 != len) {
                            sb.append(" ");
                        }
                        sb.append(r);
                        res.add(sb.toString());
                    }
                    
                }
            }
        }
        
        map.put(s, res);
        return res;
    }
    
    //Brute force
    //每次维护一个当前结果集，然后遍历剩下的所有子串，如果子串在字典中出现，则保存一下结果，并放入下一层递归剩下的字符
    public ArrayList<String> wordBreakBF(String s, Set<String> dict) {  
        ArrayList<String> res = new ArrayList<String>();  
        if(s==null || s.length()==0 || !canBreak(s, dict))  
            return res;  
        helper(s,dict,0,"",res);  
        return res;  
    }  
    private void helper(String s, Set<String> dict, int start, String item, ArrayList<String> res)  
    {  
        if(start>=s.length())  
        {  
            res.add(item);  
            return;  
        }  
        StringBuilder str = new StringBuilder();  
        for(int i=start;i<s.length();i++)  
        {  
            str.append(s.charAt(i));  
            if(dict.contains(str.toString()))  
            {  
                String newItem;
                if (item.length() > 0) {
                    newItem = item+" "+str.toString();
                } else {
                    newItem = str.toString();
                }
                
                helper(s,dict,i+1,newItem,res);  
            }  
        }  
    }
    
    public boolean canBreak(String s, Set<String> dict) {
        //state
        int len = s.length();
        boolean[] dp = new boolean[len + 1];
        
        //init
        dp[0] = true;
        
        int maxLen = Integer.MIN_VALUE;
        
        for (String word: dict) {
            maxLen = Math.max(maxLen, word.length());
        }
        
        //function
        for(int i = 1; i <= s.length(); i++) {
            for(int j = i - 1; j >= 0 && i - j <= maxLen; j--) {
                String word = s.substring(j, i);
                if (dp[j] && dict.contains(word)) {
                    dp[i] = true;
                    break;
                }
            }
        }
        
        return dp[s.length()];
    }

    

    
    public static void main(String[] args) {
        String s = "catsanddog";
        Set<String> dict = new HashSet<>();
        dict.addAll(new ArrayList<>(Arrays.asList("cat", "cats", "and", "sand", "dog")));
        WordBreakMoose wbm = new WordBreakMoose();
        System.out.println(wbm.wordBreak(s, dict));
        System.out.println(wbm.wordBreak2(s, dict));
        System.out.println(wbm.wordBreakBF(s, dict));

    }

}
```