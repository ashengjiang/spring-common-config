## Base-config



## common-util

### pom

```xml

<dependency>
    <groupId>com.github.yaoguoh</groupId>
    <artifactId>common-util</artifactId>
</dependency>
```

- **`Result`** 返回对象
- **`ResultGenerator`** 返回对象构造器

### example

```java
/**
 * 消息管理 REST API
 */
@Api(tags = "消息管理 REST API")
@Slf4j
@AllArgsConstructor
@RestController
@RequestMapping(value = "/message")
public class MessageController {

    private final MessageService messageService;

    /**
     * 根据消息ID查询消息信息
     *
     * @param messageId the message id
     * @return the result
     */
    @ApiOperation(value = "根据消息ID查询消息信息")
    @GetMapping(value = "/{messageId}")
    public Result<MessageVo> findByMessageId(@ApiParam(name = "messageId", value = "消息ID") @PathVariable Long messageId) {
        log.info("findByMessageId - 根据消息ID查询消息信息. messageId={}", messageId);

        try {
            return ResultGenerator.ok(MessageVo.create(messageService.findById(messageId)));
        } catch (Exception e) {
            log.error(e.getMessage(), e);
            return ResultGenerator.wrap(e);
        }
    }
}
```

## common-elasticsearch

### pom

```xml

<dependency>
    <groupId>com.github.yaoguoh</groupId>
    <artifactId>common-elasticsearch</artifactId>
</dependency>
```

- **`ElasticsearchProperties`**  `RestHighLevelClient` 客户端连接信息
- **`RestHighLevelClientConfiguration`** 注册 `restHighLevelClient` `Bean`处理`elasticsearch server`访问协议为`https`

### Spring Boot Application  `@Configuration`配置类 引入 `RestHighLevelClientConfiguration.class`

```java
/**
 * 应用配置置类
 */
@Configuration
@Import(RestHighLevelClientConfiguration.class)
public class ProviderConfiguration {

}
```

### 在`yaml`中添加配置信息

```yaml
elasticsearch:
  xpack-username: 'elastic'
  xpack-password: password'
  keystore: example.elasticsearch.com.jks
  keystore-password: password
  host: example.elasticsearch.com
  port: 443
  scheme: https
```

## common-jpa

### pom

```xml

<dependency>
    <groupId>com.github.yaoguoh</groupId>
    <artifactId>common-jpa</artifactId>
</dependency>
```

- **IService** 通用接口
- **BaseService** 通用接口实现

### example

```java
/**
 * User repository
 */
public interface UserRepository extends JpaRepository<User, Long>, JpaSpecificationExecutor<User> {

}
```

```java
/**
 * The interface User service.
 */
public interface UserService extends IService<User, Long> {

}
```

```java
/**
 * User service impl.
 */
@Slf4j
@Service
public class UserServiceImpl extends BaseService<User, Long> implements UserService {

}
```

## common-redis

### pom

```xml

<dependency>
    <groupId>com.github.yaoguoh</groupId>
    <artifactId>common-redis</artifactId>
</dependency>
```

## common-exception

### pom

```xml

<dependency>
    <groupId>com.github.yaoguoh</groupId>
    <artifactId>common-exception</artifactId>
</dependency>
```

