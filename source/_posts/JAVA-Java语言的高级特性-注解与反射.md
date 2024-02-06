---
title: JAVA基础|Java语言的高级特性-注解与反射

categories:
    - JAVA基础
tags:
    - 注解与反射
    - Retrofit 
    - JAVA
---
Retrofit中的注解反射与动态代理
# 注解 （标注）
* Java注解，又称为Java标注，JDK5.0引入的一种注释机制。
* 注解是<u>元数据</u>的一种形式，提供**有关于程序**但**不属于程序本身**的数据。

## 注解声明
### 声明一个注解类型
Java中所有的注解，默认实现Annotation接口
> 接口
```
//Java语言中Annotation的定义

package java.lang.annotation;

public interface Annotation {

   boolean equals(Object obj);

   int hashCode();

   String toString();

   Class<? extends Annotation> annotationType();
}
```
与声明一个"Class"不同的是，注解的声明使用 **@interface**关键字
```
public @interface Lance{

}
```
### 元注解
>在定义注解时，**注解类**也能够使用其他注解声明
#### 定义
元注解（meta-annotation），对**注解类型**进行注解的**注解类**
>另外还有@Documentened 与 @Inherited 元注解，前者用于被**javadoc**工具提取成文档，后者表示子类继承父类中定义的注解
#### @Target
注解标记另一个注解，以限制可以应用注解的Java元素类型。
#### @Retention
注解制定标记注解的存储方式

### 注解类型元素
* 在上文元注解中，允许使用注解时传递参数。
* 我们也能让**自定义注解**的主体包含annotation type element(注解类型元素)声明。
  * 使用类似方法，可以定义可选的默认值


## 注解的应用场景
 根据注解的保留级别不同，注解的应用存在不同场景

|级别|技术|说明|
|---|---|---|
|源码|APT|在编译期能够获取**注解与注解声明中的类**（包括类中所有的成员信息），一般用于生成额外的辅助类|
|字节码|字节码增强|在编译出Class后，通过修改Class数据以实现代码逻辑目的。对于是否需要修改的区分或者修改为不同逻辑的判断可以使用注解。
|运行时|反射|在程序运行期间，通过反射技术动态获取注解与其元素，从而完成不同的逻辑判定。

### APT注解处理器

{% asset_img APT注解类图.jpg %}

>Process过程会执行两次
