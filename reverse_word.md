# Reverse Word

```java
public class ReverseWord {
    public static String reverseWord1(String s) {
        //注意这里先判断是否除了空格啥也没有 
        if (s== null || s.trim().length() == 0) return "";
        
        String[] words = s.trim().split(" ");
        StringBuilder sb = new StringBuilder();
        for (int i = words.length - 1; i >= 0; i--) {
            //trim只能trim掉前后 中间要自己continue掉
            if(words[i].length() == 0) continue;
            
            //空格+单词比较好
            sb.append(" " + words[i]);
        }
        
        sb.deleteCharAt(0);
        return sb.toString();
    }
    

    
    public static void reverseWord2(char[] c) {
        if (c == null || c.length == 0) return;
        //reverse the whole array
        reverse(c, 0, c.length - 1);
        
        //reverse each word
        int start = 0;
        while (start < c.length) {
            while(start < c.length && c[start] == ' ') {
                start++;
            }
            
            //reach the end
            if (start == c.length - 1) break;
            
            int end = start;
            
            //比的是end + 1
            while (end + 1 < c.length && c[end + 1] != ' ') {
                end++;
            }
            reverse(c, start, end);
            
            //注意这里 否则死循环
            start = end + 1;
        }
        
    }
    
    public static void reverse(char[] c, int start, int end) {
        while(start < end) {
            char temp = c[start];
            c[start] = c[end];
            c[end] = temp;
            start++;
            end--;
        }
    }

    public static void main(String[] args) {
        // TODO Auto-generated method stub
        String s = "   a   b ";
        System.out.println(reverseWord1(s));
        
        
        char[] chars = {'a', 'p', 'p', 'p', 'l', 'e', ' ', 't', 'a', 's', 't', 'e', 's', ' '};
        reverseWord2(chars);
        for (char c : chars) {
            System.out.print(c);
        }
    }

}
```