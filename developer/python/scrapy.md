# scrapy 爬虫框架

## 命令行
用于创建和运行scrapy项目和项目。
```
scrapy 
```

## 基本的爬虫
继承scrapy.Spider类， 同时定义其属性，及实现方法parse用于解析响应内容。
```
import scrapy

class DmozSpider(scrapy.Spider):
    name = "dmoz"
    allowed_domains = ["dmoz.org"]
    start_urls = [
        "http://www.dmoz.org/Computers/Programming/Languages/Python/Books/",
        "http://www.dmoz.org/Computers/Programming/Languages/Python/Resources/"
    ]

    def parse(self, response):
        filename = response.url.split("/")[-2]
        with open(filename, 'wb') as f:
            f.write(response.body)

```

命令行启动爬取,scrapy crawl [spiderName]
```
scrapy crawl dmoz
```
* https://scrapy-chs.readthedocs.io/zh_CN/0.24/intro/tutorial.html
* https://scrapy-chs.readthedocs.io/zh_CN/0.24/topics/spiders.html
## Item对象
用于在parse中返回一个对象，从而处理数据。
```
class DmozItem(scrapy.Item):
    title = scrapy.Field()
    link = scrapy.Field()
    desc = scrapy.Field()
```
重写parse为: 
```
    def parse(self, response):
        data = DmozItem()

        filename = response.url.split("/")[-2]
        with open(filename, 'wb') as f:
            f.write(response.body)

        data.title = ""
        data.link = ""
        ....
```

* https://scrapy-chs.readthedocs.io/zh_CN/0.24/topics/items.html
## Selector选择器
在parse方法中， 将会自动传入一个响应对象response, 可以通过对象的
response.selector获取一个选择器。
常用的选择器有： xpath,re ...
重写parse为：
```
data = DmozItem()
        # xpath选择器 实例
        el = response.selector.xpath("/div[id='main']")
        # 或者也可以简写为
        el = response.xpath("/div")

        data.title = ""
        data.link = ""
```
* https://scrapy-chs.readthedocs.io/zh_CN/0.24/topics/selectors.html

## Item Pipeline
当parse方法获取到Item后，将会自动传入ItemPipeline，你可以咋item pipeline中序列化数据，入库等。Item Pipeline需要注册到scrapy项目配置的 ITEM_PIPELINES 下：

```
import json

class JsonWriterPipeline(object):

    def __init__(self):
        self.file = open('items.jl', 'wb')

    def process_item(self, item, spider):
        line = json.dumps(dict(item)) + "\n"
        self.file.write(line)
        return item
```
配置示例: 
```
ITEM_PIPELINES = {
    'myproject.pipelines.PricePipeline': 300,
    'myproject.pipelines.JsonWriterPipeline': 800,
}
```

* https://scrapy-chs.readthedocs.io/zh_CN/0.24/topics/item-pipeline.html



## 通过feed保存爬取数据文件


## link Extractors
若只是想提取链接，那么可以通过link extractors

## 其他
通过: ImagesPipeline 下载图片。

* ImagesPipeline https://scrapy-chs.readthedocs.io/zh_CN/0.24/topics/images.html#

通过 scrapyd 部署和管理你的爬虫项目，适合大型爬取工程。
* https://scrapyd.readthedocs.io/en/latest/overview.html

限速爬取配置：AutoThrottle

* https://scrapy-chs.readthedocs.io/zh_CN/0.24/topics/autothrottle.html
