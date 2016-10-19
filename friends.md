# Friends

* 如果要控制距离的话可以用个dist，然后bfs时候for loop每层的size控制距离
```java
public class Friends {

    public static void main(String[] args) {
        Person mike = new Person(), jelly = new Person(), miller = new Person(), billy = new Person(),
                henry = new Person(), john = new Person(), cathy = new Person();
        mike.name = "Mike";
        mike.friends.add(miller);
        mike.friends.add(jelly);
        mike.friends.add(billy);
        jelly.name = "Jelly";
        miller.name = "Miller";
        miller.friends.add(cathy);
        billy.name = "Billy";
        billy.friends.add(henry);
        billy.friends.add(john);
        billy.friends.add(mike);

        henry.name = "Henry";
        john.name = "John";
        cathy.name = "Cathy";
        cathy.friends.add(miller);

        // mike => {miller, Jelly, Billy}.
        // miller => {Cathy}
        // Billy => {Henry, John, mike}
        // Cathy => {miller}
        // print friends list of current person, e.g, mike -> miller, Jelly,
        // Billy, Cathy, Henry, John
        mike.printFriends2();
    }
}

class Person {
    int id;
    String name;
    List<Person> friends = new ArrayList<>();

    //BFS
    public void printFriends() {
        Queue<Person> queue = new LinkedList<>();
        Set<Person> set = new HashSet<>();
        queue.offer(this);
        set.add(this);
        while(!queue.isEmpty()) {
            Person curr = queue.poll();
            
            for(Person friend: curr.friends) {
                if (set.add(friend)) {
                    System.out.println(friend.name);
                    queue.offer(friend);  
                }
            }
        }
    }
    
    //dfs
    public void printFriends2() {
        Set<Person> set = new HashSet<>();
        set.add(this);
        dfs(this, set);
    }
    
    public void dfs (Person person, Set<Person> set) {
        for (Person friend: person.friends) {
            if(set.add(friend)) {
                System.out.println(friend.name);
                dfs(friend, set);
            }
        }
    }
}
```