---
title: Hexo配置
date: 2020-08-24 10:12:59
tags: Hexo
categories: Hexo
---
版本：4.2.0

官方技术文档：[hexo](https://hexo.io/docs/)

## 换源

```bash
npm install -g cnpm --registry=https://registry.npm.taobao.org
```

## next

```bash
cd <your_blog_dirname>
git clone https://github.com/theme-next/hexo-theme-next themes/next
```

```bash
vim <your_blog_dirname>/_config.yml
# 修改theme为next
theme: next
```


## 统计字数及阅读所需时间

```bash
# 安装hexo-symbols-count-time
cd <your_blog_dirname>
npm install hexo-symbols-count-time
```
如果没有配置`symbols_count_time`，将会使用默认配置，`symbols_count_time`配置如下：

```bash
# <your_blog_dirname>/_config.xml
symbols_count_time:
  symbols: true # 统计单篇文章字数
  time: true #计算阅读所需时间
  total_symbols: true # 统计全部文章总计字数
  total_time: true # 统计阅读全部文章所需时间
  exclude_codeblock: false # 排除对代码块的计数
  awl: 2 # CN ≈ 2\EN ≈ 5\RU ≈ 6
  wpm: 275 # Slow ≈ 200\Normal ≈ 275\Fast ≈ 350
  suffix: "mins." #若时间小于60分钟，将suffix作为后缀
```

在Next主题下集成了hexo-symbols-count-time，其配置选项如下：

```bash
# <your_blog_dirname>/theme/next/_config.yml
symbols_count_time:
  separated_meta: true # 是否单独一行显示
  item_text_post: true # 是否显示统计数据前的文字
  item_text_total: false # 是否显示底部统计数据前的文字
```

> 参考材料：
>
> ​	[1] [hexo-symbols-count-time 官方Github](https://github.com/theme-next/hexo-symbols-count-time)
>
> ​	[2] [启用字数和阅读时间预估](https://laytonsun.com/learning/2020-04/enable-word-count.html)




