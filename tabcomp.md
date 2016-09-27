# TabComp

```java

public class TabComp {
    
    private static class TrieNode {
        boolean hasWord;
        String word = "";
        Map<Character, TrieNode> childrens = new HashMap<>();
        
        public void insert(String s) {
            TrieNode curr = this;
            for (Character c: s.toCharArray()) {
                if (!curr.childrens.containsKey(c)) {
                    curr.childrens.put(c, new TrieNode());
                }
                curr = curr.childrens.get(c);
            }
            curr.hasWord = true;
            curr.word = s;
        }
        
//        public boolean search(String s) {
//            TrieNode curr = this;
//            for (Character c: s.toCharArray()) {
//                if(!curr.childrens.containsKey(c)) {
//                    return false;
//                }
//                curr = curr.childrens.get(c);
//            }
//            return curr.hasWord;
//        }
    }

    
    public static void main(String[] args) {
        List<String> directories = new ArrayList<>(Arrays.asList("apple", "application", "hbase", "app", "word", "napple", "aapp", "apply"));
        String prefix = "ap";
        System.out.println(autoComp(prefix, directories));
    }
    
    public static List<String> autoComp(String s, List<String> dict) {
        TrieNode root = new TrieNode();
        for (String word: dict) {
            root.insert(word);
        }
        
        return complete(s, root);      
    }
    
    public static List<String> complete(String prefix, TrieNode curr) {
        List<String> res = new ArrayList<String>();
        for (int i = 0; i < prefix.length(); i++) {
            char c = prefix.charAt(i);
            if (!curr.childrens.containsKey(c)) {
                return res;
            }
            curr = curr.childrens.get(c);
        }
        completeHelper(curr, res);
        
        return res;
    }
    
    private static void completeHelper(TrieNode curr, List<String> res) {
        if (curr == null) return;
        
        if (curr.hasWord) {
            res.add(curr.word);
        }
        
        //对curr的所有children做遍历
        for (TrieNode next: curr.childrens.values()) {
            completeHelper(next, res);
        }
    }
}
```