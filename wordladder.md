# WordLadder

http://www.lintcode.com/en/problem/word-ladder/#

![](Screen Shot 2016-09-10 at 10.26.57 AM.png)


```java
public int ladderLength(String start, String end, Set<String> dict) {
        // BFS
        if (dict == null) {
            return 0;
        }
        
        if (start.equals(end)) {
            return 1;
        }
        
        
        //注意先把start end 加入dict 才能get到他的next word
        dict.add(start);
        dict.add(end);
        
        
        HashSet<String> set = new HashSet<String>();
        Queue<String> q = new LinkedList<String>();
        
        
        set.add(start);
        q.offer(start);
        
        int length = 1;
        while (!q.isEmpty()) {
            length++;
            
            //****与clone graph类比 由于求最短路径 需要分层遍历 多一层循环
            int size = q.size();
            for (int i = 0; i < size; i++) {
                String curr = q.poll();
                for (String nextWord: getNextWord(curr, dict)) {
                    if (set.contains(nextWord)) {
                        continue;
                    }
                    
                    if (nextWord.equals(end)) {
                        return length;
                    }
                    
                    q.offer(nextWord);
                    set.add(nextWord);
                }
            }
        }
        
        return 0;
    }
    
    private String replace(String word, int index, char c) {
        //用一个char array
        char[] wordChar = word.toCharArray();
        wordChar[index] = c;
        return new String(wordChar);
    }
    
    private ArrayList<String> getNextWord(String word, Set<String> dict) {
        ArrayList<String> res = new ArrayList<String>();
        
        //两层循环换字母
        for (char c = 'a'; c <= 'z'; c++) {
            for (int i = 0; i < word.length(); i++) {
                if (word.charAt(i) == c) {
                    continue;
                }
                
                String newWord = replace(word, i, c);
                
                if (dict.contains(newWord)) {
                    res.add(newWord);
                }
            
            }
        }
        
        return res;
        
    }

```