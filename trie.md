# Trie

```java
//Trie建造dictionary树， 用dfs把所有chars的可能combination找出来 然后搜索tree

//注意dfs时候visited记录是否访问过，相同char如果前一个没visited就不能访问后一个来避免重复
public class Dictionary {
    public static TrieNode constructTrie(Set<String> dict) {
        TrieNode root = new TrieNode();
        for (String word: dict) {
            root.insert(word);
        }
        
        return root;
    }

    public static List<String> containsCombination(char[] chars, TrieNode root) {
        Arrays.sort(chars);
        
        List<String> comb = new ArrayList<>();
        boolean[] visited = new boolean[chars.length];
        
        search(chars, comb, visited, "");
        
        List<String> res = new ArrayList<>();
        
        for(String s: comb) {
            if (root.search(s)) {
                res.add(s);
            }
        }
        
        return res;
    }

    private static void search(char[] chars, List<String> comb, boolean[] visited, String s) {
        comb.add(s);
        
        if (s.length() == chars.length) return;
        
        for (int i = 0; i < chars.length; i++) {
            if (visited[i]) continue;
            
            if (i > 0 && chars[i - 1] == chars[i] && !visited[i - 1]) {
                continue;
            }
            
            visited[i] = true;
            search(chars, comb, visited, s + chars[i]);
            visited[i] = false;
        }
    }

    public static void main(String[] args) {
        Set<String> dict = new HashSet<>();
        dict.addAll(Arrays.asList("a", "aa", "cat", "cats", "aaa", "cc"));
        char[] chars = {'a', 'c', 'a', 'r', 't'};
        TrieNode root = constructTrie(dict);
        System.out.println(containsCombination(chars, root));
    }
}

class TrieNode {
    boolean hasWord;
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
    }
    
    public boolean search(String s) {
        TrieNode curr = this;
        for (Character c: s.toCharArray()) {
            if(!curr.childrens.containsKey(c)) {
                return false;
            }
            curr = curr.childrens.get(c);
        }
        return curr.hasWord;
    }
}
```