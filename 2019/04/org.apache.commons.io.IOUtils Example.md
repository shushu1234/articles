# org.apache.commons.io.IOUtils Example

在下面的例子，我们将详细说明如何使用 `org.apache.commons.io` 包中的 `IOUtils`类如何使用，通过包名我们可以知道它是 Apache Commons IO 的一部分 。该类的所有成员函数都被用来处理输入 - 输出流，它的确非常利于来编写处理此类事务的程序。`IOUtils`与其他Apache Commons中的类一样，都是处理IO操作的非常重要包装器，与手动编写这些功能的其他程序相比，它们实现这些方法的代码变得更小，更清晰，更易理解。

## 1. IOUtils类，字段和方法简介

IOUtils类的所有成员字段和方法都是静态的，因此在标准编程中不需要创建IOUtils类的对象，而是通过类名和适当的方法名来使用它。如:`IOUtils.method1 ()`。

### 1.1 IOUtils 字段

* `static char DIR_SEPARATOR`：目录分隔符
* `static char DIR_SEPARATOR_UNIX`：Unix系统的目录分隔符
* `static char DIR_SEPARATOR_WINDOWS`：Windows系统的目录分隔符
* `static String LINE_SEPARATOR`：行分隔符
* `static String LINE_SEPARATOR_UNIX`：Unix系统的行分隔符
* `static String LINE_SEPARATOR_WINDOWS`：Windows系统的行分隔符

### 1.2 IOUtils 方法摘要

现在我们将要讨论的是IOUtils中的一些非常重要的方法。类中的所有处理InputStream的方法都带有内部的缓冲区，所以我们不需要再使用 `BufferedReader`或者 `BufferedInputStream`，默认的缓冲区大小为4K，不过我们也可以自定义它的大小。

* `static void closeQuietly(Closeable closeable)`：
* `static boolean contentEquals(Reader inp1,Reader inp2)`
* `static int copy(InputStream inp,OutputStream outp)`
* `static LineIterator lineIterator(InputStream input,String enc)`
* `static List<String> readLines(InputStream inp,String enc)`
* `static List<String> readLines(Reader inp)`
* `static BufferedReader toBufferedReader(Reader rdr, int size)`
* `static InputStream toInputStream(CharSequence inp, String enc)`
* `static String toString(Reader inp)`
* `static void write(String data,Writer outp)`
* `static void writeLines(Collection<?> lines,String lineEnding,Writer outp)`
