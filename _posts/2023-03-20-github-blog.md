---
layout: post
title: Blog building tutorial and error learn
date: 2023-03-18 11:01:00
description: an example of a blog building.
categories: Blog
tags: formatting building
---

**Note:** This blog is powered by [Jekyll](https://jekyllrb.com/) with [al-folio](https://github.com/alshedivat/al-folio/) theme. Hosted by [GitHub Pages](https://pages.github.com/).

这篇主要讲下怎么具体的实现个人网站构建的过程，并总结自己花费两三天总结的问题。
具体如下：

1.下载编译：使用fork或use this template，将[al-folio](https://github.com/alshedivat/al-folio/)主题包转化成自己的repo，然后注意**这个repo名修改成自己用户名**，之后下载如下
```bash
git clone git@github.com:<用户名>/<用户名>.git
```

2.线上初步部署，在vscode的新终端进行推送

* vscode打开 _config.yml， 修改url改成 https://<用户名>.github.io，baseurl 留空
* 推送指令
    ```bash
    git init
    git add readme.md # 初步简单推上去，主要是为了配置相关选项  
    git commit -m “blog1”  
    git push -u origin master  
    # 第一次需要使用 -u 命令，之后直接 'git push' 就好了
    # git push --force origin master  #当推送失败可以试试这个，意义为强制推送
    ```
* 首次推送包成功后，在github包的Action选项中选择Enable Github Actions，之后在Settings选项中选择 Actions -> General -> Workflow permissions 中开启读写权限
* 重新提交：git add . -> git commit -m “blog2” -> git push
* 等待GitHub包的自动部署，之后会构建出一个gh-pages分支， 这个就是用来看最终网页的
* 进入Settings->Pages选项中，Brance选择gh-pages branch + /(root)，保存
* 等待刷新会看到： Your site is live at https://<用户名>.github.io/，访问即可， 部署成功
* Github actions总是在master分支进行编译，然后把页面的html都push到gh-pages 分支下并部署到Github Pages网页

3.在本地windows环境下配置+修改Jekyll环境：
* 下载安装[RubyInstaller](https://rubyinstaller.org/)
* 右键打开Git bash, 命令行安装jekyll 和 bundler
    ```bash
    gem install jekyll  bundler
    ```
* 使用VScode打开下载的repo，打开对应的终端安装该包所需插件
    ```bash
    bundle install
    ```
* 本地编译并查看网页，三者任选一个
    ```bash
    jekyll serve 
    jekyll s
    bundle exec jekyll serve
    ```
* 浏览器直接访问 [http://127.0.0.1:4000/](http://127.0.0.1:4000/)
* 如此即可随时在本地修改源代码并进行网站效果查看

  #### 实际遇到的报错解决如下
  * 注释+添加相应插件
  ```bash
    # gem 'mini_racer'
    gem 'unicode_utils'
    gem "kramdown"
    gem "kramdown-parser-gfm"
    gem "rouge"
    gem "webrick", "~> 1.7"
    gem 'wdm', '>= 0.1.0'  
  ```


4. 个性化主题本地修改
* News，project, blog 分别在 _news, _projects,  _posts文件夹进行对比学习+修改
* News小标题+文字的格式排版修改: 打开_includes->news.html
    ```bash
    <th scope="row>
    <div class="col-sm-3 p-0">
    <span class="badge primary-color-dark darken-1 font-weight-bold text-uppercase align-middle date">{{ item.date | date: "%b %-d, %Y" }}</span>
    </div>
    </th>
    ```
* Publications修改
    * 参考模板bib，填充相应的小框及对应的问题，在_includes->bib.html可拓展展示的内容，
    * 加粗自己的名字显示格式，并注释掉more_authors相关行
        ```bash
        {%- if author_is_self -%}
        <strong>
        <span style="color:#024f92">{{author.first}} {{author.last}}</span>
        </strong>
        <!-- <em>{{author.first}} {{author.last}}</em> -->
        {%- endif -%}
        ```
    * 相关内容放在首页，打开_pages->about文件，选择publications: true. bibtex条目中添加selected={true}
* 其他格式修改方法：针对自己喜欢的模板，F12刷新该网页，直接看对应的代码，基本能确定静态页面的相关参数和设计。之后在自己repo里面搜索相关的设置参数进行修改

5.最终推送
* Gemfile文件修改，回复出事的参数，不然action会报错
* 类似步骤2，重新提交：git add . -> git commit -m “blog2” -> git push


6. TODO——将public repo改成private repo
* 通过公开仓储 + 私有仓储 + Github Actions的配置，实现参考: [GitHub 私有仓库免费开启 GitHub Pages 的可行性方案](https://zhuanlan.zhihu.com/p/541944539)
* **问题：通过网页刷新F12，他人还是能看到所有的代码和参数配置，只是稍微麻烦一下而已**