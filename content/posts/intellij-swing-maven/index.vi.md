---
title: "Dùng Swing Designer của IntelliJ trong Maven"
subtitle: "Chỉ là một vài tùy chỉnh để cho phép dùng Swing của IntelliJ trong Maven"
date: 2023-10-24T22:22:56+07:00
authors: ["HSGamer"]
description: "Chỉ là một vài tùy chỉnh để cho phép dùng Swing của IntelliJ trong Maven"

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

Dạo gần đây, tôi bắt đầu làm một vài dự án liên quan đến Java Swing và Maven, nên tôi đã thử nhiều công cụ từ các IDE nổi tiếng để thử tạo Form và Dialog.

Cái yêu thích nhất của tôi là Swing Designer của IntelliJ, vì:
- Tôi thường sử dụng IntelliJ cho hầu hết dự án
- Trình chỉnh sửa khá gọn và không chứa quá nhiều những thứ không cần thiết cho môi trường làm việc của tôi
- Cấu trúc có sự phân chia rõ ràng giữa code và thiết kế (chỉ cung cấp các thành phần của Swing như là các biến trong code khi cần thiết)

Tuy nhiên, vấn đề lớn nhất là hiện không có một hướng dẫn hay công cụ chính thức nào để liên kết các form được tạo từ IntelliJ vào dự án Maven của tôi.

Sau đó thì tôi tìm thấy một bài blog của [Tobias Manske](https://tobiasmanske.de/) về phần cấu hình. Bạn có thể xem ở [đây](https://tobiasmanske.de/posts/2021-02-23-maven-ij-designer/).

Nó hoạt động trong trường hợp của tôi, nhưng tôi phải chạy Form trong IntelliJ trước khi dùng thao tác của Maven. Nó có nghĩa là tôi vẫn không thể dùng nó trong một môi trường CI như Github Actions.

Vì thế nên tôi cũng vọc vạch plugin Ant trong Maven. Cuối cùng thì nó cũng đã hoạt động hoàn hảo.

Đây là phần cấu hình tối giản của tôi:

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
