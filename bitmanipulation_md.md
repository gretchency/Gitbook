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