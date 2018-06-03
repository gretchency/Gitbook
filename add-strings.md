Given two non-negative integers`num1`and`num2`represented as string, return the sum of`num1`and`num2`.

# 思路：

以79+22 为例，先算个位，进1，再算十位再进1，最后得到结果101。

我们需要一个flag代表要进1还是不进1，然后利用i,j双指针从个位一直算到最高位

当最高位都算完后，要看一看是否flag不为0，否则加上flag

# 注意:

**int to char:**

the values of`'0', '1', '2', ...`in ascii are ascending. So e.g. '0' in ascii is 48, '1' is 49, etc. 

So if you take`'2' - '0'`you really just get`50 - 48 = 2`

Have a look at an ASCII table in order to understand this principle better. Also,`'x'`means get the ascii value of the character in Java

**char to int:**

int a = 1;

char b = \(char\)\(a + '0'\);

# 时间复杂度:

O\(N\), N为两个String的length\(\)之和

```java
class Solution {
    public String addStrings(String num1, String num2) {
        int i = num1.length() - 1;
        int j = num2.length() - 1;
        //用来判断进位
        int flag = 0;
        String res = "";
        while (i >= 0 || j >= 0) {
            int a, b;
            if (i >= 0) {
                //char to int (ascii)
                a = num1.charAt(i--) - '0';
            } else {
                a = 0;
            }
            
            if (j >= 0) {
                b = num2.charAt(j--) - '0';
            } else {
                b = 0;
            }
        
            int sum = a + b + flag;
            //int to char
            res = (char)(sum % 10 + '0') + res;
            flag = sum / 10;
        }
        
        //最高位的进位判断
        if (flag != 0) {
            return "1" + res; 
        } else {
            return res;
        }
    }
}
```



