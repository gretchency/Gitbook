# String处理 整合

**Implement strStr()** [leet](https://leetcode.com/problems/implement-strstr/)

Minimum Window SubString [link](https://gretchency.gitbooks.io/leetcode/content/minwindow.html)
* 双指针解决 O(n)
* 先根据t建立map,key是字母，value是该字母出现了几次
* 右指针先走，满足就减value,先找到满足条件的一个窗口，更新MinLen,左指针开始走，看看能不能缩小窗口，一直走到不满足条件，这时候右指针接着走，来满足左指针挖下的坑，以此类推。
* value为非负就增加Count,为负说明减多了，这时候用left指针增，直到为正时候说明又缺这一字母了。