---
layout: post
title: 创建java线程
comments: false
categories:
  - 随笔
tags:
  - 2017
abbrlink: bd5aa4ef
date: 2017-04-05 15:46:54
---

Thread thread = new Thread();
thread.start();
---------------
创建线程运行代码两种方式:
1.继承Thread类
public class MyThread extends Thread{
 public void run(){
  System.out.print("run ...");
 }
}
new MyThread().start();
*也可以写匿名类
2.实现Runnable接口
public class MyRunnable implements Runnable{
 public void run(){
  System.out.print("run ...");
 }
}
为了线程执行run方法,需要在Thread类的构造函数传入MyRunnable的实例对象
Thread thread = new Thread(new MyRunnable());
thread.strat();
<strong>子类还是实现Runnable接口?</strong>
更倾向于实现Runnable接口这种方法。因为线程池可以有效的管理实现了Runnable接口的线程，如果线程池满了，新的线程就会排队等候执行，直到线程池空闲出来为止。而如果线程是通过实现Thread子类实现的，这将会复杂一些。
有时我们要同时融合实现Runnable接口和Thread子类两种方式。例如，实现了Thread子类的实例可以执行多个实现了Runnable接口的线程。一个典型的应用就是线程池。
<strong>注意执行线程调用start()方法,而不是run().</strong>
run()方法的确如你所愿的被调用了。但是，事实上,run()方法并非是由刚创建的新线程所执行的，而是被创建新线程的当前线程所执行了。也就是被执行上面两行代码的线程所执行的。想要让创建的新线程执行run()方法，必须调用新线程的start方法。
MyRunnable runnable = new MyRunnable();
Thread thread = new Thread(runnable, "New Thread"); //指定线程名
thread.start();
System.out.println(thread.getName()); //获取Thread子类线程名
String threadName = Thread.currentThread().getName(); //获取Runnable接口的线程名字
<strong>启动线程是有序的,但执行的顺序是无序的.</strong>
