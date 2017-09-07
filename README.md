# oss-lib-adminclient

A enhanced client for oss-admin ([spring-boot-admin](https://github.com/codecentric/spring-boot-admin))

- Encrypt `security.user.name` and `security.user.password` and expose them to oss-admin.
- Custom `/info` endpoint, add encrypted `security.user.name` and `security.user.password` into it.

## How to use

In pom.xml

```xml
<dependency>
    <groupId>cn.home1</groupId>
    <artifactId>oss-lib-adminclient-spring-boot-${spring-boot.version}</artifactId>
</dependency>
```

## Config of spring-boot-admin-starter-client

### Eureka properties

 * `eureka.client.serviceUrl.defaultZone` Normally use default value.
 * `eureka.client.instance.hostname` `statusPageUrlPath` and `healthCheckUrlPath` depends on this value.
 * `eureka.client.instance.instance-id`
 * `eureka.client.instance.prefer-ip-address` Normally set to false
 * `eureka.client.instance.statusPageUrlPath` Important
 * `eureka.client.instance.healthCheckUrlPath` Important
 * `eureka.client.instance.metadata-map.management.context-path` Add `management.context-path` into eureka's metadata.
 * `eureka.client.instance.metadata-map.management.port` Add `management.port` into eureka's metadata.

> `server.port` `server.context-path` and `management.port` `management.context-path`.
> Feign client will use `server.context-path` to build request URL.

If `server.port` is not same as `management.port`, `statusPageUrlPath` and `healthCheckUrlPath` needs special config,
we recommend that use the same port.

### Logging properties

  * `logging.file` Log file name. For instance `application.log`
  * `logging.path` Location of the log file. For instance `/var/log`

Example:

    logging:
      file: ${LOGGING_FILE:oss-admin}.log
      path: ${LOGGING_PATH:${user.home}/.oss/oss-admin/logs}

### Management security
Basic authentication for actuator endpoints

 * `security.user.role` Default role of user (USER/ADMIN).

Example:

    security.user:
         name: admin
         password: ${SECURITY_USER_PASSWORD:admin_pass}
         role: ADMIN

  > NOTES: Do dot make a conflict with `oss-lib-security`'s user that has `ADMIN` role.

### Actuator endpoint
Alter actuator endpoints, for example `/beans` to `/springbeans`

    endpoints.beans.id=springbeans
    endpoints.beans.sensitive=true
    endpoints.beans.enabled=true
