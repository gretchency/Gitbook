# ZigZagPrint

```java
public class ZigzagPrint {
    public static void main(String[] args) {
        int[][] matrix = new int[][]{{1,2,3,4},{5,6,7,8},{9,10,11,12}};
        System.out.println(Arrays.toString(zigzagPrint(matrix)));
    }

    public static int[] zigzagPrint(int[][] matrix) {
        if (matrix == null || matrix[0] == null || matrix.length == 0 || matrix[0].length == 0) return null;
        
        int m = matrix.length;
        int n = matrix[0].length;
        int[] res = new int[m * n];
        res[0] = matrix[0][0];
        int index = 1;
        int i = 0;
        int j = 0;
        
        while (index < res.length) {
            //right one or down one
            if (j + 1 < n || i + 1 < m) {
                if (j + 1 < n) {
                    j++;
                } else {
                    i++;
                }
                res[index++] = matrix[i][j];
            }
            
            //bottom left
            while(j - 1 >= 0 && i + 1 < m) {
                res[index++] = matrix[++i][--j];
            }
            
            //down one or right one
            if (j + 1 < n || i + 1 < m) {
                if (i + 1 < m) {
                    i++;
                } else {
                    j++;
                }
                res[index++] = matrix[i][j];
            }
            
            //right top
            while (i - 1 >= 0 && j + 1 < n) {
                res[index++] = matrix[--i][++j];
            }
        }
        
        return res;
    }


}

```