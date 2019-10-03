# Hello Maven

GitHub Actions Maven Deploy Sample Repository

在 `pom.xml` 中加入配置

```xml
    <build>
        <plugins>
            <plugin>
                <artifactId>maven-deploy-plugin</artifactId>
                <version>2.8.1</version>
                <configuration>
                    <altDeploymentRepository>internal.repo::default::file://${project.build.directory}/mvn-repo</altDeploymentRepository>
                </configuration>
            </plugin>
            <plugin>
                <groupId>com.github.github</groupId>
                <artifactId>site-maven-plugin</artifactId>
                <version >0.12</version>
                <configuration>
                    <message>Maven artifacts for ${project.version}</message>
                    <noJekyll>true</noJekyll>
                    <outputDirectory>${project.build.directory}/mvn-repo</outputDirectory><!--本地jar地址-->
                    <branch>refs/heads/master</branch><!--分支的名称-->
                    <merge>true</merge>
                    <includes>
                        <include>**/*</include>
                    </includes>
                    <repositoryName>MavenRepository</repositoryName><!--对应github上创建的仓库名称 name-->
                    <repositoryOwner>PasteUs</repositoryOwner><!--github 仓库所有者即登录用户名-->
                </configuration>
                <executions>
                    <execution>
                        <goals>
                            <goal>site</goal>
                        </goals>
                        <phase>deploy</phase>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>

    <properties>
        <github.global.server>github</github.global.server>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
        <java.version>11</java.version>
        <maven.compiler.source>11</maven.compiler.source>
        <maven.compiler.target>11</maven.compiler.target>
    </properties>
```

在 `settings.xml` 中加入配置

```xml
    <servers>
        <server>
            <id>github</id>
            <username>GitHub 账号</username>
            <password>GitHub Token</password>
        </server>
    </servers>
```
