# 位运算


### 不用额外空间的swap



swap这个就是 a= a^b; b = a^ b; a = b^a就行了

```java
// swap a and b 
public class SwapAandB {

	public static void main(String[] args) {
		int a = 100;
		int b = 1000;

		a = a ^ b; // a^b
		b = a ^ b; // a^b^b =a
		a = a ^ b;// a^b^a=b
		System.out.println("a: " + a);
		System.out.println("b: " + b);
	}

}

```
---

### 不能用加号的加法
http://blog.csdn.net/pwiling/article/details/51842393

* 我们可以基于以上的真值表用&和^运算来实现加法，每一位的^运算得到每一位上的不加进位的和，用&运算得到每一位的进位。

```java
public int getSum(int a, int b) {
        while( b != 0) {
            int carry = a & b;
            a = a ^ b;
            b = carry << 1;
        }
        
        return a;
    }
```
---
# Bit number changes

Write a Java method that will return the number of bits that will need to be changed in order to convert an integer, X, into another integer, Y and vice versa. The method should accept two different integers as input. For example, if your method is passed the integers 12 and 16 then your method should return a 3 .

Using XOR  
* a ```^``` b 数有多少1就是要改几位

```java
public static int findNumberOfBits(int x, int y)
{
int bitCount = 0;

int z = x ^ y;  //XOR x and y

while (z != 0)
{
  //increment count if last binary digit is a 1:
  //a&b  比较a的最后一位与b是否相等 相等时候加1
  bitCount += z & 1; 
  //继续比较知道移到0
  z = z >> 1;  //shift Z by 1 bit to the right
}

return bitCount;
}
```

---
Numbr of 1 Bits

```java
public class Solution {
    // you need to treat n as an unsigned value
    public int hammingWeight(int n) {
        if (n == 0) return 0;
        int count = 0;
        for (int i =0; i < 32; i++) {
            count += n & 1;
            n = n >> 1;
        }
        
        return count;
    }
}
```