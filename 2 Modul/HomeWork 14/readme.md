Знакомство с SonarQube
===
Подготовка к выполнению 
===
![изображение](https://user-images.githubusercontent.com/60341565/168794472-5c11d0b5-cc60-4498-915d-243dab0c218d.png)

Основная часть
===
![изображение](https://user-images.githubusercontent.com/60341565/168844457-2a6ae4b3-5261-41ed-a83d-67b9543aea3e.png)
![изображение](https://user-images.githubusercontent.com/60341565/168844673-ce250ebd-1c39-4651-a53c-d63828b00fc0.png)
![изображение](https://user-images.githubusercontent.com/60341565/168854643-162b0438-6573-45de-842f-ad78d735d155.png)
![изображение](https://user-images.githubusercontent.com/60341565/168854743-e70f3407-b61c-447d-9cd8-b840be8e73e7.png)

Nexus 
===
![изображение](https://user-images.githubusercontent.com/60341565/169710733-762259f7-4997-45f7-959c-5c3d5924c390.png)
![изображение](https://user-images.githubusercontent.com/60341565/169710779-a503d7d2-5053-4990-9d6d-bd95e351f523.png)

Maven
===
![изображение](https://user-images.githubusercontent.com/60341565/170504318-9d51d2c7-d89c-468b-81e6-b52db07e8d2f.png)

Pom.xml

          <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
        <modelVersion>4.0.0</modelVersion>
      .
        <groupId>com.netology.app</groupId>
        <artifactId>simple-app</artifactId>
        <version>1.0-SNAPSHOT</version>
         <repositories>
          <repository>
            <id>my-repo</id>
            <name>maven-public</name>
            <url>http://localhost:8081/repository/maven-public/</url>
          </repository>
        </repositories>
        <dependencies>
           <dependency>
            <groupId>netology</groupId>
            <artifactId>java</artifactId>
            <version>8_282</version>
            <classifier>distrib</classifier>
            <type>tar.gz</type>
          </dependency>
        </dependencies>
      </project>
