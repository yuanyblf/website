+++
title = "使用任务调度"
weight = 2
description = "讲述了如何在choerodon平台上自定义定时任务"
+++


## 前置条件

在开始使用定时任务之前，要确保服务的choerodon-starters依赖在 0.6.3.RELEASE 版本及之上。

## 介绍

定时任务基于`quartz`的数据库模式，位于`asgard-service`，消费端依赖于`choerodon-starter-asgard`。在页面上手动创建定时任务，定时任务支持简单定时任务和cron表达式定时任务，并指定消费端的特定方法去消费。如果下一次定时任务被触发，而上一条定时任务未被消费端执行，则该定时任务状态设置为失败。

## 使用

### 消费端添加依赖

```xml
<dependency>
    <groupId>io.choerodon</groupId>
    <artifactId>choerodon-starter-asgard</artifactId>
    <version>${choerodon.starters.version}</version>
</dependency>
```

### 添加消费端方法

- 服务启动后，`asgard-service`通过kafka消息监听服务启动后主动拉取@JobTask定义的方法。
- @JobTask注解的方法参数必须为Map<String, Object>。
- @JobParam为执行参数, 类型需要为String，Integer，Long，Double，Boolean之一，如果没有设置默认值则创建定时任务时必须指定方法参数。
- @JobTask注解的方法返回值为Map<String, Object>或者为void。如果返回值为void则传入的参数为前端传入，不会改变；如果为Map<String, Object>，则下一次的执行参数为上一次执行的返回值，可以动态改变。
    
```java
@Component
public class Task {
    private static final Logger LOGGER = LoggerFactory.getLogger(Task.class);

    @JobTask(code = "test",
            maxRetryCount = 2, params = {
            @JobParam(name = "isInstantly", defaultValue = "true", type = Boolean.class),
            @JobParam(name = "name", defaultValue = "zh"),
            @JobParam(name = "age", type = Integer.class)
    })
    public Map<String, Object> test(Map<String, Object> data) {
        LOGGER.info("data {}", data);
        Object age = data.get("age");
        if (age != null) {
            data.put("age", (Integer)age + 1);
        }
        return data;
    }
}
```

### 消费端的配置

```yaml
choerodon:
  schedule:
    consumer:
      enabled: true # 启用任务调度消费端
      thread-num: 1 # 任务调度消费线程数
      poll-interval-ms: 1000 # 拉取间隔，默认1000毫秒
```

### 创建定时任务
在前端页面的`任务调度` --> `任务明细` --> `创建任务`，填入任务执行参数以及扫描到的服务执行方法后创建任务。
