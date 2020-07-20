---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "E-Slides 开发文档"
subtitle: "根据小组讨论与会议纪要作出"
summary: "开发者心路历程"
authors: ["meijiayi"]
tags: ["document"]
categories: ["document"]
date: 2020-07-21T20:46:57+08:00
lastmod: 2020-07-21T20:46:57+08:00
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---


# 课件自动生成

- 用户调研

  - 用户定位：教师

  - 应用场景：备课、生成课件pdf

    - 教学逻辑较强，由逻辑——>内容——>展示

    - 配合教案使用

    - 页面间跳转 超链接

    - 需要储存云端

  - 痛点：

    - 排版操作重复

    - 调整知识内容不方便(新学期update）

  - 用户访谈

    - 辅助工具：

      - 思维导图vs 概念图

      - 备课过程中不会具象化，或停留在纸上

    - 中学vs大学

      - 中：课程完整、系统，使用指定的标准化教材

      - 教案仅存在于中学

      - 大学老师：知识的创造者，自己编写教材，非标准化
        ppt -> 文档 ->教材​

      - 大学成熟的课：与中学流程一样

    - 备课流程：
      - 参考 - >大纲 -> 迭代

    - 现有解决方案

      - ppt：动画特效

      - latex：适合负责的

      - markdown：缺少复杂的视觉

      - jupyter notebook：代码

    - 做一门新课的周期：2~3月，有可能一边备课一边授课

  - 问卷：

    - 教师身份、类型定位
      Q : 是中学还是大学老师？
      Q：是什么学科？ 数理/工程/​文科/艺术...

    - 现行解决方案
      Q：习惯用什么方式制作课件？ppt/Latex/Markdown/jupyter notebook/其他(？)
      Q：在该工具下是否存在版本适配性/卡顿的问题？严重吗？
      ​​Q：你觉得该工具的便利性

    - 使用习惯
      Q：（if ppt）常使用ppt模板吗？
      Q：​课件中是否使用动画效果？使用的频率？
      Q：课件是否配合文稿使用/使用ppt“备注”功能？​​
      Q：花在排版上的时间？​
      Q：常使用公式吗​？
      Q：​一个课件的页数区间？
      Q：一门课的备课周期？​
      Q：课程迭代，对知识结构调整幅度大吗？​

    - 意愿调查

      Q：在备课时如果有思维导图帮助梳理大纲，觉得帮助大吗？
      Q：是否愿意采取线上编辑的形式？

      - 如果有...的功能，对你的帮助大吗？

  - 调研结果：

    - 现行解决办法![img](https://api2.mubu.com/v3/document_image/2444e7f9-bc69-4262-a1e5-a5be9c7ea327-2361089.jpg)

    - 排版耗时![img](https://api2.mubu.com/v3/document_image/eb00693d-72a8-4df2-9876-fcd1686a6e75-2361089.jpg)

      课件的内容是核心，而排版多为锦上添花的作用。然而在制作课件时，若在排版上耗费过多时间，则会造成很多不必要的精力消耗。由统计结果看，还是有多数人在排版上所耗费的时间达到了一半甚至更多，因此我们希望能实现课件自动排版的功能。

    - 卡顿问题![img](https://api2.mubu.com/v3/document_image/91ab4740-d9d7-43bc-b5f0-108ec52d7a8f-2361089.jpg)

      版本适配性与卡顿问题通常容易影响用户的使用感受。而当前市面上制作课件的产品大都已经比较成熟，并没有在这两方面出现非常大的纰漏，但是仍会偶尔出现类似的瑕疵。理想情况下，我们希望能尽量避免这类情况，以给用户更好的体验感受。

    - 动画效果![img](https://api2.mubu.com/v3/document_image/699ab06c-475f-4aa5-a07d-26580517918f-2361089.jpg)

      用户在课件演示时对动画的需求仍较大，动画能协助用户演讲时更生动具象、易于理解，因此是个比较重要的组成部分。

    - 使用模板![img](https://api2.mubu.com/v3/document_image/407af8e6-2e8b-4b1c-9f6b-b52ee016f125-2361089.jpg)

    - 是否配合文稿![img](https://api2.mubu.com/v3/document_image/cfbc940d-890a-4e08-b5c0-be77c7d2e4a1-2361089.jpg)

    - 是否愿意在线编辑![img](https://api2.mubu.com/v3/document_image/5ebd5a19-b976-4b3e-baa0-130bf0b27418-2361089.jpg)
      ​从统计结果来看，多数人愿意在线编辑课件。因此，在一定程度上证实了该产品的推出将会获得一定的市场需求。

    - 制作课件的页数![img](https://api2.mubu.com/v3/document_image/1869b500-4080-437b-ae1e-ba508271eedb-2361089.jpg)

    - 制作课件周期![img](https://api2.mubu.com/v3/document_image/22294a94-86f1-4dc9-8345-095841d4b29c-2361089.jpg)

    - 迭代时对知识结构的调整幅度![img](https://api2.mubu.com/v3/document_image/9b0f74a5-8758-4022-b3a2-f859c25d9177-2361089.jpg)

    - 思维导图的帮助![img](https://api2.mubu.com/v3/document_image/68fa362e-c6fb-41bf-8ef6-fc9a26e6ee14-2361089.jpg)

- 定义问题

  - 功能需求(Question)：

    根据用户调研结果的指向性

    - \1. 在线输入编辑/上传md文件

    - \2. 自动排版

    - \3. 在线编译预览

    - \4. 课件下载

    - \5. 需要长期稳定的备份存储

    - \6. 兼容公式、代码

    - \7. 提供jupyter运行服务

    - \6. 思维导图辅助梳理大纲

  - 核心功能：

    - markdown转pdf（静态）

    - 线上编辑

    - 线上演示

    - pdf下载

  - 迭代功能

    - md语法定义的超集

    - 学生版pdf/教师版pdf区分

    - 生成后支持编辑

      渲染优先级

      - 文本位置

      - 文本修改

      - 图片位置

      - 图片缩放

    - 动画演示

      - 每一点分页

      - 新生成一个页面
        canvas

    - jupyter代码演示页面
      jupyter lab 服务器，用户上传文件直接运行，无需本地环境

    - 交互式调整知识结构

- 技术调研

  - 语言&框架：python+flask

  - 前端网页模板：贴近原型设计图

  - 在线编辑：网页嵌入markdown
    找样例

  - pdf预览：网页嵌入显示pdf

  - latex模板：贴近课件形式
    是否能设定背景图片？
    是否能设定背景颜色？
    标题页和内容页样式不同
    插入图片的放置方式？​​​scale？

  - 数据库：Docker+？

- How to do it -

  - 宏观流程

    - 1 输入：markdown

    - 2 解析 -> text img数据

    - 3 模板：latex课件模板

    - 4 输出：.tex、.pdf文件

  - 代码实现 v1

    按照函数/任务的颗粒度拆分；
    其中有些功能在version1中非必。​

    - 前端：选好网页模板

    - 前端：在线文本输入

    - 前端：发送请求

      用jQuery之类的方式

      - \1. 用户指定课件模板

      - \2. 用户输入引导(是否有提示，待定)

      - \4. 完整文本打包发送

      - \5. 文件上传

      - \6. pdf文件下载

    - 服务端：完整文本—(解析)—>内容

      - \1. 接收文本/从md读取文本

      - \2. 定义一些正则匹配的函数

      - \3. 内容存储入数据结构(object)
        怎么设计数据结构？object的设计很重要！​
        图片如何处理？​

      - \4. 内容备份入数据库
        存入什么样的数据库？文档型还是关系型?
        ​如果是关系型schema怎么设计？
        ​存的是文本完整内容还是解析提取过的内容？
        ​如果用户存档后下次接着编辑，从什么数据恢复到上次的编辑页？
        接着编辑修改后的内容怎么向存档添加/复写？​

    - 后台：

      - \1. 内容—(生成)—>.tex文件

      - \2. 调用latex编译器，生成pdf文件

      - \3. pdf文件路径存入数据库/返回pdf文件路径

    - 服务端：pdf接收

      - 用户下载

      - 发送给前端

    - 前端：pdf预览

- 项目一

  - 创建的人物角色

    梅佳奕

    - 大学老师

    - 中学老师

    - 学生

    - 文/理科...

  - 对问题的定义

    雷雅婧

    - 现状

    - 痛点

    - 需求

    - 创新点

  - 挖掘出来的点子（What）

    魏如蓝

    - 自动排版

    - 所有想到的功能

  - 用户调研总结

    王艺鸣

    - 访谈总结

    - 问卷总结

      - 中学 vs 大学 特点、区别

      - ......

  - 原型方案（How）

    吴双 processon+xiaopiu的使用作图
    邹弘嘉 文字​

    - 平台

    - 功能定义

    - 技术调研

- 项目二