# ZigZag Conversion

```
看坐标的变化。并且需要分块处理。

 n=2时，字符串坐标变成zigzag的走法就是：

 0 2 4 6

 1 3 5 7

 n=3时的走法是：

 0     4     8

 1  3 5  7 9

 2     6    10 

 n=4时的走法是：

 0      6        12

 1   5 7    11 13

 2 4   8 10    14

 3      9         15
```
可以发现规律，每一轮从上往下，再斜上走到第一行之前的长度永远是 2n-2。利用这个规律，可以按行填字，第一行和最后一行，就是按照2n-2的顺序一点点加的。 其他行除了上面那个填字规则，就是还要处理斜着那条线的字，可以发现那条线的字的位置永远是当前列j+(2n-2)-2i(i是行的index）。

```java
public class Solution {
    public String convert(String s, int numRows) {
        if (s == null || numRows < 2 || s.length() < 2) return s;
        
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < numRows; i++) {
            //注意j从i开始
            for (int j = i; j < s.length(); j += 2 * numRows - 2) {
                sb.append(s.charAt(j));
                if (i != 0 && i != numRows - 1) {
                    int tmp = j + 2 * numRows - 2 - 2 * i;
                    if (tmp < s.length()) {
                        sb.append(s.charAt(tmp));
                    }
                }
            }
        }
        
        return sb.toString();
    }
}
```