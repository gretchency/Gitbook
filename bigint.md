# BigInt

http://blog.csdn.net/antgan/article/details/51044098
http://blog.csdn.net/lichong_87/article/details/6860329



```java
public class BigInt {
    public static void main(String[] args) {
        BigInt num1 = new BigInt("00005");
        BigInt num2 = new BigInt("-10");
        //BigInt sum = num1.multiply(num2);
        BigInt sum2 = num1.add(num2);
        //System.out.println(sum.toString());
        System.out.println(sum2.toString());
    }

    private String value;

    public BigInt(String value) {
        this.value = value;
    }

    public String getValue() {
        return value;
    }

    @Override
    public String toString() {
        return value;
    }
    
    public BigInt add(BigInt other) {
        String num1 = getValue();
        String num2 = other.getValue();
        
        if(num1.charAt(0) == '-' && num2.charAt(0) == '-') {
            BigInt value1 = new BigInt(num1.substring(1));
            BigInt value2 = new BigInt(num2.substring(1));
            String result = value1.addHelper(value2).toString();
            return new BigInt("-" + result);
        }
        
        if(num1.charAt(0) == '-') {
            BigInt value1 = new BigInt(num1.substring(1));
            return other.minus(value1);
        }
        
        if(num2.charAt(0) == '-') {
            BigInt value2 = new BigInt(num2.substring(1));
            return this.minus(value2);
        }      
        return this.addHelper(other);
    }
    
    public BigInt minus(BigInt other) {
        String num1 = getValue();
        char[] n1 = new StringBuilder(num1).reverse().toString().toCharArray();
        String num2 = other.getValue();
        char[] n2 = new StringBuilder(num2).reverse().toString().toCharArray();
        
        int len = Math.max(num1.length(), num2.length());
        
        int[] res = new int[len];
        
        for (int i = 0; i < res.length; i++) {
            int a = i < n1.length ? (n1[i] - '0'): 0;
            int b = i < n2.length ? (n2[i] - '0'): 0;
            if (isBigger(num1, num2)) {
                res[i] = a - b;
            } else {
                res[i] = b - a;
            } 
        }
        
        for (int i = 0; i < res.length - 1; i++) {
            if (res[i] < 0) {
                res[i + 1] -= 1;
                res[i] += 10;
            }
        }
        System.out.println(Arrays.toString(res));
        StringBuilder sb = new StringBuilder();
        if (!isBigger(num1, num2)) {
            sb.append('-');
        }
        for (int i = res.length - 1; i >= 0; i--) {
           
            boolean flag = true;
            if (res[i] == 0 && flag) {
                continue;
            } else {
                flag = false;
            }
            sb.append(res[i]);
        }
        return new BigInt(sb.toString());
    }
    
    private Boolean isBigger(String s1, String s2) {
        int len1 = s1.length();
        int len2 = s2.length();
        for (int i = 0; i < s1.length(); i++) {
            if (s1.charAt(i) != '0') break;
            len1--;
        }
        
        for (int i = 0; i < s2.length(); i++) {
            if (s2.charAt(i) != '0') break;
            len2--;
        }
        if (len1 > len2) return true;
        if (len1 < len2) return false;
        
        for (int i = s1.length() - 1; i >= 0; i--) {
            if (s1.charAt(i) - '0' > s2.charAt(i) - '0') {
                return true;
            } else if (s1.charAt(i) - '0' < s2.charAt(i) - '0') {
                return false;
            }
        }
        return true;
    }
    
    public BigInt addHelper(BigInt other) {
        String num1 = getValue();
        char[] n1 = new StringBuilder(num1).reverse().toString().toCharArray();
        String num2 = other.getValue();
        char[] n2 = new StringBuilder(num2).reverse().toString().toCharArray();
        
        int len = Math.max(num1.length(), num2.length());
        
        int[] res = new int[len];
        
        for (int i = 0; i < res.length; i++) {
            int a = i < n1.length ? (n1[i] - '0'): 0;
            int b = i < n2.length ? (n2[i] - '0'): 0;
            res[i] = a + b;
        }

        

        for (int i = 0; i < res.length - 1; i++) {
            res[i + 1] += res[i] / 10;
            res[i] = res[i] % 10;
        }

        StringBuilder sb = new StringBuilder();
        
        for (int i = res.length - 1; i >= 0; i--) {
            sb.append(res[i]);
        }
        
        while(sb.toString().charAt(0) == '0') {
            sb.deleteCharAt(0);
        }
        
        return new BigInt(sb.toString());
    }

    public BigInt multiply(BigInt other) {
        String num1 = value;
        String num2 = other.getValue();
        //init
        int[] n1 = new int[num1.length()];
        int[] n2 = new int[num2.length()];
        int[] res = new int[n1.length + n2.length - 1];
        for (int i = 0; i < num1.length(); i++) {
            n1[i] = num1.charAt(i) - '0';
        }
        
        for (int i = 0; i < num2.length(); i++) {
            n2[i] = num2.charAt(i) - '0';
        }
        
        
        for (int i = 0; i < n1.length; i++) {
            for (int j = 0; j < n2.length; j++) {
                res[i + j] += n1[i] * n2[j];
            }
        }
        
        System.out.println(Arrays.toString(res));
        
        for (int i = res.length - 1; i > 0; i--) {
            res[i - 1] += res[i] / 10;
            res[i] = res[i] % 10;
        }
        
        StringBuilder sb = new StringBuilder();
        for (int i: res) {
            sb.append(i);
        }
        
        while (sb.toString().charAt(0) == '0') {
            sb.deleteCharAt(0);
        }
        return new BigInt(sb.toString());
    }
    

}
```