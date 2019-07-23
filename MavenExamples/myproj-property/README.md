# Maven property属性

## 1、简介

这是maven属性的测试项目。

在pom.xml文件中我们可以使用${propertyName}的形式引用属性。是值的占位符，类似EL，类似ant的属性，比如${X}，可用于pom文件任何赋值的位置。有以下分类：内置属性、环境变量、project根元素下面的子元素的值、Maven本地配置文件settings.xml或本地Maven安装目录下的settings.xml文件根元素settings下的元素、java的系统属性、自定义属性。

## 2、关键代码及简介

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>

	<groupId>com.oops.myproj</groupId>
	<artifactId>myproj-property</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<packaging>jar</packaging>

	<name>myproj-property</name>
	<url>http://maven.apache.org</url>
	<!-- 除了这里的这三种，还可以用settins.开头的属性引用settings里的元素 -->
	<!-- s所有的java系统属性都可以用maven属性引用 -->
	<!-- 所有的环境变量都可以用env.开头的属性引用 -->
	<properties>
		<springVersion>5.1.5.RELEASE</springVersion>
		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
	</properties>

	<dependencies>
		<dependency>
		    <!-- POM属性可以用project.×××来引用POM文件中对应元素的值 -->
			<groupId>${project.groupId}</groupId>
			<artifactId>projectA</artifactId>
			<!-- 内置属性 -->
			<version>${version}</version>
			<scope>compile</scope>
		</dependency>
		<!-- https://mvnrepository.com/artifact/org.springframework/spring-expression -->
		<dependency>
			<groupId>org.springframework</groupId>
			<artifactId>spring-expression</artifactId>
			<!-- 自定义属性：可以在POM的properties下自定义maven属性 -->
			<version>${springVersion}</version>
		</dependency>
		<dependency>
			<groupId>junit</groupId>
			<artifactId>junit</artifactId>
			<version>3.8.1</version>
			<scope>test</scope>
		</dependency>
	</dependencies>
</project>

```

按代码中出现的顺序，${project.groupId}可以引用POM文件中groupId的值，因为projectA和当前项目是位于同一个groupId的，所以可以导入projectA的包。

内置属性${version}，maven预定义可以直接使用。

自定义属性，可以在POM的properties下自定义maven属性。

最后导入的jar包如下：

![1563841293327](./images/3.png)