---
title: "Java笔记"
tags: [ "Java", "Note" ]
date: 2022-04-14
description: "含有Java的编译知识，以及一些和其他语言不同的注意事项"
slug: "java-note"
---

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


### 修饰符
- protected同包下继承的子类中，其他类中可调用，不同包下仅继承的子类中可调用
- 不写修饰符，仅同包下可调用

### 继承
- 可以使用父类作为形参，调用时调用父类的方法名，可以在同一方法下使用不同子类重写的方法
- 可以在`if`中使用`子类 instanceof 父类`来判断类型

### 接口
- 可用接口定义方法，接口中定义的变量默认为`public static final`
- 接口中定义的方法默认为`public abstract`
- 可使用接口实现不同的操作：声明接口变量，调用统一的接口方法，只需在声明变量时赋值不同的实现类，即可切换不同的实现方案

### 内部类
- 内部类可访问外部类的私有成员
- 内部类可访问外部类的静态成员
- 实现内部类`Outer.Inner inner  = new Outer.Inner();`

### 泛型
- 泛型方法
  - 实现: `private <T> T get(ArrayList<T> arrayList){}`
  - 区别：
    - 通配符同时支持上限和下限，泛型方法仅支持上限
    - 泛型方法可以保证形参和返回值类型一致，形参之间类型一致，通配符不能
    - 泛型方法支持多个边界，通配符不支持

### API


### JDBC编程
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