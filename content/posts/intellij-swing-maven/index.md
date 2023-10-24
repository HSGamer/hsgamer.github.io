---
title: "Use IntelliJ's Swing Designer in Maven"
subtitle: "Just a configuration that enables using IntelliJ's Swing in Maven"
date: 2023-10-24T22:22:56+07:00
authors: ["HSGamer"]
description: "Just a configuration that enables using IntelliJ's Swing in Maven"

tags:
- intellij
- swing
- java
- maven
categories:
- development

comment:
  enable: true
share:
  enable: true
---

Recently, I've been working on several projects related to Java Swing and Maven, so I tried many tools from popular IDEs to create the Forms & Dialogs.

My favorite was IntelliJ's Swing Designer because:
- I mainly use IntelliJ in most of my projects
- The editor is pretty clean and not too bloated for my workspace
- The structure has clear separation between code and design (Only provide components variables when needed)

However, the biggest problem was that there was no clear & official tool or tutorial to integrate the forms into my Maven projects.

Then, I found a blog from [Tobias Manske](https://tobiasmanske.de/) on the configuration. You can check it [here](https://tobiasmanske.de/posts/2021-02-23-maven-ij-designer/).

It worked in my case, but I had to run the forms in IntelliJ to get them compiled before running the Maven actions. It means that I still couldn't use it in a continuous integration (CI) like Github Actions.

So then I dug around the Ant plugin. Finally, it works perfectly now.

Here is my minimal configuration:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>me.hsgamer</groupId>
    <artifactId>example</artifactId>
    <version>1.0-SNAPSHOT</version>

    <properties>
        <intellij.version>232.9921.53</intellij.version>
    </properties>

    <repositories>
        <repository>
            <id>jetbrains.releases</id>
            <url>https://www.jetbrains.com/intellij-repository/releases</url>
        </repository>
        <repository>
            <id>jetbrains.3rdparty</id>
            <url>https://cache-redirector.jetbrains.com/intellij-dependencies</url>
        </repository>
    </repositories>

    <build>
        <plugins>
            <plugin>
                <artifactId>maven-antrun-plugin</artifactId>
                <version>3.0.0</version>
                <executions>
                    <execution>
                        <phase>compile</phase>
                        <goals>
                            <goal>run</goal>
                        </goals>
                        <configuration>
                            <target>
                                <property name="build.compiler" value="extJavac"/>
                                <path id="j2sp">
                                    <pathelement location="${project.basedir}/src/main/java"/>
                                </path>
                                <taskdef name="javac2" classpathref="maven.compile.classpath" classname="com.intellij.ant.Javac2"/>
                                <javac2 destdir="${project.basedir}/target/classes">
                                    <src refid="j2sp"/>
                                    <classpath>
                                        <path refid="maven.plugin.classpath"/>
                                        <path refid="maven.compile.classpath"/>
                                        <path refid="maven.runtime.classpath"/>
                                    </classpath>
                                </javac2>
                            </target>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>

    <dependencies>
        <dependency>
            <groupId>com.jetbrains.intellij.java</groupId>
            <artifactId>java-gui-forms-rt</artifactId>
            <version>${intellij.version}</version>
            <scope>compile</scope>
        </dependency>
        <dependency>
            <groupId>com.jetbrains.intellij.java</groupId>
            <artifactId>java-compiler-ant-tasks</artifactId>
            <version>${intellij.version}</version>
            <scope>provided</scope>
        </dependency>
    </dependencies>
</project>
```
