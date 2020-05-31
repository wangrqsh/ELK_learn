#### 资源链接

https://www.elastic.co/cn/start

elasticsearch官方基础视频教程

https://www.elastic.co/cn/webinars/getting-started-elasticsearch?elektra=startpage

kibana官方基础视频教程

https://www.elastic.co/cn/webinars/getting-started-kibana?elektra=startpage


当前最新版本  Elasticsearch 7.7.0

1.运行环境

	a.JDK8+  
	b.系统可用内存>2G 
	c.win7

2.下载 个人觉得迅雷相对较快 

https://artifacts.elastic.co/downloads/kibana/kibana-7.7.0-windows-x86_64.zip

https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.7.0-windows-x86_64.zip



#### 运行启动


Windows:
<pre>cd elasticsearch/bin
elasticsearch.bat</pre>
<pre> kibana.yml 
elasticsearch.hosts: ["http://localhost:9200"]
若elasticsearch开启用户密码则需要配置
elasticsearch.username: "elastic"
elasticsearch.password: "changeme"
国际化中文界面开启
i18n.locale: "zh-CN"
启动双击
bin/kibana.bat
浏览器访问  http://localhost:5601/
</pre>



####  基本使用

http://localhost:5601/

菜单点击dev-tools工具进行基本使用调试

![image-20200531141637885](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200531141637885.png)

##### 计算集群中文档的数量

GET _count
{
    "query": {
        "match_all": {}
    }
}

####  添加文档

PUT  testuser/_doc/1
{
  "name":"kuKi",
  "address":"北京",
  "sex":"女",
  "about":"runing climbing joking",
  "age":24
}

####  检索文档

GET  testuser/_doc/1

####  搜索全部文档

GET  testuser/_search

#### URL参数搜索

GET  testuser/_search?q=address:上海

#### 表达式搜索  match查询

GET  testuser/_search

{"query":{
    "match": {
      "address": "上海"
    }
   }}

####  表达式 匹配加过滤

GET  testuser/_search
{
  "query":{
    "bool": {
      "must": [
        {"match": {
          "address": "上海"
        }}
      ],
      "filter": [
        {
         "range": {
           "age": {
             "gte": 15,
             "lte": 25
           }
         }
        }
      ]
    }
  }
}

####  全文检索 

GET  testuser/_search
{
  "query": {
    "match": {
      "address": "北京"
    }
  }
}

####  检索短语搜索

GET  testuser/_search
{
  "query": {
    "match_phrase": {
      "about": "runing climbing"
    }
  }
}



####  高亮检索结果显示

GET  testuser/_search
{
  "query": {
    "match_phrase": {
      "about": "runing climbing"
    }
  },
  "highlight": {
    "fields": {
      "about": {}
    }
  }
}

#### 聚合分析

GET  testuser/_search
{
  "query":{
    "bool": {
      "must": [
        {"match": {
          "address": "上海"
        }}
      ],
      "filter": [
        {
         "range": {
           "age": {
             "gte": 15,
             "lte": 25
           }
         }
        }
      ]
    }
  }
}

#### 分词处理

GET  testuser/_analyze
{
  "text": ["goods morning every body"]
}



#### 更多特性

suggestions、geolocation、percolation、fuzzy 与 partial matching 等特性后面继续玩

