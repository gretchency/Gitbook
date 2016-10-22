# Course Schedule

https://leetcode.com/problems/course-schedule/


我们定义二维数组graph来表示这个有向图，一位数组in来表示每个顶点的入度。我们开始先根据输入来建立这个有向图，并将入度数组也初始化好。然后我们定义一个queue变量，将所有入度为0的点放入队列中，然后开始遍历队列，从graph里遍历其连接的点，每到达一个新节点，将其入度减一，如果此时该点入度为0，则放入队列末尾。直到遍历完队列中所有的值，若此时还有节点的入度不为0，则说明环存在，返回false，反之则返回true。



```java
public boolean canFinish(int numCourses, int[][] prerequisites) {
        int len = prerequisites.length;

        if (numCourses == 0 || len == 0) return true;
        //counter for number of prerequisites
        int[] pCount = new int[numCourses];
        
        
        //Create posts graph, so that we can get classes can be finished after index class is finished
        List<List<Integer>> posts = new ArrayList<>();
        for (int i = 0; i < numCourses; i++) {
            posts.add(new ArrayList<Integer>());
        }
        
        
        for (int i = 0; i < len; i++) {
            //count courses that need prerequisties
            pCount[prerequisites[i][0]]++;
            posts.get(prerequisites[i][1]).add(prerequisites[i][0]);
        }
        
        Queue<Integer> queue = new LinkedList<>();
        
        //add degree 0 courses to the queue
        for (int i = 0; i < numCourses; i++) {
            if (pCount[i] == 0) {
                queue.offer(i);
            }
        }
        
        //count how many courses degree 0
        int numNoPre = queue.size();
        
        while(!queue.isEmpty()) {
            int top = queue.poll();
            
            // for (int i = 0; i < len; i++) {
            //     //Satisfy the prerequisite condition
            //     if (prerequisites[i][1] == top) {
            //         pCount[prerequisites[i][0]]--;
                    
            //         if (pCount[prerequisites[i][0]] == 0) {
            //             numNoPre++;
            //             queue.offer(prerequisites[i][0]);
            //         }
            //     }
                
            // }
            for (int i: posts.get(top)) {
                if (--pCount[i] == 0) {
                    numNoPre++;
                    queue.offer(i);
                }
            }
        }
        
        return numNoPre == numCourses;
        
    }
```

下面我们来看DFS的解法，也需要建立有向图，还是用二维数组来建立，和BFS不同的是，我们像现在需要一个一维数组visit来记录访问状态，大体思路是，先建立好有向图，然后从第一个门课开始，找其可构成哪门课，暂时将当前课程标记为已访问，然后对新得到的课程调用DFS递归，直到出现新的课程已经访问过了，则返回false，没有冲突的话返回true，然后把标记为已访问的课程改为未访问。

* 这里-1代表访问过 1代表正在访问 0代表没访问
* 由于-1表示访问过且走的通的dfs，所以下次访问到他的时候直接return true
* 但是如果boolean数组的话 只有两种状态 访问中和没访问 所以就不行

* 参考

http://www.cnblogs.com/zmyvszk/p/5348786.html
http://www.jyuan92.com/blog/leetcode-course-schedule-ii/

```java
public class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        if(prerequisites == null){
            throw new IllegalArgumentException("illegal prerequisites array");
        }
     
        int len = prerequisites.length;
     
        if(numCourses == 0 || len == 0){
            return true;
        }
     
        //track visited courses
        int[] visited = new int[numCourses];
     
        // use the map to store what courses depend on a course 
        HashMap<Integer,ArrayList<Integer>> map = new HashMap<Integer,ArrayList<Integer>>();
        for(int[] a: prerequisites){
            if(map.containsKey(a[1])){
                map.get(a[1]).add(a[0]);
            }else{
                ArrayList<Integer> l = new ArrayList<Integer>();
                l.add(a[0]);
                map.put(a[1], l);
            }
        }
     
        for(int i=0; i<numCourses; i++){
            if(!canFinishDFS(map, visited, i))
                return false;
        }
     
        return true;
    }
     
    private boolean canFinishDFS(HashMap<Integer,ArrayList<Integer>> map, int[] visited, int i){
        if(visited[i] == 1) 
            return false;
            
        if(visited[i] == -1) 
            return true;
        
     
        visited[i]= 1;
        if(map.containsKey(i)){
            for(int j: map.get(i)){
                if(!canFinishDFS(map, visited, j)) 
                    return false;
            }
        }
     
        visited[i]= -1;
     
        return true;
    }
    }
```