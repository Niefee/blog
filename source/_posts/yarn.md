---
title: yarn
date: 2018-07-22 10:50:16
tags: ES6
categories: 工具 
---

## 安装

Mac用户建议使用`brew`安装。

```js
brew install yarn
```

## 操作命令

功能相同，语法不同：

Npm                       | Yarn                      | 功能描述
--------------------------|---------------------------|--------------------------------
npm install(npm i)        | yarn install(yarn)        | 根据 package.json 安装所有依赖
npm i –save [package]     | yarn add [package]        | 添加依赖包
npm i –save-dev [package] | yarn add [package] –dev   | 添加依赖包至 devDependencies
npm i -g [package]        | yarn global add [package] | 进行全局安装依赖包
npm update –save          | yarn upgrade [package]    | 升级依赖包
npm uninstall [package]   | yarn remove [package]     | 移除依赖包

相同含义：

Npm                              | Yarn                              | 功能描述
---------------------------------|-----------------------------------|---------------------------------------
npm run                          | yarn run                          | 运行 package.json 中预定义的脚本
npm config list                  | yarn config list                  | 查看配置信息
npm config set registry 仓库地址 | yarn config set registry 仓库地址 | 更换仓库地址
npm init                         | yarn init                         | 互动式创建/更新 package.json 文件
npm list                         | yarn list                         | 查看当前目录下已安装的node包
npm login                        | yarn login                        | 保存你的用户名、邮箱
npm logout                       | yarn logout                       | 删除你的用户名、邮箱
npm outdated                     | yarn outdated                     | 检查过时的依赖包
npm link                         | yarn link                         | 开发时链接依赖包，以便在其他项目中使用
npm unlink                       | yarn unlink                       | 取消链接依赖包
npm publish                      | yarn publish                      | 将包发布到 npm
npm test                         | yarn test                         | 测试 = yarn run test
npm bin                          | yarn bin                          | 显示 bin 文件所在的安装目录
yarn info                        | yarn info                         | 显示一个包的信息

## 单独命令

### Npm 

 - npm rebuild

用户更改`node`版本后，重新编译当中的二进制文件。例如`Sass（Scss)`，通过`npm rebuild node-sass`重新编译当中的二进制文件。


### Yarn

 - yarn import：依据原npm安装后的node_modules目录生成一份yarn.lock文件；
 - yarn licenses：列出已安装包的许可证信息；
 - yarn pack：创建一个压缩的包依赖 gzip 档案；
 - yarn why：显示有关一个包为何被安装的信息。
 - yarn autoclean：从包依赖里清除并移除不需要的文件。


> 参考:
>https://jeffjade.com/2017/12/30/135-npm-vs-yarn-detial-memo/
> https://yarnpkg.com/zh-Hans/docs/cli/