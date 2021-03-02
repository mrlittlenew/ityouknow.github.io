---
layout: post
title: elasticsearch IK分词
category: elasticsearch
tags: [elasticsearch,IK]
keywords: elasticsearch,ik

---


## 中文分词器使用

[https://github.com/medcl/elasticsearch-analysis-ik](https://github.com/medcl/elasticsearch-analysis-ik)



## 安装方法

./bin/elasticsearch-plugin install https://github.com/medcl/elasticsearch-analysis-ik/releases/download/v6.3.0/elasticsearch-analysis-ik-6.3.0.zip

安装文件地址可以通过[releases](https://github.com/medcl/elasticsearch-analysis-ik/releases) 获取最新版本


## 验证分词器

``` shell
POST http://localhost:9200/_analyze
{
  "text": "美国阿拉斯加州发生8.0级地震",
  "tokenizer": "ik_smart"
}
```

## 远程词典配置

IKAnalyzer.cfg.xml can be located at {conf}/analysis-ik/config/IKAnalyzer.cfg.xml or {plugins}/elasticsearch-analysis-ik-*/config/IKAnalyzer.cfg.xml

``` xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE properties SYSTEM "http://java.sun.com/dtd/properties.dtd">
<properties>
	<comment>IK Analyzer 扩展配置</comment>
	<!--用户可以在这里配置自己的扩展字典 -->
	<entry key="ext_dict">custom/mydict.dic;custom/single_word_low_freq.dic</entry>
	 <!--用户可以在这里配置自己的扩展停止词字典-->
	<entry key="ext_stopwords">custom/ext_stopword.dic</entry>
 	<!--用户可以在这里配置远程扩展字典 -->
	<entry key="remote_ext_dict">location</entry>
 	<!--用户可以在这里配置远程扩展停止词字典-->
	<entry key="remote_ext_stopwords">http://xxx.com/xxx.dic</entry>
</properties>

``` 

## 致命问题

两个位置的配置文件并非OR的关系。
在{conf}/analysis-ik/config/IKAnalyzer.cfg.xml
配置了远程扩展字典。

而没有在{plugins}/elasticsearch-analysis-ik-*/config/IKAnalyzer.cfg.xml
配置远程扩展字典的情况下，
远程字典将会失效。

此情况在elasticsearch-analysis-ik-7.10.2版本存在。






