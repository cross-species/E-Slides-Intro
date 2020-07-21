---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Zouhj_notedemo"
subtitle: ""
summary: ""
authors: [zouhongjia]
tags: [notes]
categories: []
date: 2020-07-21T21:58:19+08:00
lastmod: 2020-07-21T21:58:19+08:00
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

Demo    V1

在线编辑模式

客户端给出的接口和功能: 

1. 模版选定
3. 用户按照模版指示一行行输入文本或图片数据
4. 文本打包发送给服务器端
5. 需要一个实时解析latex 模版的解析器. 并有一个展示解析成果的界面.



服务端提供的功能:

	1. 需要有一个模版库, 供用户在搜索时选择,搜索结束之后返回相应的latex文件给客户端(也许也可以放在前端完成)
 	2. 接收用户发送过来的tex文件或者txt文件, (如果是txt文件则需要再转化成tex格式),生成pdf并返回



软件端所需要的功能:

1. 对文本文件转化为tex文件进行解析.
2. txt文件转 tex文件(可能需要)