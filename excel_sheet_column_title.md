# Excel Sheet Column Title

Excel Sheet Column Title

Given a positive integer, return its corresponding column title as appear in an Excel sheet.
For example:
```
    1 -> A
    2 -> B
    3 -> C
    ...
    26 -> Z
    27 -> AA
    28 -> AB
```

减1再取余就是和A差几步，可以除几次26就代表有几位，最后要reverse一下
```java
public class Solution {
    public String convertToTitle(int n) {
        if (n <= 0) return "";
        StringBuilder sb = new StringBuilder();
        
        while (n != 0) {
            //这里要n--, 因为A从1开始
            n--;
            char c = (char) (n % 26 + 'A');
            sb.append(c);
            
            n /= 26;
        }
        
        return sb.reverse().toString();
    }
}
```