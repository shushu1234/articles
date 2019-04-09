# IOUtils使用介绍

在下面的例子，我们将详细说明如何使用 `org.apache.commons.io` 包中的 `IOUtils`类如何使用，通过包名我们可以知道它是 Apache Commons IO 的一部分 。该类的所有成员函数都被用来处理输入 - 输出流，它的确非常利于来编写处理此类事务的程序。`IOUtils`与其他Apache Commons中的类一样，都是处理IO操作的非常重要包装器，与手动编写这些功能的其他程序相比，它们实现这些方法的代码变得更小，更清晰，更易理解。

## 1. IOUtils类，字段和方法简介

IOUtils类的所有成员字段和方法都是静态的，因此在标准编程中不需要创建IOUtils类的对象，而是通过类名和适当的方法名来使用它。如:`IOUtils.method1 ()`。

## 2. IOUtils 字段

- `static char DIR_SEPARATOR`：目录分隔符
- `static char DIR_SEPARATOR_UNIX`：Unix系统的目录分隔符
- `static char DIR_SEPARATOR_WINDOWS`：Windows系统的目录分隔符
- `static String LINE_SEPARATOR`：行分隔符
- `static String LINE_SEPARATOR_UNIX`：Unix系统的行分隔符
- `static String LINE_SEPARATOR_WINDOWS`：Windows系统的行分隔符

## 3. IOUtils 方法摘要

现在我们将要讨论的是IOUtils中的一些非常重要的方法。类中的所有处理InputStream的方法都带有内部的缓冲区，所以我们不需要再使用 `BufferedReader`或者 `BufferedInputStream`，默认的缓冲区大小为4K，不过我们也可以自定义它的大小。

- `static void closeQuietly(Closeable closeable)`：它将无条件的关闭一个可被关闭的对象而不抛出任何异常。它也有很多版本去支持关闭所有的InputStream、OutputStream、Reader和Writer。
- `static boolean contentEquals(Reader inp1,Reader inp2)`：这个方法将比较两个Reader对象的内容是否相同，相同返回true，否则返回false。它还有另外的一个版本去比较InputStream对象。还有一个方法 `contentEqualsIgnoreEOL(Reader r1,Rrader r2)`，它将忽略行结束符而比较内容。
- `static int copy(InputStream inp,OutputStream outp)`：这个方法将内容按字节从一个InputStream对象复制到一个OutputStream对象，并返回复制的字节数。同样有一个方法支持从Reader对象复制到Writer对象。
- `static LineIterator lineIterator(InputStream input,String enc)`：这个方法将从InputStream中返回一个行迭代器，我们可以指定一个字符格式（或者为空而使用默认的）。行迭代器将持有一个打开的InputStream的引用。当你迭代结束后，应当关闭stream来释放内部资源。这个字符编码也可以是一个字符集对象。同样也有一个方法支持Reader对象。
- `static List<String> readLines(InputStream inp,String enc)`
- `static List<String> readLines(Reader inp)`
- `static BufferedReader toBufferedReader(Reader rdr, int size)`
- `static InputStream toInputStream(CharSequence inp, String enc)`
- `static String toString(Reader inp)`
- `static void write(String data,Writer outp)`
- `static void writeLines(Collection<?> lines,String lineEnding,Writer outp)`

## 4. 方法使用

1. `IOUtils.toInputStream()`方法

   ```java
   InputStream is=IOUtils.toInputStream("This is a String","utf-8");
   ```

   `IOUtils.toInputStream()`方法为*"This is a String"*创建一个InputStream，并返回该对象。

2. `IOUtils.closeQuietly()`方法

   ```java
   public void test2() throws IOException {
       InputStream is=IOUtils.toInputStream("This is a String","utf-8");
       OutputStream os=new FileOutputStream("test2.txt");
       int bytes=IOUtils.copy(is,os);
       System.out.println("File Written with "+bytes+" bytes");
       IOUtils.closeQuietly(os);
   }
   ```

   我们可以方便的关闭输出流而不用抛出异常，我们打开它的源码看看：

   ```java
   @Deprecated
   public static void closeQuietly(final Closeable closeable) {
       try {
           if (closeable != null) {
           	closeable.close();
           }
       } catch (final IOException ioe) {
           // ignore
       }
   }
   ```

   可见，它跟我们传统的关闭输出流是一样的，没什么区别，不过我们可以看见它已经被废弃了，现在推荐的是利用Java7引入的 `try-with-resources`方式来关闭。

   ```java
   @Test
   public void test2() throws IOException {
       try (InputStream is = IOUtils.toInputStream("This is a String", "utf-8");
            OutputStream os = new FileOutputStream("test2.txt")) {
           int bytes = IOUtils.copy(is, os);
           System.out.println("File Written with " + bytes + " bytes");
       }
   }
   ```

   更多关于 `try-with-resources`可以看 [try-with-resources 和 multi-catch](https://www.jianshu.com/p/3022f7daa2a4)

3. `IOUtils.copy()`方法

   ```java
   public void test2() throws IOException {
       try (InputStream is = IOUtils.toInputStream("This is a String", "utf-8");
            OutputStream os = new FileOutputStream("test2.txt")) {
           int bytes = IOUtils.copy(is, os);
           System.out.println("File Written with " + bytes + " bytes");
       }
   }
   ```

   `IOUtils.copy()`方法有很多版本，我这里举例的是最常用的方法，同时还有一个`IOUtils.copyLarge()`方法支持复制（不超过2GB）的InputStream或者Reader对象。

4. `IOUtils.toString()`方法

   ```java
   FileReader fileReader = new FileReader("test2.txt"));
   System.out.println(IOUtils.toString(fileReader));
   ```

   和上面所看到的toString方法类似，IOUtils有支持 `InputStream`、`URI`和 `URL`的方法，它们都需要指定字符集。

5. `IOUtils.read()`方法

   ```java
   @Test
   public void test4(){
       try(FileInputStream fin=new FileInputStream("test2.txt")){
           byte[] buf= new byte[100];
           int len=IOUtils.read(fin,buf);
           System.out.println("The Length of Input Stream:"+len);
       }catch (IOException e){
           e.printStackTrace();
       }
   }
   ```

   该方法从InputStream中读取bytes并返回一个`byte[]`。之后我们可以对该byte[]数组进行操作。有些时候该方法非常有用，但是我们建议使用readlines()方法。

6. `IOUtils.writeLines()`方法

   ```java
   @Test
   public void test5() {
       try (FileInputStream fin = new FileInputStream("test2.txt")) {
           List ls = IOUtils.readLines(fin, "utf-8");
           for (int i = 0; i < ls.size(); i++) {
               System.out.println(ls.get(i));
           }
       } catch (IOException e) {
           e.printStackTrace();
       }
   }
   ```

   我们可以将InputStream的内容作为字符串列表，然后对其进行操作。

7. `IOUtils.writeLines()`方法

   ```java
   @Test
   public void test6(){
       List<String> ls=new ArrayList<>();
       ls.add("asdasd");
       ls.add("ada21");
       ls.add("addsf");
       try(OutputStream os=new FileOutputStream("test3.txt")) {
           IOUtils.writeLines(ls,IOUtils.LINE_SEPARATOR_WINDOWS,os);
       } catch (IOException e) {
           e.printStackTrace();
       }
   }
   ```

8. `LineIterator` 类和 `lineIterator()` 方法

   ```java
   @Test
   public void test7(){
       try(FileInputStream fin=new FileInputStream("test2.txt")){
           LineIterator lt=IOUtils.lineIterator(fin,"utf-8");
           while (lt.hasNext()){
               String line=lt.nextLine();
               System.out.println(line);
           }
       }catch (IOException e){
           e.printStackTrace();
       }
   }
   ```

   通过`lineIterator`方法返回一个`LineIterator`对象，然后进行迭代。

9. `IOUtils.write()`方法

   ```java
   @Test
   public void test8(){
       try(OutputStream os=new FileOutputStream("test4.txt")){
           IOUtils.write("sahjsdhjad",os,"utf-8");
       }catch (IOException e){
           e.printStackTrace();
       }
   }
   ```

   我们可以通过IOUtils.write()方法将String写到一个Writer对象或者OutputStream对象中去。
