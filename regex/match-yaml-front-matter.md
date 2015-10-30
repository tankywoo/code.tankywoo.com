---
title: '正则匹配YAML Front Matter'
description: 'regex match yaml front matter'
tag: yaml,jekyll
date: 2015-10-25 22:01
id: UVMgMQ77
---

YAML Front Matter 见 [Jekyll](http://jekyllrb.com/docs/frontmatter/) 解释.

我的 [Simiki](https://github.com/tankywoo/simiki) 和 [tfcs](https://github.com/tankywoo/tfcs) 都是用的这个格式.

使用正则匹配, 区分post的meta和body两个部分, 现在的解决方案:

	regex = re.compile('(?sm)^---(?P<meta>.*?)^---(?P<body>.*)')


第一个里面的`(?sm)`表示:

* s - dotall，默认dot匹配除\n以外字符, 这个可以匹配包括\n
* m - multiple line, 表示多行模式, 适用于^表示每行的首字母匹配

这种匹配模式需要在模式的开头定义。也可以在compile配置第二个参数flag。不过前者就相当于把所有的都写入模式中了。

注意这里的三个横线号指定了`^`开头. 否则如这种情况就会匹配:

	---
	title: "xxx ---"  # <- 匹配这里
	xxx
	---

另外, `(?P<meta>.*?)` 注意这里最后的问号，python的re是贪婪匹配，如上的情况，其实是匹配最后一个, 如果这里加上了问号，就是匹配第一个。 处理的是这种情况:

	---
	xxx
	---
	正文
	...
	---      # <— 默认会匹配到这里，导致yaml报错: expected a single document in the stream
	...


关于修改re的贪婪匹配为匹配第一次出现, 参考 [Match first instance of Python regex search](http://stackoverflow.com/questions/5074331/match-first-instance-of-python-regex-search)

其它参考:

* [Python Regex to match YAML Front Matter](http://stackoverflow.com/questions/9756392/python-regex-to-match-yaml-front-matter)
* [How to generate a blog-wide word count in Jekyll](http://hypertext.net/2013/02/jekyll-word-count/)

不过这两个链接里的解决方案都或多或少有点问题, 没有考虑上面提到的情况.
