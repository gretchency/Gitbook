# Bit number changes

Write a Java method that will return the number of bits that will need to be changed in order to convert an integer, X, into another integer, Y and vice versa. The method should accept two different integers as input. For example, if your method is passed the integers 12 and 16 then your method should return a 3 .

Using XOR  a XOR b 数有多少1就是要改几位
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