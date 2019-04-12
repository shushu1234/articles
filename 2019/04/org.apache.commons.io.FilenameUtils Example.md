# org.apache.commons.io.FilenameUtils Example

> FilenameUtils是Apache Commons IO下面的一个工具类，主要用于处理文件名和文件夹名等相关的操作。

## 1. 文件名字常用属性

该类含有六个重要属性作为文件名，我们采用例子

```
X:\JCG\articles\org.apache.commons.io.FilenameUtils Example\notes.txt
```

- `X:\` ：盘符首部
- `JCG\articles\org.apache.commons.io.FilenameUtils Example\` ：不带盘符的路径
- `X:\JCG\articles\org.apache.commons.io.FilenameUtils Example\`：完整路径
- `notes.txt`：名字
- `notes`：基本名字
- `txt`：扩展名

下面这个例子我们将获取这六个属性

```java
import org.apache.commons.io.FilenameUtils;
 
public class FilenameUtilsExample1 {
 
    public static void main(String [] args) {
             
        filenameComponents_();
    }
 
    private static void filenameComponents_() {
     
        String filename = "X:\\JCG\\articles\\org.apache.commons.io.FilenameUtils Example\\notes.txt";
     
        System.out.println("*** File name components ***");
        System.out.println("File name: " + filename);
     
        String prefix = FilenameUtils.getPrefix(filename);
        System.out.println("Prefix: " + prefix);
         
        String path = FilenameUtils.getPath(filename);
        System.out.println("Path: " + path);
         
        String fullPath = FilenameUtils.getFullPath(filename);
        System.out.println("Full path: " + fullPath);
         
        String name = FilenameUtils.getName(filename);
        System.out.println("Name: " + name);
         
        String baseName = FilenameUtils.getBaseName(filename);
        System.out.println("Base name: " + baseName);
         
        String extension = FilenameUtils.getExtension(filename);
        System.out.println("Extension: " + extension);
    }
}
```

输出结果为：

```
*** File name components ***
File name: X:\JCG\articles\org.apache.commons.io.FilenameUtils Example\notes.txt
Prefix: X:\
Path: JCG\articles\org.apache.commons.io.FilenameUtils Example\
Full path: X:\JCG\articles\org.apache.commons.io.FilenameUtils Example\
Name: notes.txt
Base name: notes
Extension: txt
```

## 2. 路径规范化

规范化文件路径即删除双（..）和单（.）点路径。此方法适用于Windows以及unix系统。

```java
import org.apache.commons.io.FilenameUtils;
 
public class FilenameUtilsExample1 {
 
    public static void main(String [] args) {
             
        normalize_();
    }
 
    private static void normalize_() {
     
        System.out.println("*** Normalization ***");
 
        String filename = "X:\\JCG\\.\\org.apache.commons.io.FilenameUtils Example\\notes.txt";
        System.out.println("Before: " + filename);
        String normalized = FilenameUtils.normalize(filename);
        System.out.println("After single dot normalization: " + normalized);
         
        filename = "X:\\JCG\\articles\\..\\notes.txt";
        System.out.println("Before: " + filename);
        normalized = FilenameUtils.normalize(filename);
        System.out.println("After double dot normalization: " + normalized);    
    }
}
```

输出结果为：

```
*** Normalization ***
Before: X:\JCG\.\org.apache.commons.io.FilenameUtils Example\notes.txt
After single dot normalization: X:\JCG\org.apache.commons.io.FilenameUtils Example\notes.txt
 
Before: X:\JCG\articles\..\notes.txt
After double dot normalization: X:\JCG\notes.txt
```

我们可以看到对于 `..`即回到上级，`.`直接删除。

## 3. 文件名比较

使用 `equals()`方法对两个文件名进行比较，并返回结果：

```java
import org.apache.commons.io.FilenameUtils;
 
public class FilenameUtilsExample1 {
 
    public static void main(String [] args) {
             
        equals_();
    }
 
    private static void equals_() {
     
        System.out.println("*** File name equality ***");
     
        String filename1 = "FilenameUtilsExample.java";
        String filename2 = "FilenameUtilsExample.java";
        System.out.println("Filename 1: " + filename1);
        System.out.println("Filename 2: " + filename2);
        boolean result = FilenameUtils.equals(filename1, filename2);
        System.out.println("Equals: " + result);
         
        filename1 = null;
        System.out.println("Filename 1: " + filename1);
        System.out.println("Filename 2: " + filename2);
        result = FilenameUtils.equals(filename1, filename2);
        System.out.println("Equals: " + result);
    }
}
```

输出结果为：

```
*** File name equality ***
Filename 1: FilenameUtilsExample.java
Filename 2: FilenameUtilsExample.java
Equals: true
 
Filename 1: null
Filename 2: FilenameUtilsExample.java
Equals: false
```

## 4. 文件名连接

使用contact()方法对两个文件名进行连接操作，并返回一个规范化的路径：

```java
import org.apache.commons.io.FilenameUtils;
 
public class FilenameUtilsExample1 {
 
    public static void main(String [] args) {
             
        concat_();
    }
 
    private static void concat_() {
     
        System.out.println("*** Concatenation ***");
     
        // base and added names are paths
        String filename1 = "X:\\JCG\\Examples\\org.apache.commons.io.FilenameUtils";
        String filename2 = "articles\\";
        String concatenatedPath = FilenameUtils.concat(filename1, filename2);
        System.out.println("Filename 1: " + filename1 );
        System.out.println("Filename 2: " + filename2 );
        System.out.println("Concatenated: " + concatenatedPath);
         
        // base is path and added name is file name
        filename1 = "X:\\JCG\\Examples\\org.apache.commons.io.FilenameUtils";
        filename2 = "FilenameUtilsExample.java";
        concatenatedPath = FilenameUtils.concat(filename1, filename2);
        System.out.println("Filename 1: " + filename1 );
        System.out.println("Filename 2: " + filename2 );
        System.out.println("Concatenated: " + concatenatedPath);
         
        // base is reative path and added name is file name
        filename1 = "org.apache.commons.io.FilenameUtils";
        filename2 = "FilenameUtilsExample.java";
        concatenatedPath = FilenameUtils.concat(filename1, filename2);
        System.out.println("Filename 1: " + filename1 );
        System.out.println("Filename 2: " + filename2 );
        System.out.println("Concatenated: " + concatenatedPath);    
    }
}
```

输出结果为：

```
*** Concatenation ***
Filename 1: X:\JCG\Examples\org.apache.commons.io.FilenameUtils
Filename 2: articles\
Concatenated: X:\JCG\Examples\org.apache.commons.io.FilenameUtils\articles\
 
Filename 1: X:\JCG\Examples\org.apache.commons.io.FilenameUtils
Filename 2: FilenameUtilsExample.java
Concatenated: X:\JCG\Examples\org.apache.commons.io.FilenameUtils\FilenameUtilsExample.java
 
Filename 1: org.apache.commons.io.FilenameUtils
Filename 2: FilenameUtilsExample.java
Concatenated: org.apache.commons.io.FilenameUtils\FilenameUtilsExample.java
```

## 5. 分隔符转换

此类定义将路径分隔符从unix（/）转换为Windows（\）的方法，反之亦然。

以下示例显示了两个方法`separatorsToUnix()`和`separatorsToSystem()`的用法。还有一个方法`separatorsToWindows()`将路径分隔符转换为Windows系统（\）

```java
import org.apache.commons.io.FilenameUtils;
 
public class FilenameUtilsExample1 {
 
    public static void main(String [] args) {
             
        separators_();
    }
 
    private static void separators_() {
     
        System.out.println("*** Separator conversion ***");
     
        String filename = "X:\\JCG\\articles\\org.apache.commons.io.FilenameUtils Example\\notes.txt";
        System.out.println("File name: " + filename);
        filename = FilenameUtils.separatorsToUnix(filename);
        System.out.println("File name after separatorsToUnix(): " + filename);
 
        filename = "/JCG/articles/org.apache.commons.io.FilenameUtils Example/notes.txt";
        System.out.println("File name: " + filename);
        filename = FilenameUtils.separatorsToSystem(filename);
        System.out.println("File name after separatorsToSystem(): " + filename);
   }
}
```

输出结果为：

```
*** Separator conversion ***
File name: X:\JCG\articles\org.apache.commons.io.FilenameUtils Example\notes.txt
File name after separatorsToUnix(): X:/JCG/articles/org.apache.commons.io.FilenameUtils Example/notes.txt
 
File name: /JCG/articles/org.apache.commons.io.FilenameUtils Example/notes.txt
File name after separatorsToSystem(): \JCG\articles\org.apache.commons.io.FilenameUtils Example\notes.txt
```

