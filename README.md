# oss-lib-adminclient

A enhanced client for oss-admin ([spring-boot-admin](https://github.com/codecentric/spring-boot-admin))

- Encrypt `security.user.name` and `security.user.password` and expose them to oss-admin.
- Custom `/info` endpoint, add encrypted `security.user.name` and `security.user.password` into it.
  
### How to use

In pom.xml

```xml
    <dependency>
        <groupId>cn.home1</groupId>
        <artifactId>oss-lib-adminclient-spring-boot-${spring-boot.version}</artifactId>
    </dependency>
```