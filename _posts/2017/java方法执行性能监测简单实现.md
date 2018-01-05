---
layout: post
title: java方法执行性能监测简单实现
comments: false
categories:
  - 随笔
tags:
  - 2017
abbrlink: 50c63fd1
date: 2017-02-15 12:00:36
---

<pre>package about.performance.methodMonitor;

public class MyMonitor {

	//ThreadLocal类可以将非线程安全类转变成线程安全类
	private static ThreadLocal record = new ThreadLocal();
	
	//启动对某方法的监视
	public static void begin(String method){
		System.out.println("begin...");
		MethodPerformace mf = new MethodPerformace(method);
		record.set(mf);
	}
	
	public static void end(){
		System.out.println("end...");
		MethodPerformace mp = record.get();
		mp.printPerformace();
	}
	
}
</pre>

<pre>package about.performance.methodMonitor;

public class MethodPerformace {
	private long begin;
	private long end;
	private String serviceMethod;
	
	public  MethodPerformace(String serviceMethod){
		this.serviceMethod = serviceMethod;
		this.begin = System.currentTimeMillis();
	}
	
	public void printPerformace(){
		end = System.currentTimeMillis();
		long e = end - begin;
		System.out.println(serviceMethod+"执行了"+e+"毫秒.");
	}
	
}
</pre>
测试demo的main方法
<pre>MyMonitor.begin("Tool.outFile");
Tool.outFile("C:\\Users\\long\\Desktop\\hpes\\Desperate Housewives10.txt");
MyMonitor.end();</pre>
执行结果
begin...
File not found
end...
Tool.outFile执行了2毫秒.
//结合aop使用,效果会更好
