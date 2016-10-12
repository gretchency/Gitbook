# 面试总结

First, I know IBM since I get interested in Information Technology. IBM is one of the oldest and biggest IT company in the world. When I first use a computer in our school lab, It is a IBM computer.. So I can say I start to know the IT world through IBM. It would be a pride for me if I can work for IBM. For the specific cognitive team, since during my cmu school time, I conducted several project that is ML and NPL related, during these time, I developed my interest in these areas.

During this summer, I worked with a consulting company to do a NLP project. we tried to generate key terms of the survey and define whether it is positive or negative. Also, we utilized IBM watson api to do tone analysis, I found it was very interesting to use the api. This makes me a great candidate for your team

I am currently learning objective-c ios development and different library and frameworks of iOS on my own.

I think for the pros, oc development is fundamental of iOS and mac software development, even your are trying to learn swift, you are better to start from objective c. there are lots of good examples for learning. 
Cons: The syntax of oc is quite different from other ool like java. the way it defines classes and methods are not the way I like comparing with JAVA. So it takes a hard shift when I was trying to develop my first app.
Also, comparing with swift, oc have much more codes, not elegant and neat enough. Also, it only support iOS and mac development. It is bounded to a small area.

I will collect the data, do data preprocessing, generate the key terms based on TF-IDF algorithms.
After I collect the data, I will first do data preprocessing.Text tokenization. Remove number and punctuation. Remove stop word in English.Do stemming. Retain meaningful and non-trivial information for the later-on analysis

For training, KNN, C4.5 decision tree. And validate through cross validation. Im not very familiar with logistic regression

```java
private static String filter(String s) {

        if (s == null || s.length() == 0)
            return s;

        String[] words = s.split("\\|");
        if (words.length <= 1)
            return s;

        String[] filtered = new String[words.length];

        // pre process the string to trim and remove special chars
        for (int i = 0; i < words.length; i++) {

            String cur = filterHelper(words[i]);
            filtered[i] = cur;

            // if contained in any results, or any results is contained in
            // current:
            for (int j = 0; j < filtered.length; j++) {

                if (filtered[j] == null || j == i)
                    continue;

                //String tmp = filtered[j];
                if (filtered[j].equals(cur)) {
                    int len1 = words[j].length();
                    int len2 = words[i].length();
                    //i < j
                    if (len2 < len1)
                        filtered[j] = null;
                    else
                        //i > j
                        filtered[i] = null;

                    continue;
                }

                if (filtered[j].contains(cur)) { // equal is included
                    filtered[i] = null;
                } else if (cur.contains(filtered[j])) {
                    filtered[j] = null;
                }

            }

        }

        StringBuilder res = new StringBuilder();

        // output the remaining words
        for (int i = 0; i < filtered.length; i++) {
            if (filtered[i] != null && filtered[i].length() > 0)
                res.append(words[i].replaceAll("\\s+", " ") + "|");
        }

        return res.substring(0, res.length() - 1);
    }

    // take care of the space / specials
    private static String filterHelper(String s) {
        //remove multiple whitespaces to one whitespace
        s = s.trim().replaceAll("\\s+", " ");
        System.out.println("PreProcess: " + s);
        s = s.replaceAll("[^A-Za-z0-9\\s]", "");
        s = s.toLowerCase();
        System.out.println("After: " + s.toString());
        return s;
        /*
        String[] words = s.split("\\s");

        StringBuilder sb = new StringBuilder();

        // remove
        for (int i = 0; i < words.length; i++) {

            char[] chars = words[i].toCharArray();

            String tmp = "";
            for (int j = 0; j < chars.length; j++)
                if (Character.isLetterOrDigit(chars[j])) {
                    tmp += Character.toLowerCase(chars[j]);
                }

            sb.append(tmp);
            sb.append(" ");
        }
        
        return sb.substring(0, sb.length() - 1);
        */
    }
```

```java
    public static String reverse(String s) {
        if (s == null || s.length() == 0) return "";
        
        String[] words = s.split("\\s");
        System.out.println(Arrays.toString(words));
        StringBuilder sb = new StringBuilder();
        for (int i = words.length - 1; i >= 0; i--) {
            String reversed = reverseHelper(words[i]);
            sb.append(reversed + " ");
        }
        return sb.substring(0, sb.length() - 1);
    }
    
    private static String reverseHelper(String s) {
        if (s.length() == 1) return s;
//        char[] chars = s.toLowerCase().toCharArray();
//        int i = 0;
//        int j = s.length() - 1;
//        while (i < j) {
//            char tmp = chars[i];
//            chars[i] = chars[j];
//            chars[j] = tmp;
//            i++;
//            j--;
//        }
//        chars[0] = Character.toUpperCase(chars[0]);
        String s2 = new StringBuilder(s.toLowerCase()).reverse().toString();
        Character c = Character.toUpperCase(s2.charAt(0));
        String res = c + s2.substring(1);
        return res;
    }
```