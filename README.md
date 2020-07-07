# Project 2 for Design Thinking in DaSE SUMMERMID2020

The code are mainly based on [X-lab website](https://github.com/X-lab2017/xlab-website)

## Member

- Jiayi Mei([Wence May](https://github.com/orgs/cross-species/people/Wence-May))
- Hongjia Zou([Wheelsmuggler](https://github.com/Wheelsmuggler))
- Shuang Wu([Yoyo Wu](https://github.com/orgs/cross-species/people/1054096100))

## Description

全流程在线协作打造现代化CMS系统

- **目标**：利用数字化协作工具，完成一个CMS系统，可以是一个主题网站、内容博客等
- **内容**：给出一个CMS的半成品（[X-lab](https://github.com/X-lab2017/xlab-website)），在此基础上，根据小组的偏好，将其做成一个相对完整的内容系统。
- **技能点**：代码类在线多人协作、敏捷设计思维过程
- **完成节点**：7月20日

## Guide

### Prerequisites

* **Software**: [Git][git-install], and [Hugo][hugo-install]. As an example of working configuration:
```bash
git --version
hugo version
```

* **Hardware**: 2 CPUs, 8GB memory RAM.

### Getting started

Make sure that you have installed `Git` and `Hugo`, **in particular**, you must install Hugo with its [extended_0.65+ version][hugo-version]. And then set

Steps:

1. Clone this project & get into it
```bash
git clone https://github.com/cross-species/pj2.git
cd pj2
```
*Note:*
We assume you are looking for the `master` module so you can make your own submodule.
If not, update all the submodules:
```bash
git submodule update --init --recursive
```

2. Install the theme and run the server:
```bash
# Since we have removed the academic theme for `git commit` but hugo needs theme, we need to reinstall it.
git clone https://github.com/gcushen/hugo-academic.git themes/academic
hugo server
```

3. Git commit: 
Since the **Git cache of theme `academic`** comflict with the **Git of our main part `master`**, we need to remove it for `git commit`.
```bash
rm -rf ./themes/academic
git add .
git commit -m "<your commit name>"
git push
```

The site will be ready after a while in `http://localhost:1313`.

## Support

If you have any questions or feature requests, please feel free to submit an issue.

For developers, the `Git` is **necessary**, but the `Hugo` is **not necessary** if you do not want to view the site locally or generate some pages automatically, follow our [Contributing Guide][CONTRIBUTING_PATH] will undoubtedly lead you making changes to our site!


[git-install]: https://git-scm.com/downloads

[hugo-install]: https://gohugo.io/getting-started/installing/#quick-install

[hugo-version]: https://github.com/gohugoio/hugo/releases

[CONTRIBUTING_PATH]: ./CONTRIBUTING.zh-CN.md
