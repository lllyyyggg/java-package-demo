## java的编译

目录结构如下

```
java-package/com//a/A.java
java-package/com/lanyage/b/B.java
```

`A.java`

```
package com.lanyage.a;
public class A {
	public String getName() {
		return "This is a";
	}
}
```

`B.java`

```
package com.lanyage.b;
import com.lanyage.a.A;
public class B {
	public static void main(String[] args) {
		A a = new A();
		System.out.println(a.getName());
	}
}
```

然后在`java-package`目录下执行`$ javac com/lanyage/b/B.java`，然后就会将`B`和`A`依赖的文件都编译了，并且在`java`文件的同集目录下生成`.class`文件。


## java有第三方的依赖jar包如何编译
同上面的目录结构一样，先编译`com/lanyage/a/A.java`文件。

因为`B`依赖`A`,现将`A.class`打包成`jar`。

在`java-package`目录下， 执行

```
jar -cvf A.jar com/lanyage/a/*.class
```
就会在`java-package`目录下生成一个`A.jar`文件。

然后执行

```
$ mkdir /Users/lanyage/git/java-package/dest
$ javac -d /Users/lanyage/git/java-package/dest com/lanyage/b/B.java
```
就会在`/Users/lanyage/git/java-package/dest`目录下创建好`com/lanyage/b/B.class`。

切换到`/Users/lanyage/git/java-package/dest`目录。执行。

```
java -cp .:/Users/lanyage/git/java-package/A.jar com/lanyage/b/B

or

java -cp .:../a.jar com/lanyage/b/B
```
就可以将程序跑起来了。`.:`后面的`jar`可以有多个。


如果想要运行一个有第三方依赖的程序的话。

```
java -cp .:./lib/log4j-1.2.17.jar:./lib/slf4j-api-1.7.25.jar:./lib/slf4j-log4j12-1.7.25.jar com/lanyage/datamining/run/CPTreeConstructor
```

其中`.:./lib/log4j-1.2.17.jar:./lib/slf4j-api-1.7.25.jar:./lib/slf4j-log4j12-1.7.25.jar`是依赖的三方`jar`包。windows使用`;`来代替`:`。





