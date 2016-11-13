# String


### String保留两位小数



```DecimalFormat df = new DecimalFormat("#.00");```
```java
public static void main(String[] args) {
        //Note the "00", meaning exactly two decimal places.
        //If you use "#.##" (# means "optional" digit), it will drop trailing zeroes - 
        //ie new DecimalFormat("#.##").format(3.0d); prints just "3", not "3.00".
        double a = 5;
        double b = 3;
        DecimalFormat df = new DecimalFormat("#.00");
        System.out.println(a / b);
        System.out.println(df.format(a/b));
        System.out.println( String.format( "%.2f", a / b ) );
    }
```
