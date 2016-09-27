# Anagrams

```java
public class Anagrams {

    public boolean anagram(String s, String t) {
        //ASCii 开个256位的数组
        //把S往里塞
        //验证sHash[t.charAt(i)] < 0 return false
        if (s.length() != t.length()) return false;
        
        int[] sHash = new int[256];
        
        for (int i = 0; i < s.length(); i++) {
            sHash[s.charAt(i)]++;
        }
        
        for (int i = 0; i < s.length(); i++) {
            sHash[t.charAt(i)]--;
            
            if (sHash[t.charAt(i)] < 0) return false;
        }
        
        return true;
    }
    

    
    
    public ArrayList<String> anagrams(String[] strs) {
        //把每个单词弄成char[] 然后sort 多于1的就add进tmp
        ArrayList<String> res = new ArrayList<String>();
        
        if (strs == null || strs.length == 0) {
            return res;
        }
        
        HashMap<String, ArrayList<String>> map = new HashMap<String, ArrayList<String>>();
        for(String word: strs) {
            char[] wordArray = word.toCharArray();
            Arrays.sort(wordArray);
            
            String key = String.valueOf(wordArray);
            if (!map.containsKey(key)) {
                map.put(key, new ArrayList<String>());
            }
            map.get(key).add(word);
            
            
            
        }
        
        //这里注意写法
        for (ArrayList<String> tmp : map.values()) {
            if (tmp.size() > 1) {
                res.addAll(tmp);
            }
        }
         return res;
    }
    
    
    public static void main(String[] args) {
        // TODO Auto-generated method stub
        Anagrams ana = new Anagrams();
        System.out.println(ana.anagram("abc", "cba"));
        String[] strs = new String[]{"lint", "intl", "inlt", "code"}; 
        System.out.println(ana.anagrams(strs));
    }
```