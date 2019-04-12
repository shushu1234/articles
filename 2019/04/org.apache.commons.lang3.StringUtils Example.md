# org.apache.commons.lang3.StringUtils Example

> 在本文章中，我们将介绍StringUtils的使用方法，正如它的名字一样，它是Apache Commons Lang中的一员，被用来处理字符串的常用操作，它对我们一些常用的操作进行了包装，相比于我们自己写的代码，使用它会显得更加小巧，简介和易读。

## 1. 简介

在Apache Commons包中，有两个StringUtils类，一个是`org.apache.commons.lang.StringUtils`（Commons Lang 2.x API），另外一个是 `org.apache.commons.lang3.StrinUtils`（Commons Lang 3.1x API及以后版本），我们这里讨论的是最新的版本。StringUtils中所有成员都是static的，所以我们不用自己手动创建对象，直接通过类名就可以调用了。

## 2. StringUtils属性

- `static String CR`: 回车字符`\r`
- `static String EMPTY`: 空字符串`""`
- `static int INDEX_NOT_FOUND`:索引搜索失败 -1
- `static String LF`: 换行字符 `\n`
- `static String SPACE`:空格字符 ` `

## 3. StringUtils方法摘要

1. `static String abbreviate(String str,int offset,int maxWidth)`：该方法将通过省略号简写str，offset是可选的参数，maxWidth是最后字符串的长度，不能太小，如果小于4的话将会抛出异常（省略号是三个）。
2. `static String abbreviateMiddle(String str,String middle,int length)`：该方法是将str中间的字符用指定的middle字符替代，length是最后所得的字符长度。
3. `static String appendIfMissing(String str,CharSequence suffix,CharSequence... suffixes)`：该方法是如果str末尾缺少了给定的后缀suffixes，那么自动在str后面添加上后缀suffix。同理还有`prependIfMissing(String str,CharSequence prefix,CharSequence... prefixes)`给字符添加前缀。
4. `static String center(String str,int Size,char padChar)`：该方法将扩大字符串的长度，如果str的长度小于给定的Size，那么将把str放在新的字符串中间，并在左右用padChar填充，同理还有但对对左或右进行填充的`leftPad(String str,int size,char padChar)`或`rightPad(String str,int size,char padChar)`。
5. `static String chomp(String str)`：该方法从str的末尾删除一个换行字符，如果存在换行字符存在的话，换行字符包括 `\n`、`\r`、`\r\n`。
6. `static String chop(String str)`：该方法将删除str末尾的一个字符，字符包括 `\n`、`\r`、`\r\n`或者字母数字等。
7. `static boolean contains(CharSequence str,CharSequence searchStr)`：该方法将判断str中是否包含searchStr，如果存在则返回true，否则返回false。与之相对的是`containsNone(CharSequence cs, char... searchChars)`判断是否不包含。
8. `static String deleteWhitespace(String str)`：删除str中的whitespace，whitespace指的是Character.isWhitespace（char）定义的字符。
9. `static String difference(String str1,String str2)`：以str1作为源字符，str2作为比较字符，返回str2不在str1中的字符。
10. `static boolean endsWith(CharSequence str,CharSequence suffix)`：检查str是否以suffix作为结尾，并返回结果，如果两个str和suffix都为null的话讲返回true。同理还有`static boolean startsWith(CharSequence str,CharSequence preffix)`检查前缀字符。
11. `static boolean equals(CharSequence cs1,CharSequence cs2)`：该方法比较两个字符序列是否相等
12. `static String getCommonPrefix(String... strs)`：从给定的一个字符串数组中找出公共的前缀。
13. `static double getJaroWinklerDistance(CharSequence first,CharSequence second)`：根据Jaro Winkler算法计算两个序列的相似度。
14. `static int getLevenshteinDistance(CharSequence str1,CharSequence str2,int threshold)`：如果两个字符串之间的距离小于或等于给定的阈值，则此方法返回Levenshtein值(将一个字符串更改为另一个字符串所需的更改数量，其中每个更改都是单个字符修改)。阈值参数在lang3中是可选的。
15. `static boolean isAllBlank(final CharSequence... css)`:检查多个字符序列是否都是空字符("")、null、或者whitespace(空格、制表符\t、换行符\n、换页符\f和回车符\n )。
16. `static boolean isAllEmpty(final CharSequence... css)`：检查该多个符序列都是空字符("") 或者null。
17. `static boolean isAlpha(final CharSequence cs)`：检查该字符序列是否都是字母
18. `static boolean isAlphanumeric(final CharSequence cs)`：检查该字符序列是否只包含数字或字母。
19. `static boolean isAlphanumericSpace(final CharSequence cs)`：检查该字符学历是否只包含数字、字母或者空格。
20. `static boolean isAlphaSpace(final CharSequence cs)`：检查该字符序列是否只包含字母或空格。
21. `static boolean isBlank(final CharSequence cs)`：检查该字符是否都是空字符("")、null、或者whitespace(空格、制表符\t、换行符\n、换页符\f和回车符\n)。
22. `static boolean isEmpty(final CharSequence cs)`：检查该字符空字符("") 或者null。
23. `static String removeEnd(String str,String remove)`：如果源str是以remove字符串结尾的话，则删除，否则返回源str。同理还有`static String removeStart(String str,String remove)`
24. `static String repeat(String str,String separator,int repeat)`：该方法将str重复repeat次，并用separator隔开（separator是可选的）。
25. `static String replace(String text,String searchStr,String replacement,int n)`：该方法用于将text中的searchStr替换为replacement，从前往后一共替换n次。
26. `static String reverse(String str)`：用于字符串的反转，用的是StringBuilder的reverse()方法。
27. `static String[] split(String str,String separator,int max)`：将给定的字符串str按照separator进行分割，最多分割max次，并返回分割后的数组。
28. `static String strip(String str,String stripChars)`：去掉字符串str前后的stripChars
29. `static String swapCase(String str)`：将字符串str中的大写换成小写，小写换成大写。
30. `static String trim(String str)`：该方法删除str两端的控制字符（char<=32）。



