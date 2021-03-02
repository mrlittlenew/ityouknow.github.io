---
layout: post
title: elasticsearch 中文分词（elasticsearch-analysis-hanlp）
category: elasticsearch
tags: [elasticsearch,hanlp]
keywords: elasticsearch,hanlp

---


## 中文分词器使用

[https://github.com/KennFalcon/elasticsearch-analysis-hanlp](https://github.com/KennFalcon/elasticsearch-analysis-hanlp)



## 安装方法

./bin/elasticsearch-plugin install https://github.com/KennFalcon/elasticsearch-analysis-hanlp/releases/download/v6.5.4/elasticsearch-analysis-hanlp-6.5.4.zip

安装文件地址可以通过[releases](https://github.com/KennFalcon/elasticsearch-analysis-hanlp/releases) 获取最新版本


## 验证分词器

``` shell
POST http://localhost:9200/_analyze
{
  "text": "美国阿拉斯加州发生8.0级地震",
  "tokenizer": "hanlp"
}
```

## 远程词典配置

配置文件为ES_HOME/config/analysis-hanlp/hanlp-remote.xml

``` xml
<properties>
    <comment>HanLP Analyzer 扩展配置</comment>

    <!--用户可以在这里配置远程扩展字典 -->
    <entry key="remote_ext_dict">words_location</entry>

    <!--用户可以在这里配置远程扩展停止词字典-->
    <entry key="remote_ext_stopwords">stop_words_location</entry>
</properties>
``` 

## 致命问题

自定义词热更新大概1分钟更新。
但只能增加新词，删除无法移除，只能通过重启ES生效。

此情况在 elasticsearch-analysis-hanlp-7.10.2 版本存在







