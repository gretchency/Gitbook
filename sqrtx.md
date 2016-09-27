# Sqrtx

```java
public class sqrtx {
    
    public int sqrtx(int x) {
        if (x < 0) return -1;
        
        long start = 0;
        long end = x;
         while (start + 1 < end) {
             long mid = start + (end - start) / 2;
             
             if (mid * mid <= x) {
                 start = mid;
             } else {
                 end = mid;
             }
         }
         
         if (start * start <= x) {
             return (int) start;
         }
         
         if (end * end <= x) {
             return (int) end;
         }
         
         return -1;
    }

    public static void main(String[] args) {
        // TODO Auto-generated method stub
        sqrtx sq = new sqrtx();
        System.out.println(sq.sqrtx(1887415157));
        
    }
    
}

```