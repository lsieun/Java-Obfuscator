# ProGuard Quick Start

<!-- TOC -->

- [1. How ProGuard helps to my project?](#1-how-proguard-helps-to-my-project)
- [2. Where can I download Proguard](#2-where-can-i-download-proguard)
- [3. How ProGuard perform Obfuscation?](#3-how-proguard-perform-obfuscation)
- [4. Example](#4-example)
  - [4.1. config proguard](#41-config-proguard)
  - [4.2. execute proguard](#42-execute-proguard)

<!-- /TOC -->

ProGuard is a Java class file shrinker and code obfuscator.

## 1. How ProGuard helps to my project?

- (1) It detect and remove unused classes, method and attributes.
- (2) List the dead code, so you can remove it from the source code.
- (3) Rename the classes, fields, methods with meaning less names, so it is difficult to reverse engineer.

## 2. Where can I download Proguard

You can download ProGuard from following location.

```txt
https://sourceforge.net/projects/proguard/
```

## 3. How ProGuard perform Obfuscation?

The process is divided into 4 steps.

- (1) **Shrink**: Detects and removes unused classes, fields, methods, and attributes.
- (2) **Optimize**: Analyzes and optimizes the bytecode of the methods.
- (3) **Obfuscate**: Renames the remaining classes, fields, and methods using short meaningless names.
- (4) **Preverify**: Adds preverification information to Java classes, it is required for Java Micro Edition and for Java 6 and higher.

## 4. Example

### 4.1. config proguard

filename: `myconfig.pro`

```txt
-injars       agent.jar
-outjars      out.jar
-libraryjars  /usr/local/jdk1.8.0_181/jre/lib/rt.jar:./lib/javassist-3.24.0-GA.jar
-printmapping myapplication.map

-keep public class lsieun.javaagent.gui.GUIMain{ 
      public static void main(java.lang.String[]); 
}
```

注意：下面的配置文件更简洁，使用`<java.home>`代替`/usr/local/jdk1.8.0_181/jre`

```txt
-injars       agent.jar
-outjars      out.jar
-libraryjars  <java.home>/lib/rt.jar:./lib/javassist-3.24.0-GA.jar
-overloadaggressively
-repackageclasses In.God.We.Trust
-printmapping myapplication.map

-keep public class lsieun.javaagent.gui.GUIMain{
    public static void main(java.lang.String[]);
}
```

### 4.2. execute proguard

You can find the ProGuard jar(`proguard.jar`) in the `lib` directory of the ProGuard distribution.

```bash
java -jar proguard.jar @myconfig.pro -verbose
```
