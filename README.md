# Project 2 for Design Thinking in DaSE SUMMERMID2020

The code are mainly based on [X-lab website](https://github.com/X-lab2017/xlab-website)

## Member

- 梅佳奕([Wence May](https://github.com/orgs/cross-species/people/Wence-May))
- 邹弘嘉([Wheelsmuggler](https://github.com/Wheelsmuggler))
- 吴双([Yoyo Wu](https://github.com/orgs/cross-species/people/1054096100))
- 雷雅婧([Rheaaaaayy](https://github.com/orgs/cross-species/people/Rheaaaaayy))
- 魏如蓝([RulanWei](https://github.com/orgs/cross-species/people/RulanWei))
- 王艺鸣([yiqingmo](https://github.com/orgs/cross-species/people/yiqingmo))

(*Note: 吴双的英语，不行；邹弘嘉的英语，行！我们邹哥哥的代码能力真的——太——好——了——*)

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
git clone https://github.com/cross-species/xlab-website.git
cd xlab-website
```
*Note:*

网站部署上，我已经将网站部署好了，部署的网页基于“master”这一分支。所以我们组员在修改的时候希望都基于当前的master分支创建自己的分支，只在最后提交的时候 pull request 到 “master” 的分支。

Make your own submodule, modify it, and merge it into `master`:

```bash
git checkout -b members/<yourname>_branch
# ...
```

You should update all the submodules:

```bash
git submodule update --init --recursive
```

2. Install the theme and run the server:
```bash
# We have removed the academic theme for `git commit` but `hugo` needs theme. So we need to reinstall it.
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

### 修改内容，并提交

对相应文件做出修改，修改完成后，提交：

```shell
git add .
git commit -sm "feat: add personal info (#264)"
```

修改时，请参考 [Code Rules][rules].

> (可选) 修改完成后，可使用以下命令预览效果 (http://localhost:1313/)：
>
> ```bash
> hugo server
> ```

提交时，尽量：

(1) 用一句话清楚的描述这次提交做了什么。
(2) 关联相关 `issue`，如 `fix #1` 、`close #2`、`#3`（畅所欲言）

#### 同步上游仓库变更
同步上游仓库变更，因为可能有其他人先于你提交到上游仓库，防止冲突：

```bash
git remote add upstream git@github.com:cross-species/xlab-website.git
git fetch upstream
```

若上游仓库变更，需要先进行 `rebase`:

```bash
git rebase upstream/master
```

如果发生冲突，你需要手动修改冲突文件，然后:

```shell
git add my-fix-file
git rebase --continue
```

####  推送新分支到自己的远程仓库

```shell
git push -f origin my-fix-branch:my-fix-branch
```

#### 提 `Pull Request`


在自己仓库的页面上提 `Pull Request` 到上游仓库 `X-lab2017/xlab-website`。

在提交 `Pull Request` 之前，请确保已经签署 [Contributor License Agreement (CLA)](#cla)。

我们准备了一个 [Pull Request 模板][pr-template] ，你可以在 `Pull Request` 中详细地描述你所作的修改。


其他人将会对你的 `Pull Request` 进行`review`， `review` 之后，如果需要再进行更改，就修改相关内容，然后执行以下操作，该 PR 将会自动同步该 `commit` 。
```shell
git add .
git commit --amend
git push -f origin branch-name
```



**如果你的代码合并时出现冲突时，你可以：**

- 删除远程分支:
 ```shell
 git push origin --delete branch-name
 ```

- 切回到 `master` 分支:

 ```shell
 git checkout master -f
 ```
- 删除本地分支(可选):
 ```shell
 git branch -D my-fix-branch
 ```
- 保持本地 `master` 分支与上游分支同步:

 ```shell
 git pull --ff upstream master
 ```

完整配置可详见配置文件 [hypertrons.json](./.github/hypertrons.json)。



在提交 `Pull Request` 之前，请确保已经签署 [Contributor License Agreement (CLA)](#cla)。

我们准备了一个 [Pull Request 模板][pr-template] ，你可以在 `Pull Request` 中详细地描述你所作的修改。



其他人将会对你的 `Pull Request` 进行`review`， `review` 之后，如果需要再进行更改，就修改自己分支的相关内容，然后执行以下操作，该 PR 将会自动同步该 `commit` 。



\```shell

git add .

git commit --amend

git push -f origin branch-name

\```



#### 创建网页

在 “academic” 中，网页的创建需要明确 Front matter（类似于\_\_init\_\_函数中初始化超参，一般被包含在两个“---”之间）。

例如：

```markdown
---
# Display name
title: xx # 中文名

# Username (this should match the folder name)
authors:
- xx # 用户名

# Is this the primary user of the site?
superuser: false

# Role/position
role: 2020硕

# Organizations/Affiliations
organizations:
- name: East China Normal University
  url: "http://www.ecnu.edu.cn/"

# Short bio (displayed in user profile at end of posts)
bio: Life is so beautiful!

interests:
- Movie
- music

education:
  courses:
  - course: MEng in Computer Science
    institution: East China Normal University
    year: 2023
  - course: MEng in Digital Media Technology
    institution: Chengdu University of Information Technology
    year: 2020

# Social/Academic Networking
# For available icons, see: https://sourcethemes.com/academic/docs/page-builder/#icons
#   For an email link, use "fas" icon pack, "envelope" icon, and a link in the
#   form "mailto:your-email@example.com" or "#contact" for contact widget.
social:
- icon: envelope
  icon_pack: fas
  link: "mailto:1723687793@qq.com"  # For a direct email link, use "mailto:test@example.org".
- icon: github
  icon_pack: fab
  link: https://github.com/kanesang1
# Link to a PDF of your resume/CV from the About widget.
# To enable, copy your resume/CV to `static/files/cv.pdf` and uncomment the lines below.
# - icon: cv
#   icon_pack: ai
#   link: files/cv.pdf

# Enter email to display Gravatar (if Gravatar enabled in Config)
email: "1723687793@qq.com"

# Organizational groups that you belong to (for People widget)
#   Set this to `[]` or comment out if you are not using People widget.
user_groups:
- Master
---
```

以上这些，都是 front matter的范畴。

**网页的具体内容的编写可以参考[这里的官方文档][https://sourcethemes.com/academic/zh/docs/managing-content/]。**

## Support

If you have any questions or feature requests, please feel free to submit an issue.

For developers, the `Git` is **necessary**, but the `Hugo` is **not necessary** if you do not want to view the site locally or generate some pages automatically, follow our [Contributing Guide][CONTRIBUTING_PATH] will undoubtedly lead you making changes to our site!


[git-install]: https://git-scm.com/downloads

[hugo-install]: https://gohugo.io/getting-started/installing/#quick-install

[hugo-version]: https://github.com/gohugoio/hugo/releases

[CONTRIBUTING_PATH]: ./CONTRIBUTING.zh-CN.md
