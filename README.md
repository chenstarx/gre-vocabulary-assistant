# Vue单词助手

一款用Vue写的高效率在线背单词Web App，经实践两周即可背完GRE机经词。

功能理论依据是艾宾浩斯记忆周期，同时参考了杨鹏的《17天搞定GRE单词》，以及不少同学和自己使用Excel背单词的经验。

本项目尤其适合做为Excel背单词法的替代方案，尤其适合准备GRE这种考试，需要短期记忆大量单词的同学。

>因为是备考GRE时在空余时间写的，项目一些地方的代码复用和算法写的比较糟糕，有很大的提升空间。

[点此进入本项目的demo页面（甚至可以直接在这背GRE单词）](超链接地址 "https://gre.lukerr.com")

如果觉得本项目有帮助记得给个star~

## 项目特点

1. 使用Vue.js做为整体框架
2. 使用HTML5的indexDB做为本地数据库
3. 异步api全部使用Promise封装
4. 前端页面很简单，主要的时间花在了api上
5. 基于多方面考虑做了用户系统，不同用户有独立的学习进度

因为项目使用了indexDB这种浏览器本地数据库来储存数据，
不同机器间学习数据不互通。但又因为在本地就有用户系统，
之后能很方便的把数据接上云端。

之所以使用indexDB是因为学习进度需要被长久保存，
在Web端能满足需求的只有localStorage和indexDB。
但在这种应用使用localStorage太不优雅了，所以你懂的。

## 技术栈

Vue + Vuex + Vue-router + indexDB

## 代码说明

本项目核心是两个封装好的api，位于```/src/api```目录下，剩余的都是在一般的vue项目里很常见的代码，花一点时间就能看懂故不多介绍。

### /src/api/cache.js
- 操作本地数据库indexDB的api，类似于MVC模型中的M和V
- 因为indexDB是异步读写，所以每个api都用到了Promise
- 数据库设计了三个表，每个表的数据结构在代码内有详细介绍。
  - user表，储存用户基本信息，比如用户名和密码。
  - learned表，储存用户对每个单词的熟悉度，记忆周期等数据
  - progress表，储存用户对每个list的学习进度等信息（这个表好像有点鸡肋，但一时半会也想不出更好的能满足需求的方案，相当于为了查询性能做了数据储存的冗余的操作）

### /src/api/word.js
 - 应用层api，类似于MVC模型的C
 - 包含诸如"获取下一批要复习的单词"这样的api
 - 艾宾浩斯记忆周期和《17天搞定GRE单词》中的方法在这里体现

## 本地安装与使用

```
# 下载项目到本地
git clone https://github.com/chenstarx/vue-vocabulary

# 进入项目文件夹
cd vue-vocabulary

# 安装npm依赖
npm install

# 开发模式运行
npm run serve
```
