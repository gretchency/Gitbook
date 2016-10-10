# Java基础





# Collections
---

| Interface | Implementaion |
| -- | -- |
| List | ArrayList, LinkedList |
| Set | HashSet, TreeSet |
| Map | HashMap, TreeMap |



### ArrayList VS LinkedList



1) **Search**: ArrayList search operation is pretty fast compared to the LinkedList search operation. ```get(int index)``` in ArrayList gives the performance of ```O(1)``` while LinkedList performance is ```O(n)```.

Reason: ArrayList get index; LinkedList iterate from the beginning

2) **Deletion**: LinkedList remove operation gives ```O(1)``` performance while ArrayList gives variable performance: ```O(n)``` in worst case (while removing first element) and ```O(1)``` in best case (While removing last element).

Reason: ArrayList need to shift all the trailing elemnets after removal.
* Insertion same as removal

**Conclusion**

1) As explained above the insert and remove operations give good performance (```O(1)```) in LinkedList compared to ArrayList(```O(n)```). Hence if there is a requirement of frequent addition and deletion in application then LinkedList is a best choice.

2) Search (get method) operations are fast in Arraylist (```O(1)```) but not in LinkedList (```O(n)```) so If there are less add and remove operations and more search operations requirement, ArrayList would be your best bet.

*ArrayList is better for **storing and accessing data**.*

*LinkedList is better for **manipulating data**.*

---

### Java Inner Class vs Nested Class

Inner class is subset of nested class, Inner class is non-static nested class

* When you want to instantiate an **inner class** object, you need to instantiate the **outer class** first.

* But with **static nested class**, you can simply instantiate the class object
```java
public class BinaryTreeToDoublyLinkedList {
     class TreeNode {
        int val;
        TreeNode left;
        TreeNode right;
        public TreeNode(int val) {
            this.val = val;
        } 
    }
    
    public static void main(String[] args) {
        //instantiate class first
        BinaryTreeToDoublyLinkedList list = new BinaryTreeToDoublyLinkedList();
        TreeNode root = list.new TreeNode(10);
    }
}
```
---

### Shallow Copy VS Deep Copy
http://javaconceptoftheday.com/difference-between-shallow-copy-vs-deep-copy-in-java/
* **Shallow copy**: Clone this object and keep its references
*** Deep copy**: Clone this object and every reference to every other object it has



In java, ```clone()``` method creates the shallow copy of an object.

The **shallow copy** of an object will have exact copy of all the fields of original object. That means any changes made to those objects through clone object will be reflected in original object or vice-versa.
![](http://javaconceptoftheday.com/wp-content/uploads/2015/04/ShallowCopy.png)

**Deep copy** of an object will have exact copy of all the fields of original object just like shallow copy. But in additional, if original object has any references to other objects as fields, then copy of those objects are also created by calling clone() method on them.

![](http://javaconceptoftheday.com/wp-content/uploads/2015/04/DeepCopy.png)
