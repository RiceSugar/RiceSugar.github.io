---
title: "Java笔记"
tags: [ "Java", "Note" ]
date: 2022-04-14
description: "含有Java的编译知识，以及一些和其他语言不同的注意事项"
slug: "java-note"
---

# JDK

### java
>java -jar jarname.jar

### javac
- 单文件编译
>javac filepath -d foldername

- 复杂的包结构编译
- filepaths.txt要在要编译的文件夹外面
>javac @filepaths.txt -d foldername 

### jar
- MANIFEST要放在要打包的class文件夹外面
>jar cvfm jarname MANIFEST.MF -C classfoldername/ .
```
MANIFEST:
Manifest-Version: 1.0
Created-By: 17.0.5 (Oracle Corporation)
Main-class: （编译后class文件夹的主程序位置）（注意冒号后有一个空格）
```

### javadoc
>javadoc -d folderpath packagepath1 packagepath2

# 环境变量配置
- 在环境变量中创建 `JAVA_HOME` ，将其设置为 `JDK 1.8` 目录，不要添加多个路径，防止部分软件无法识别
- 在 `Path` 中添加 `%JAVA_HOME%\bin` 
- 添加环境变量 `classpath` 设置为 `.;%JAVA_HOME%libdt.jar;%JAVA_HOME%lib\tools.jar`


# 修饰符
- protected同包下继承的子类中，其他类中可调用，不同包下仅继承的子类中可调用
- 不写修饰符，仅同包下可调用

# 继承
- 可以使用父类作为形参，调用时调用父类的方法名，可以在同一方法下使用不同子类重写的方法
- 可以在`if`中使用`子类 instanceof 父类`来判断类型

# 接口
- 可用接口定义方法，接口中定义的变量默认为`public static final`
- 接口中定义的方法默认为`public abstract`
- 可使用接口实现不同的操作：声明接口变量，调用统一的接口方法，只需在声明变量时赋值不同的实现类，即可切换不同的实现方案

# 内部类
- 内部类可访问外部类的私有成员
- 内部类可访问外部类的静态成员
- 实现内部类`Outer.Inner inner  = new Outer.Inner();`

# 泛型
- 泛型方法
  - 实现: `private <T> T get(ArrayList<T> arrayList){}`
  - 区别：
    - 通配符同时支持上限和下限，泛型方法仅支持上限
    - 泛型方法可以保证形参和返回值类型一致，形参之间类型一致，通配符不能
    - 泛型方法支持多个边界，通配符不支持

# 容器

## 链表 LinkedList
## 数组 ArrayList
```java
ArrayList a = new ArrayList();
```
### ArrayList 转 Int[]
使用 stream 流
```java
int[] newArr = arr.stream().mapToInt(Integer::intValue).toArray();
```

## 队列 Queue
```java
Queue<Integer> q = new LinkedList<>();
```
#### 语法
- `add(E e)` 将指定的元素插入队列尾部，如果队列满，则抛出异常
- `remove()` 移除并返回队列头部的元素，如果队列为空，则抛出异常
- `element()` 返回队列头部的元素，但不移除，如果队列为空，则抛出异常
- `offer(E e) ` 将指定的元素插入队列尾部，如果队列满，则返回 `false`
- `poll()` 移除并返回队列头部的元素，如果队列为空，则返回  `null`
- `peek()` 返回队列头部的元素，但不移除，如果队列为空，则返回  `null`
- `isEmpty()` 判断队列是否为空
- `size()` 返回队列中元素的数量

### 优先队列 PriorityQueue
括号内为比较函数
```java
PriorityQueue<Integer> q = new PriorityQueue<>((a, b) -> a - b);
```

### 双端队列 Deque
```java
Deque<Integer> q = new ArrayDeque<>();
```

#### 语法
- `addFirst(E e)` 将指定的元素插入双端队列的开头
- `addLast(E e)` 将指定的元素插入双端队列的末尾
- `removeFirst()` 移除并返回双端队列的第一个元素，如果队列为空，则抛出异常
- `removeLast()` 移除并返回双端队列的最后一个元素，如果队列为空，则抛出异常。
- `getFirst()` 返回双端队列的第一个元素，但不移除，如果队列为空，则抛出异常
- `getLast()` 返回双端队列的最后一个元素，但不移除，如果队列为空，则抛出异常。
- `offerFirst(E e)` 将指定的元素插入双端队列的开头，如果队列满，则返回 `false`
- `offerLast(E e)` 将指定的元素插入双端队列的末尾，如果队列满，则返回 `false`
- `pollFirst()` 移除并返回双端队列的第一个元素，如果队列为空，则返回 `null`
- `pollLast()` 移除并返回双端队列的最后一个元素，如果队列为空，则返回 `null`
- `peekFirst()` 返回双端队列的第一个元素，但不移除，如果队列为空，则返回 `null`
- `peekLast()` 返回双端队列的最后一个元素，但不移除，如果队列为空，则返回 `null`
-  `isEmpty()` 判断双端队列是否为空
- `size()` 返回双端队列中元素的数量

## 栈 Stack
```java
Stack<String> stack = new Stack<>();
```
### 语法
- `push(E item)`：将元素压入栈顶。
- `pop()`：从栈顶弹出元素。
- `peek()`：获取栈顶元素但不移除。
- `isEmpty()`：判断栈是否为空。
- `size()`：获取栈中元素的个数。
- `search(Object o)`：搜索指定元素在栈中的位置，返回相对于栈顶的位置（从1开始计数），如果不存在则返回 -1。
- `clear()`：清空栈中的所有元素。


# JDBC编程
```JAVA
String url = "jdbc:mysql://localhost:3306/mydatabase";
String username = "root";
String password = "password";
Connection connection = null;
try {
    // 加载数据库驱动
    Class.forName("com.mysql.jdbc.Driver");

    // 建立数据库连接
    connection = DriverManager.getConnection(url, username, password);

    // 执行数据库操作
} catch (ClassNotFoundException e) {
    e.printStackTrace();
} catch (SQLException e) {
    e.printStackTrace();
} finally {
    // 关闭数据库连接
    if (connection != null) {
        try {
            connection.close();
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```