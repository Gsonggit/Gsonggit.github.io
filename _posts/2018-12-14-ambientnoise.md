---
layout: post
title: '地震背景噪声处理（MSnoise使用）'
date: 2018-12-14
author: 路过音乐
color: rgb(255,210,32)
categories: myorigion
tags: 地震学 背景噪声
---


本文记载毕业论文中关于《地震背景噪声监测地壳波速变化》的数据处理部分，主要用到python编写的[MSnoise库](http://www.msnoise.org) <br>

1.数据来源于IRIS，下载获得miniSEED格式（仅包含波形数据）和dataless SEED格式（仅包含台站元数据，可以提取仪器响应）数据，通过rdseed解压转换为SAC格式  
2.按官网步骤将MSnoise安装完毕，建立新目录并通过bash执行msnoise install  
3.msnoise提供网页浏览模式，通过msnoise admin命令并打开浏览器127.0.0.1:5000浏览，修改Configuration中的相应值，由于msnoise不支持此次数据的命名模式，需要修改Configuration标签下的data_structure，并在目录下编写custom.py，通过msnoise scan_archive导入数据后可在Database标签中查看  
4.由于台站仪器可能不同，需要去除仪器响应，仪器响应原理比较复杂，可参考seisman博文[https://blog.seisman.info/instrumental-response/](https://blog.seisman.info/instrumental-response/)及其相关文章，msnoise中可修改response_format和response_path选项将仪器响应文件放入指定路径  
5.配置好后，依次执行msnoise new_jobs增加任务，msnoise compute_cc计算单日互相关，msnoise stack叠加指定天数的互相关，互相关结果存放于该目录下的STACKS文件夹  
