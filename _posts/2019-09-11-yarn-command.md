---
layout: post
title:  "yarn的安装与使用"
date:   2019-09-11
categories: ""
tag:
- yarn 
--- 


> yarn的安装

* `npm install -g yarn`（使用Node) 
* `npm install yarn@latest -g`（升级到最新版本）

* `/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"` (homebrew的安装)
* `brew install yarn` (使用homebrew安装yarn)


> 1.查询当前配置的镜像

* `yarn config get registry`


>设置成淘宝镜像

* `yarn config set registry http://registry.npm.taobao.org/`

> yarn和npm的使用

#### 1、初始化包
* `npm init`
* `yarn init`
#### 2、安装包
* `npm install xxx --save`
* `yarn add xxx`
#### 3、移除包
* `npm uninstall xxx`
* `yarn remove xxx`
#### 4、更新包
* `npm update xxx`
* `yarn upgrade xxx`
#### 5、安装开发依赖的包
* `npm install xxx --save-dev`
* `yarn add xxx --dev`
#### 6、全局安装
* `npm install -g xxx`
* `yarn global add xxx`
#### 7、设置下载镜像的地址
* `npm config set registry url`
* `yarn config set registry url`
#### 8、安装所有依赖
* `npm install`
* `yarn install`
#### 9、执行包
* `npm run`
* `yarn run`

> yarn装依赖时报错

```
error  Incorrect integrity when fetching from the cache
info Visit https://yarnpkg.com/en/docs/cli/add for documentation about this command. 
```
使用 `yarn cache clean` 解决（清除缓存）