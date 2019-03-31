# JVM, JDK, JRE: What's the difference?

> 三个必不可少的Java平台组件，它们如何在你的Java程序中协同工作的呢？

新的Java开发者常常对 ` Java Virtual Machine`、` Java Development Kit`、` Java Runtime Environment`感到困惑。也好奇这个三个组件是如何在Java程序中协同工作的？

**下面作简介的说明：**

* JVM是执行你的程序的Java平台组件
* JRE创建了JVM并且确保了你的程序的依赖能够被使用
* JDK允许您创建可由JVM和JRE执行和运行的Java程序

作为一个开发者，你将通过JDK写你的程序，然后通过JVM调试并且优化它们，特别是性能。JRE大多数时间工作在后台，但您可以将它用于程序监视和内存配置

**下载并安装JVM、JDK和JRE：**

当你下载[JDK](https://www.oracle.com/technetwork/java/javase/downloads/index.html)时，它里面已经包含了一个与之版本兼容的JRE，而JRE将里面又包含了一个默认的JVM，你可以从JDK中单独下载[JRE](https://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html)，然后也可以选择不同版本的[JVM](https://en.wikipedia.org/wiki/List_of_Java_virtual_machines)
