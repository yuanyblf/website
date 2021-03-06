﻿+++
title = "应用管理"
description = "一个系统可以被解耦成很多应用，每一个应用都是一个独立的服务，实现某一类具体的功能都可以独立部署，应用仅关注于完成一部分任务，每部分任务代表一个小的业务模块，因此各应用之间关系是松耦合的。另外，每创建一个应用，平台会自动在gitlab创建对应的代码库，应用也可以通过应用市场导入产生。"
weight = 2
+++

# 应用管理
 
应用是满足用户某些需求的程序代码的集合，一个系统可以被解耦成很多应用，每一个应用都可以独立部署，每一个应用仅关注于完成一部分任务，每部分任务代表一个小的业务模块，因此各应用之间关系是松耦合的。

另外，每创建一个应用，平台会自动在 Gitlab 创建好对应的代码库。

只有该项目的`项目所有者`才有应用操作权限，`项目成员`仅能查看应用。
  
  - **菜单层次**：项目层
  - **菜单路径**：应用管理 > 应用
  - **默认角色**：项目所有者、项目成员

<blockquote class="note">
  项目成员对应用管理只有查看应用列表的权限，无编辑和启停用应用的权限，对应操作按钮不可见。
</blockquote>

## 创建应用

输入`应用编码`及`应用名称`，创建一个新的应用。步骤如下：您也可以选择一个应用模板，快速创建应用，平台会在Gitlab上为您自动创建对应的代码库以便管理该应用代码。
 
 1. 点击 `创建应用` 按钮；

 2. 输入`应用编码`、`应用名称`进行数据校验，以及选择`应用模板`。
 ![](/docs/user-guide/application-management/image/Create Application.png "Create Application") 
    - 应用编码：该字段是必输的，编码只能由小写字母、数字、"-"组成，且以小写字母开头，不能以"-"结尾并且是唯一的。
    - 应用名称：唯一，不能和其他应用相同。
    - 应用模板：系统预定义模板或组织自定义的模板快。

        系统预定义模板：微服务-MicroService；web前端-MicroServiceUI；Java库-JavaLib。
 3. 点击 `创建` 按钮；
    
 4. 创建成功后，可在 Gitlab 中查看已创建的代码库。

<blockquote class="note">
  若不选择预定义模板，则会创建空仓库，基础代码、默认分支、gitlab-ci.yml等内容都需要自行创建并配置。
</blockquote>

## 查看应用详情

  1. 点击`应用`菜单，在应用管理界面，可查看应用名称、编码、对应Gitlab仓库地址、应用状态等信息，有些项目可能没有仓库地址，则说明该应用是导入的应用，目前应用默认是排序是项目下的启用项目->停用项目->导入应用的排序方式。
![](/docs/user-guide/application-management/image/Create Application .png "Create Application ") 

 - 应用名称：应用的自定义名称；
 - 应用编码：应用的自定义编码，Gitlab 仓库的地址将会取应用编码作为仓库地址中的一段路径，且编码是项目下唯一且不可修改的；
 - 仓库地址：应用 Gitlab 仓库地址；
 - 应用状态：应用运行有三种状态，分别为启用、停用、创建中。

<blockquote class="note">
  若应用状态一直都是创建中，请先检查是否正确配置了项目所有者角色及其角色标签，并且分配给该操作用户。另外，若您本地搭建的 Gitlab 不稳定的话也可能导致消息发送至 Gitlab 处理失败。
</blockquote>

## 修改应用信息

点击`修改应用`→ ![修改应用按钮](/docs/user-guide/development-pipeline/image/update_app_button.png) 对应用信息进行修改。

## 停用/启用应用

 点击 `停用`→ ![停用按钮](/docs/user-guide/development-pipeline/image/stop_button.png) 即可停用应用。若应用已停用，不可以修改应用名称，且不可以部署该应用。
 
<blockquote class="note">
  若该应用已被部署在某环境上生成实例则不可以停用。 
</blockquote>

 点击 `启用`→ ![启用按钮](/docs/user-guide/development-pipeline/image/start_button.png) 即可重新启用被停用的应用，恢复相关操作。

## 查看代码质量

 点击 `代码质量`→ ![代码质量按钮](/docs/user-guide/development-pipeline/image/app_quality.png)，若平台部署了[sonarqube](https://www.sonarqube.org/)服务，并且CI集成sonarqube检查即可看见该应用的代码质量信息

## 更多操作
- [什么是应用模板](../application-template)
- [应用版本](../application-version)
- [应用发布](../application-release)