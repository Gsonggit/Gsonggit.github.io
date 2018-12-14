---
layout: post
title: 'DIA项目记录'
date: 2018-11-16
author: 路过音乐
color: rgb(255,210,32)
categories: myorigion
tags: DIA scrapy python
---



## 前言 <br>
一直想做个项目，名字为DiveIntoAmusement(DIA),项目地址在[另一篇博客](http://www.lgyysblog.com/entertain/2018/09/19/entertainv1.html)，原定目标是:<br>
1.搜索。利用用户关键词爬虫综合爬取相关信息    <br>
2.推荐。利用用户记录训练模型利用ACL算法推荐  <br>
涉及的方面还挺多的，前端、爬虫、数据库、推荐算法等  <br>
此博客用于记录项目过程遇到的大问题及解决办法  <br>


## [1]前端 <br>
# 1.想在网页加入iframe，但是显示空白 <br>
我遇到2种情况，<br>
1是默认博客使用https协议而iframe目标网页使用http，会提示不能访问http的资源，故使用此项目在iframe中查看结果须用http访问；<br>
2是需要修改iframe目标网页服务器设置，使得网页可以被其他网站引用，例如本项目Django中setting将XFrameOptions中间件注释掉<br>


## [2]爬虫  <br>
# 1.scrapy爬虫出现forbidden by robots.txt  <br>
scrapy会默认遵守待爬网址robot.txt的爬取规范，只需在scrapy的setting中将ROBOTSTXT_OBEY 设定为 False即可	<br>
# 2.scrapy中使用Xpath路径得到空内容 <br>
scrapy爬取的和浏览器中显示的Xpath路径可能不一致，因为scrapy爬取的是网页源代码，需要直接查看网页源代码，再确定Xpath



## [3]数据库



## [4]推荐算法



## [5]其他