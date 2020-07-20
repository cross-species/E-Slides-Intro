---
# Display name
title: E-slides

# Username (this should match the folder name)
authors:
- e-slides

# Is this the primary user of the site?
superuser: true

# Role/position
role: "跨物种开发"

# Organizations/Affiliations
organizations:
- name: East China Normal University
  url: "http://www.ecnu.edu.cn/"

# Short bio (displayed in user profile at end of posts)
bio: 拥抱开源，热爱生活

interests[]:
- Advocating lofty academic feelings and technical feelings!
- Encourage highly respected, open and innovative geek culture!
- Rejecting the “sophisticated egoism”!
- Adhering to the “open”, “equal”, ”positive”, ”mutual respect”, “mutual support” culture!
- Stay hungry, stay foolish

education[]:
  courses:
  - course: PhD in Artificial Intelligence
    institution: Stanford University
    year: 2012
  - course: MEng in Artificial Intelligence
    institution: Massachusetts Institute of Technology
    year: 2009
  - course: BSc in Artificial Intelligence
    institution: Massachusetts Institute of Technology
    year: 2008

# Social/Academic Networking
# For available icons, see: https://sourcethemes.com/academic/docs/page-builder/#icons
#   For an email link, use "fas" icon pack, "envelope" icon, and a link in the
#   form "mailto:your-email@example.com" or "#contact" for contact widget.
social:
# - icon: envelope
#   icon_pack: fas
#   link: '#contact'  # For a direct email link, use "mailto:test@example.org".
# - icon: twitter
#   icon_pack: fab
# # link: https://twitter.com/GeorgeCushen
# - icon: google-scholar
#   icon_pack: ai
# # link: https://scholar.google.co.uk/citations?user=sIwtMXoAAAAJ
- icon: github
  icon_pack: fab
  link: https://github.com/cross-species/E-Slides-Intro
# Link to a PDF of your resume/CV from the About widget.
# To enable, copy your resume/CV to `static/files/cv.pdf` and uncomment the lines below.
# - icon: cv
#   icon_pack: ai
#   link: files/cv.pdf

# Enter email to display Gravatar (if Gravatar enabled in Config)
email: ""

# Organizational groups that you belong to (for People widget)
#   Set this to `[]` or comment out if you are not using People widget.
user_groups:
- admin
---

**E-slides**是一个教学课件的自动生成平台, 致力于解决教师在备课过程中所遇到的操作繁琐、课程迭代不便等问题。其基本的功能有：
1. 支持在线输入编辑/上传md文件
2. 课件内容自动排版
3. 支持在线编译预览
4. 课件免费下载
5. 长期稳定的备份存储
6. 兼容公式、代码
7. 提供jupyter运行服务
6. 思维导图辅助梳理大纲
 

平台将以在线形式提供服务，用户访问指定网页客户端, 首先选定心仪的模版, 随后，进入在线编辑页面或上传自己的markdown文件, 即可获得由文件内容自动生成的pdf课件。

E-slides的技术架构由前端、服务端、后端三个部分组成。
- 在Request链路中：前端部分对用户的请求进行解析、提供在线编辑引导等一系交互功能，并将用户数据打包发送给客户端；客户端进行用户内容的正则解析、数据重构与数据备份；后端则根据用户选定的模板，运行latex编译器，进行pdf格式的课件生成，同时将pdf等文件路径存储在后端运行的数据库中。
- 在Return链路中：后端向服务端返回pdf所在路径，服务端接收并发送给前端，前端以pdf嵌入网页的形式向用户提供课件预览。

<!-- **X-Lab** is a combination of two leading and pioneering laboratories from **computer science** and **data science and engineering** respectively in Tongji University (同济大学) and East China Normal University (华东师范大学).The lab is supported by a number of core members, including doctorial supervisors, Ph.D students, master students and undergraduate students.

**X-Lab** is an intercross multi-discipline, cutting-edge research lab which focuses on the following research domains: **Cloud Computing, Big Data, Data Intelligence,** and **Education Science & Technology**.

With regard to the lab culture, we keep all along holding the several opinions below:
- Advocating lofty academic feelings and technical feelings!
- Encourage highly respected, open and innovative geek culture!
- Rejecting the “sophisticated egoism”!
- Adhering to the “open”, “equal”, ”positive”, ”mutual respect”, “mutual support” culture!
- Stay hungry, stay foolish

Your attention to our lab would be highly appreciated. It’s not only our pursuit but also our faith endeavoring to build a harmonious team with a strong sense of belonging: mentors and students like one family!

<font color='orangered'>* We are always looking for highly-motivated students to work with us on the exciting area of computer science. If you are interested, please contact us by email.</font> -->
