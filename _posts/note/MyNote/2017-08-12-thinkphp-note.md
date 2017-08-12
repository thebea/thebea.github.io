---
layout: post
title: "thinkphp5学习笔记"
date: 2017-08-12 09:00:00 +0800 
categories: 笔记
tag: MyNote
---
* content
{:toc}

`PHP框架学习`

<!-- more -->

<!-- TOC -->

- [基础](#基础)
- [URL和路由](#URL和路由)
- [请求和响应](#请求和响应)
- [数据库](#数据库)
- [查询语言](#查询语言)
- [模型和关联](#模型和关联)
- [试图和模板](#试图和模板)
- [调试和日志](#调试和日志)
- [API开发](#API开发)
- [命令行工具](#命令行工具)
- [扩展](#扩展)
- [杂项](#杂项)


内容来源：[ThinkPHP5快速入门](https://www.kancloud.cn/thinkphp/thinkphp5_quickstart/147278)


<!-- /TOC -->

## 基础

### 1.目录结构

```
├─application 应用目录（可设置）
│ ├─index 模块目录(可更改)
│ │ ├─config.php 模块配置文件
│ │ ├─common.php 模块公共文件
│ │ ├─controller 控制器目录
│ │ ├─model 模型目录
│ │ └─view 视图目录
│ │
│ ├─command.php 命令行工具配置文件
│ ├─common.php 应用公共文件
│ ├─config.php 应用配置文件
│ ├─tags.php 应用行为扩展定义文件
│ ├─database.php 数据库配置文件
│ └─route.php 路由配置文件
```



