---
layout: post
title: "learner.video 上线并且开源，欢迎订阅"
subtitle:   ""
date:   2016-02-04
author: "RryLee"
tags:
    - php
    - Eloquent
---

* content
{:toc}

## learner.video

[![License](https://poser.pugx.org/laravel/framework/license.svg)](https://packagist.org/packages/laravel/framework)

learner.video 使用 [laravel](http://laravel.com/) + [vue](http://vuejs.org/)(Vue 主要用在了后台的部分)， 方便的搭建个人 CMS。

## 日志

## 主要功能

* 视频管理 (vimeo(清晰，快，无障碍), youtube(未), youku(未))

* 博客管理

* 发布 newsletter

## 安装

克隆之后　[composer install]，然后 migrate 导入数据库，你就可以使用

账号: boss
密码: 121212

登陆到后台了。

## 一些依赖

* [Zizaco/Entrust](https://github.com/Zizaco/entrust) -- 待移除

* [mercuryseries/flashy](https://github.com/mercuryseries/flashy)

* [laravolt/avatar](https://github.com/laravolt/avatar)

* [erusev/parsedown](https://github.com/erusev/parsedown)

* [spatie/laravel-newsletter](https://github.com/spatie/laravel-newsletter)

## 注意

可能不是都会出现的问题，　表默认的　created_at 都会有个　current timestamp 属性，需要手动移除，不然每次　update 都会自动重置　created 到当前时间。

    ALTER table [表名] modify created_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP;

然后就是　laravel5.2 之后移除　bindShared() 的问题，请手动修改安装滞之后的错误提示。

## 角色

目前有 user, admin, boss 三个角色，并不能通过后台添加更多。

## Newsletter

使用的 [Mailchimp](http://mailchimp.com/) 请手动设置你的 list-id 以及 app_key。

当然欢迎订阅 [learner newsletter](http://learner.video/)

## 贡献

[讨论贴](http://learner.video/blogs/34).

### License

learner.video [MIT license](http://opensource.org/licenses/MIT)

