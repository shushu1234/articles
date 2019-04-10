# org.apache.commons.io.FileUtils Example

> 这篇文章我们会介绍FileUtils类相关的功能，它也是Apache Commons IO的一部分。它所提供的方法将我们常用的任务进行了包装，使我们写的代码更简洁易读。

## 1. FileUtils方法

我将介绍FileUtils类中一些重要的方法，并详细说明它们如何使用。FileUtils是一个静态类，这样意味着我们可以不用实例化就可以直接通过类去调用方法。

* `contentEquals(File file1, File file2)`：比较两个文件的内容，返回比较的结果。
* `copyDirectory(File source, File destination)`：复制整个文件夹到另外一个地方。
* `copyDirectory(File source, File destination, FileFilter filter)`：作用跟上面的方法类似，不过我们可以过滤一些指定的文件（比如名字，修改时时间等等）
* `copyFile(File srcFile, File destFile)`：拷贝一个文件到另外一个文件
* `deleteDirectory(File directory)`：递归的删除一个文件夹
* `getTempDirectory()`：返回表示系统临时目录的File对象
* `getUserDirectory()`：与上面相同，但这次代表用户目录。
* `lineIterator(File file)`：它创建了一个迭代器，可以按行遍历给定的文件。
* `sizeOfDirectory(File directory)`：它返回目录内容的大小
* `write(File file, CharSequence data)`：使用指定的编码将CharSequence写入文件中。
* `writeLines(File file, Collection<?> lines)`：将集合按行写入到文件中

## 2. FileUtils例子

```java
import org.apache.commons.io.FileUtils;
import org.apache.commons.io.LineIterator;
import org.apache.commons.io.filefilter.SuffixFileFilter;
import org.testng.annotations.Test;

import java.io.File;
import java.io.IOException;

/**
 * @ClassName FileUtilsTest
 * @Description:
 * @Author: liuyao
 * @Date: 2019/4/10 9:50
 * @Version: 1.0
 **/
public class FileUtilsTest {
    private static final String MAIN_PATH = "D:\\Workspace\\IdeaProjects" +
            "\\pms_study\\src\\main\\java\\commonsio\\";

    @Test
    public void test() throws IOException {
        File file1 = FileUtils.getFile(MAIN_PATH + "cmpFile1.txt");
        File file2 = FileUtils.getFile(MAIN_PATH + "cmpFile2.txt");
        System.out.println("Are cmpFile1 and cmpFile2 equal: " + FileUtils.contentEquals(file1, file2));

//        拷贝文件夹
        FileUtils.copyDirectory(FileUtils.getFile(MAIN_PATH),
                FileUtils.getFile(MAIN_PATH+"copiedPath\\"));

        System.out.println("Does the copiedPath exist: " + FileUtils.getFile(MAIN_PATH + "copiedPath\\").exists());

//        只拷贝后缀为txt的文件
        FileUtils.copyDirectory(FileUtils.getFile(MAIN_PATH),
                FileUtils.getFile(MAIN_PATH + "copiedFilterPath\\"),
                new SuffixFileFilter(".txt"));

//        输出该文件夹下的所有文件名
        for (File f : FileUtils.getFile(MAIN_PATH + "copiedFilterPath\\").listFiles()) {
            System.out.println("Contents of copiedFilterPath: " + f.getName());
        }

//        拷贝文件
        File copy=FileUtils.getFile(MAIN_PATH+"copyOfFile1.txt");
        FileUtils.copyFile(file1,copy);
        System.out.println("Are cmpFile1 and copyOfFile1 equal: " +
                FileUtils.contentEquals(file1, copy));

//        删除文件夹
        FileUtils.deleteDirectory(FileUtils.getFile(MAIN_PATH + "copiedFilterPath\\"));
        for (File f: FileUtils.getFile(MAIN_PATH).listFiles()) {
            System.out.println("Contents of MAIN_PATH after deletion: " + f.getName());
        }

//        获得系统临时目录
        System.out.println("Temp Dir: "+FileUtils.getTempDirectory().getAbsolutePath());
//        获得用户目录
        System.out.println("User Dir: "+FileUtils.getUserDirectory().getAbsolutePath());

//        按行遍历文件
        LineIterator iterator=FileUtils.lineIterator(file2);
        while (iterator.hasNext()){
            System.out.println("cmpFile2 lines:"+iterator.next());
        }

//        统计文件夹大小
        System.out.println("Size of Dir:"+FileUtils.sizeOfDirectory(FileUtils.getFile(MAIN_PATH))+" bytes");

//        将字符序列写入文件
        File fileToWrite1 = FileUtils.getFile(MAIN_PATH + "fileToWrite1.txt");
        FileUtils.write(fileToWrite1,"ccccccccc");
        iterator=FileUtils.lineIterator(fileToWrite1);
        while (iterator.hasNext()) {
            System.out.println("fileToWrite1 lines: " + iterator.next());
        }

    }
}

```

输出结果为：

```
Are cmpFile1 and cmpFile2 equal: false
Does the copiedPath exist: true
Contents of copiedFilterPath: cmpFile1.txt
Contents of copiedFilterPath: cmpFile2.txt
Contents of copiedFilterPath: copyOfFile1.txt
Contents of copiedFilterPath: fileToWrite1.txt
Contents of copiedFilterPath: test.txt
Are cmpFile1 and copyOfFile1 equal: true
Contents of MAIN_PATH after deletion: cmpFile1.txt
Contents of MAIN_PATH after deletion: cmpFile2.txt
Contents of MAIN_PATH after deletion: copiedPath
Contents of MAIN_PATH after deletion: copyOfFile1.txt
Contents of MAIN_PATH after deletion: fileToWrite1.txt
Contents of MAIN_PATH after deletion: FileUtilsTest.java
Contents of MAIN_PATH after deletion: Git.png
Contents of MAIN_PATH after deletion: IOUtilsTest.java
Contents of MAIN_PATH after deletion: test.txt
Temp Dir: C:\Users\liuyao\AppData\Local\Temp
User Dir: C:\Users\liuyao
cmpFile2 lines:Hello World!!!!
cmpFile2 lines:asdf
Size of Dir:63814 bytes
fileToWrite1 lines: ccccccccc
```

