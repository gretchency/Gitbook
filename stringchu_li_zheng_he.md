# String处理 整合

**Implement strStr()** [leet](https://leetcode.com/problems/implement-strstr/)

[**Minimum Window SubString** ](https://gretchency.gitbooks.io/leetcode/content/minimum_window_substring.html)
* 双指针解决 O(n)
* 先根据t建立map,key是字母，value是该字母出现了几次
* 右指针先走，满足就减value,先找到满足条件的一个窗口，更新MinLen,左指针开始走，看看能不能缩小窗口，一直走到不满足条件，这时候右指针接着走，来满足左指针挖下的坑，以此类推。
* value为非负就增加Count,为负说明减多了，这时候用left指针增，直到为正时候说明又缺这一字母了。

[Longest Substring Without Repeating Characters](https://gretchency.gitbooks.io/leetcode/content/longest_substring_without_repeating_characters.html) 
* 滑动窗口法（end:橘色指针，start蓝色指针）
* 256 boolean数组存储访问状态
* 先滑end，走到划不动，开始滑start,全都变为false，直到能滑动为止，每次更新maxLen
* start + len = s.length()就可以停止了

[ZigZag Conversion](https://gretchency.gitbooks.io/leetcode/content/zigzag_conversion.html)

可以发现规律，每一轮从上往下，再斜上走到第一行之前的长度永远是 2n-2。利用这个规律，可以按行填字，第一行和最后一行，就是按照2n-2的顺序一点点加的。 其他行除了上面那个填字规则，就是还要处理斜着那条线的字，可以发现那条线的字的位置永远是当前列j+(2n-2)-2i(i是行的index）。

[Excel Sheet Column Title](https://gretchency.gitbooks.io/leetcode/content/excel_sheet_column_title.html)

减1再取余就是和A差几步，可以除几次26就代表有几位，最后要reverse一下

[Group Anagram](https://gretchency.gitbooks.io/leetcode/content/group_anagram.html)

* Sort + HashMap. 根据sort后的string建key, 把sorted后一样的string都作为value.根据题设按字母顺序输出，最后还要sort一遍再加入result.

Find all anagrams in a String

