---
title: spider
author: 'xingqi'
date: '2022-10-16'
slug: spider
study: []
life: []
---
什么是爬虫

--通过编写程序 ，模拟浏览器上网，然后在其互联网上抓取数据的过程。

#### 1.爬虫的价值：

~~~~--实际应用

~~~~

--就业

爬虫是否合法

--在法律中是不被禁止的

--具有违法的风险

--善意爬虫  恶意爬虫

###### 爬虫的风险体现在下面2个方面;

--爬虫干扰了被访问网站的正常运行

--爬虫抓取了收到法律保护的特定类型的数据或信息

###### 如何避免在编写爬虫过程中进局子？

--时常优化自己的程序，避免干扰被访问网站的正常运行

--在使用，传播抓取数据时，审核抓取到的内容，如果发现涉及到用户的隐私

商业机密等敏感内容需要及时停止爬取或传播



###### 爬虫在场景中的分类

一.通用爬虫

​			抓取的是系统重要组成部分。抓取的是一整张页面数据。

二.聚焦爬虫

​			建立在通用爬虫的基础上。抓取页面的局部内容。

三.增量式爬虫

​			检测网站中更新的情况。只会抓取更新出来的数据。



#### 2.反爬机制

​		门户网站，可以通过制定相应的策略或技术手段，防止爬虫程序进行 网站

数据的爬取

反反爬策略

爬虫程序可以通过制定相关的策略或者技术手段，破解门户网站中具备的反爬机制。

robots.txt协议

​		君子协议。规定了网站上哪些数据可以被爬取，哪些数据不可以被爬取。

http协议：

​		--就是服务器与客户端数据交互的一种形式。

常用请求头信息

​		--User-Agent:请求载体的身份标识。

​		--Connection：请求完毕后是断开连接还是保持连接

常用响应头信息

​		--Content-Type:服务器响应回客户端的数据类型

https协议：

​		--安全的超文本传输协议

###### 



requests模块

​	-urllib模块

​	-requests模块

requests模块;

python中原生的一款基于网络请求模块，功能非常强大，简单便捷，效率极高。

作用:模拟浏览器发请求。

如何使用（requests模块的编码流程）：

​		指定url

```
mport requests
if __name__=="__main__":
    url="https://www.sogou.com/web"
```

​		发起请求

```
kw=input("enter a word:")
param={
    "query":kw
}
response=requests.get(url=url,params=param)
```

​		获取响应数据

```
page_text=response.text
```

​		持久化存储

```
fileName=kw+"html"#新建一个html的文件夹用于存放爬取到的数据
with open(fileName,"w",encoding="utf-8")as fp:
    fp.write(page_text)
```

安装环境：

​		pip install requests

###### #UA**检测**（反反爬）：门户网站的服务器会检测对应请求的载体身份标识，如果检测到请求的载体身份

为某款浏览器，说明该请求为正常的请求。但是，如果检测到的载体身份标识不是某一款浏览器，则表示为不正常的请求，则服务器并部给予响应。拒绝该次请求。

UA——User-Agent(请求载体身份标识)

查找浏览器的UA只需要在浏览器根路劲输入about:version，用户代理的一行就是User-Agent.

#### 3.**UA伪装**：

让爬出对应的请求载体身份标识为某一款浏览器

实战编码;

​		需求;爬取搜狗首页的页面数据

为了使每一次的请求都能成功，需要进行UA伪装

```
import requests
#需求：爬取搜狗首页的数据
if __name__=="__main__":
    #第一步：指定url
    url="https://www.sogou.com/"
    #第二部:发起请求，使用get返回一个响应对象
    reponse=requests.get(url=url)
    #第三步：返回响应数据.text返回的是字符串形式的响应数据
    page_text=reponse.text
    print(page_text)
    #第四步：将=数据进行持久化存储
    with open('./sougou.html','w',encoding='utf-8')as fp:
        fp.write(page_text)
    print('爬取数据结束!!!')
```

实战巩固

​		-需求：爬取搜狗指定词条对应的搜索结果页面（简易网页采集器）

UA检测，UA伪装

```
import requests
if __name__=="__main__":
    url="https://www.sogou.com/web"
    #处理url携带的参数，封装到字典中
    kw=input("enter a word:")
    param={
        "query":kw
    }
    #向url发起请求，并且相应的url是携带参数的，并且在请求过程中解决了参数
    #获取响应数据
    response=requests.get(url=url,params=param)
    #持久化存储
    page_text=response.text
    fileName=kw+"html"#新建一个html的文件夹用于存放爬取到的数据
    with open(fileName,"w",encoding="utf-8")as fp:
        fp.write(page_text)
    #爬取成功进行提示
    print(fileName,"保存成功!!!")
```

​		-需求：破解百度翻译

post请求：含参数

响应数据是json数据

```
import requests
import json
if __name__=="__main__":
    #1.获取url
    post_url="https://fanyi.baidu.com/sug"
    #2.进行UA伪装
    headers={
        "User-Agent":"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/96.0.4664.110 Safari/537.36 Edg/96.0.1054.62"
    }

    #3.post请求参数处理，同get相同
    # 进行data数据参数处理,将它进行封装
    word=input("enter a word")
    data={
        "kw":word
    }
    #4.发送请求
    response=requests.post(url=post_url,data=data,headers=headers)
    #5.获取响应数据，json()方法返回的是obj(对象)，如果确定数据是json才能使用json（）
    dic_obj=response.json()
    #永久化存储
    fileName=word+".json"
    fp=open(fileName,'w',encoding='utf-8')
    json.dump(dic_obj,fp=fp,ensure_ascii=False)#不要在括号前面写等号
    print("over!!!")
```

​		-需求：抓取豆瓣电影（“[豆瓣电影 (douban.com)](https://movie.douban.com/)”）中的电影详情数据

```
import requests
import json
if __name__=="__main__":
    #1.指定url
    url="https://movie.douban.com/j/chart/top_list"
    #创建一个prame参数，用于封装参数
    parame={
        'type': '24',
        'interval_id': '100:90',
        'action':'',
        'start': '20',#从库中的第几部电影开始取,可以通过改变他从而来改变不同提取信息
        'limit': '20'#一次性取几步电影
    }
    #进行UA伪装
    header={
        "User-Agent":"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/96.0.4664.110 Safari/537.36 Edg/96.0.1054.62"
    }
    #获取数据，如浏览器所示，采用的方法是get方法
    response=requests.get(url=url,params=parame,headers=header)
    #获取的数据采用json文件进行存储
    list_data=response.json()

    fp=open("./douban.json",'w',encoding="utf-8")
    json.dump(list_data,fp=fp,ensure_ascii=False)
    print("over!!!")
```

​		-需求：查询肯德基餐厅查询http://www.kfc.com.cn/kfccda/index.aspx中指定餐厅地点数据

```
import requests
import json
if __name__=="__main__":
    #1.指定url
    post_url="http://www.kfc.com.cn/kfccda/ashx/GetStoreList.ashx?op=keyword"
    #2.进行UA伪装
    headers={
    "User-Agent":"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/96.0.4664.110 Safari/537.36 Edg/96.0.1054.62"
    }
    #3.进行信息获取
    address=input("请输入要查询哪个餐厅的城市")
    #采用字典将输入的参数进行封装
    data={
        "keyword":address
    }
    # 4.发送请求
    param={
        'cname':'',
        'pid':'',
        'keyword': '北京',
        'pageIndex': '1',
        'pageSize': '10'
    }
    response = requests.post(url=post_url, data=data,params=param, headers=headers)
    # 5.获取响应数据，json()方法返回的是obj(对象)，如果确定数据是json才能使用json（）
    list_data = response.json()

    # 永久化存储
    fileName = address + ".json"
    fp = open(fileName, 'w', encoding='utf-8')
    json.dump(list_data, fp=fp, ensure_ascii=False)  # 不要在括号前面写等号
    print("over!!!")
```

​		-需求：爬取国家药管总局中基于中华人名共和国化妆品生产许可证等相关数据[化妆品生产许可信息管理系统服务平台 (nmpa.gov.cn)](http://scxk.nmpa.gov.cn:81/xk/)

使用ctrl+F可以进行抓取搜寻

###### 动态加载出来的数据有不同的url，是由ajax请求得到的。

通过对详情url的观察发现：

​		-url的域名都是一样的，只有携带的参数不一样

​		-id值可以从首页对应的ajax请求得到的json串中获取

​		-域名和id值拼接在一起形成一个完整的企业对应详情页的url.

```
import requests
import json
if __name__=="__main__":
    #1.批量获取不同企业对应的id
    url="http://scxk.nmpa.gov.cn:81/xk/itownet/portalAction.do?method=getXkzsList"
    #2.进行UA伪装
    headers={
        'User-Agent':"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/96.0.4664.110 Safari/537.36 Edg/96.0.1054.62"
    }
    id_list = []
    all_data_json = []
    #获取参数,当数据页发生变化时，获取全部数据
    for page in range(1,6):
        page=str(page)
        params={
            'on': 'true',
            'page': 'page',
            'pageSize': '15',
            'productName':'',
            'conditionType': '1',
            'applyname':'',
            'applysn':''
        }

        id_text=requests.post(url=url,headers=headers,params=params).json()
        for id in id_text['list']:
            id_list.append(id['ID']);
    #print(id_list)
    #获取网页的详情数据
    post_url="http://scxk.nmpa.gov.cn:81/xk/itownet/portalAction.do?method=getXkzsById"
    #获取参数
    for id in id_list:
        data={
            "id":id
        }
        detail_data=requests.post(url=post_url,headers=headers,data=data).json()
        all_data_json.append(detail_data)
        #print(detail_data)
    #永久化封装存储
    fp=open("./换妆品数据1.html",'w',encoding="utf-8")
    json.dump(all_data_json,fp=fp,ensure_ascii=False)
    print("over!!!!")
```

#### 4.数据解析

###### 聚焦爬虫：爬取页面中指点的页面内容。

​	-编码流程：

​			-指定url

​			-发起请求

​			-获取响应数据

​			-数据解析

​			-持久化存储

数据解析分类：

​		--正则

​		 --bs4

​		 --xpath

数据解析原理概述：

​		-解析的局部的文本内容都会在标签之间或标签对应的属性中进行存储

​		-1.进行指定标签的定位

​		-2。标签或者标签对应的属性中存储的数据值进行提取（解析）

数据解析案列

1.爬取糗事百科中糗图板块下所有的糗事图片

content返回的是二进制形式的图片数据

text 字符串  json()(对象)

#### 5.正则表达式


![aa](https://github.com/zxingq/down/raw/main/img/aa.png)

![image-20220325220057299](https://github.com/zxingq/down/raw/main/img/image-20220325220057299.png)

![1652593773936](https://github.com/zxingq/down/raw/main/img/1652593773936.png)


![1652593926625](https://github.com/zxingq/down/raw/main/img/1652593926625.png)

**\d:匹配数字**

**\w:匹配字母，数字，下划线**

**\s：匹配空白**

**\b；匹配单词的边界**

\D:匹配所有的非数字

\w:匹配所有的非字母，数字，下划线

\S:匹配所有非空白

^:匹配开始

$:匹配结束

.  :匹配任意字符，除了换行符

| *    | 匹配前面的子表达式零次或多次。要匹配 * 字符，请使用 \*。  |
| ---- | --------------------------------------------------------- |
| .    | 匹配除换行符 \n 之外的任何单字符。要匹配 . ，请使用 \. 。 |

？:可选字符，可以出现也可以不出现，

| ?    | 匹配前面的子表达式零次或一次，或指明一个非贪婪限定符。要匹配 ? 字符，请使用 \?。 |
| ---- | ------------------------------------------------------------ |
|      |                                                              |

{}：表示数字的个数

()：用于分组

re.sub('a','A','abcdacd')：在第三个中查找到a用A来替换

bs4进行数据解析

​	-数据解析的原理：

​	-1.标签定位

​	-2.提取标签，标签属性中存储数据值

-bs4数据解析的原理：

​	-1.实列化一个BeautifulSoup对象，并且将页面源码数据加载到对象中

​	-2.通过调用BeautifulSoup对象中相关的属性或者方法进行标签定位和数据提取

-环境安装

​		-pip install bs4

​		-pip install lxml

-如何实列化BeautifulSoup对象

​	-from bs4 import BeautifulSoup

​	-对象实例化：

​		-1.将本地的html文档中的数据加载到对象中

​					fp=open('./test.html','r',encoding='utf-8')

​					soup=BeautifulSoup(fp,'lxml')

​		-2.将互联网上的页面数据加载到对象中

​				page_text=response.text

​				soup=BeautifulSoup(page_text,'lxml')

​		-提供用于数据解析的方法和属性：

​			-soup.tagName:返回文档中第一次出现的tagName对应的标签

​			-soup.find():

​				-find('tagName'):等于soup.div

​				-属性定位

​					-soup.find('div',class_/id/attr='song')

​				-soup.find_all('tagName'):返回符合要求的所有标签（列表）

​			-select:

​					-select('某种选择器(id,cloass,标签...选择器)')，返回的是一个列表

​					-层级选择器

​							-soup.select('.tang>ul>li>a'):>表示的是一个层级

​							-oup.select('.tang>ul  a'):空格表示的是多个层级 

 	-获取标签中的文本数据：

​			-soup.a.text/string/get_text()

​			-text/get_text():可以获取某一标签中所有的文本内容

​			-string;只能获取该标签下面的直系文本内容

​	-获取标签中的属性值：

​			-soup.a['herf' ]

###### **实例：爬取诗词名句中三国演义的标题和详情页内容**

```
import requests
from bs4 import BeautifulSoup
#需求：爬取三国演义小说所有章节标题和章节内容
if __name__=="__main__":
    #指定章节标题页的url
    url="http://www.shicimingju.com/book/sanguoyanyi.html"
    headers={
        "User-Agent":"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/97.0.4692.71 Safari/537.36 Edg/97.0.1072.62"

    }
    page_text=requests.get(url=url,headers=headers).text
    #在章节中解析出标题和详情页数据的url
    #实例化BeautifulSoup对象，需要将页面详情源码数据加载到该对象中
    soup=BeautifulSoup(page_text,'lxml')
    #先创立一个文档用于持久化存储详情页的内容
    fp=open('./sanguo.txt','w',encoding='utf-8')
    #解析章节标题和详情页的url
    li_list=soup.select('book-mulu>ul>li')
    for li in li_list:
        title=li.a.string
        #解析出每一个详情页对应的url
        detail_url='http://www.shicimingju.com'+li.a['href']
        #对详情页发起请求，获取详情页的数据内容,内容以文本形式展现出来
        detail_page_text=requests.get(url=detail_url,headers=headers).text
        #解析出详情页中相关的章节内容，需要创建新的实例化对象
        detail_soup=detail_page_text(detail_page_text,'lxml')
        #由检查源码可知详情页的数据存在与指定的p标签中
        div_tag=detail_soup.find('div',class_ ='chapter_content')
        #解析到了章节内容，进行持久化存储
        content=div_tag.text
        fp.write(title+':'+content+'\n')
        print(title,'爬取成功')

```



​		 xpath解析：最常用并且最便捷高效的一种解析方式。通用性		

​				-xpath解析原理：

​					-1.实例化一个etree的对象，且需要将被解析的页面源码数据加载到该对象中

​					-2.调用etree对象中的xpath方法结合着xpath表达式实现标签的定位和内容的捕获。

   -环境的安装;

​       -pip install lxml

  -如何实例化一个entree对象:from lxml import entree

​			-1.将本地的html文档中的源码数据加载到entree对象中：

​				entree.parse(filePath)

​			-2.可以将从互联网上获取的源码数据加载到该对象中

​				entree.HTML('page_text')

​			-xpath('xpath表达式')

-xpath表达式：

​		-/:表示的是一个层级。表示从根节点开始。

​		-//表示的是多个层级，可以可以表示从任意位置开始定位。

​		-属性定位：//div[@class='song'] tag[@attrName='attrValue']

​		-索引定位：///div[@class='song']/p[3]索引是从1开始的。这里表示的就是第三个p标签里面的内容

​		-取文本：

​			-/text()获取的是标签中直系的文本内容

​			-//text()标签中非直系的文本内容（所有的文本内容）

​			-取属性：

​					/@attrName          ==>img/src img/@src

案例：解析下载图片[4K动漫壁纸_高清4K动漫图片_彼岸图网 (netbian.com)](https://pic.netbian.com/4kdongman/)

```python
import requests
from lxml import etree
import  os
if __name__=='__main__':
    #获取指定的url
    url="https://pic.netbian.com/4kdongman/"
    headers={
        "User-Agent":"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/97.0.4692.71 Safari/537.36 Edg/97.0.1072.62"

    }
    response=requests.get(url=url,headers=headers)
    #手动设置响应数据编码格式
    #response.encoding='utf-8'
    page_text=response.text
    #数据解析，src属性和alt属性
    #将从互联网上获取的源码数据加载到该对象中
    tree=etree.HTML(page_text)
    #要获取图片找到图片对应的位置
    li_list=tree.xpath('//div[@class="slist"]/ul/li')
    if not os.path.exists('./Picture'):
        os.mkdir('./Picture')
    #采用循环去获取到每一张图片的src和alt
    for li in li_list:
        image_src='https://pic.netbian.com'+li.xpath('./a/img/@src')[0]
        image_name=li.xpath('./a/img/@alt')[0]+'.jpg'
        #通用用于处理中文乱码问题
        image_name=image_name.encode('iso-8859-1').decode('gbk')
        #print(image_name,image_src)
        #请求图片，进行持久化存储
        img_data=requests.get(url=image_src,headers=headers).content
        img_path='Picture/'+image_name#拼成图片的存储文件路径
        with open(img_path,'wb') as fp:
            fp.write(img_data)
            print(image_name + '下载成功')

```





爬取站长素材中免费的简历模板

```python
import requests
from lxml import etree
import  os
if __name__=='__main__':
    #获取指定的url
    url="https://pic.netbian.com/4kdongman/"
    headers={
        "User-Agent":"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/97.0.4692.71 Safari/537.36 Edg/97.0.1072.62"

    }}
#创建一个文件夹
if not os.path.exists('./resumelibs'):  # 如果不存在
    os.mkdir('./resumelibs')

url = 'http://aspx.sc.chinaz.com/query.aspx?keyword=%E5%85%8D%E8%B4%B9&classID=864'
page_text = requests.get(url=url,headers=headers).text

tree = etree.HTML(page_text)
div_list = tree.xpath('//div[@id="container"]/div')

for div in div_list:
    resume_src = div.xpath('./a/@href')[0]
    resume_name = div.xpath('./a/img/@alt')[0]+'.zip'

    #对每个简历页面发起请求
    detail_text = requests.get(url=resume_src, headers=headers).text
    tree1 = etree.HTML(detail_text)
    #解析出下载链接
    download_src = tree1.xpath('//div[@class="clearfix mt20 downlist"]/ul/li[1]/a/@href')[0]

    #对下载链接发起请求
    down_load_resume = requests.get(url=download_src, headers=headers).content
    down_load_path = 'resumelibs/' + resume_name
    
    with open( down_load_path,'wb') as fp:
         fp.write(down_load_resume)
         print(resume_name,'下载成功！！！！')

```

#### 6.模拟登陆

验证码，识别验证码图片中的数据用于模拟登录操作

模拟登录

- -点击登录按钮之后发出一个post请求
- 每次发起请求，验证码都会发生变化

编码流程：

1.验证码识别，获取验证码图片文字数据

2.对post发起请求

3.对相应数据进行永久化存储

##### cookie

**在模拟登录成功之后，http/https协议特征：无状态**要保证模拟登录时候不在需要登录，利用post请求直接实现自动登录。

- 发起的第二次基于个人主页页面的请求的时候，服务器并不知道此请求是基于登陆状态下的请求
- cookie:用来让服务器记录客户端相关的状态

可以在compile文件中寻找到cookie(不推荐)-----手动处理，通过抓包工具获取包中的cookie值，将cookie进行封装

--自动处理：

cookie来源于哪里？

- --模拟登录post请求后，由客户端创建
- session会话对象
  - 可以进行请求的发送
  - 如果请求过程中产生了cookie则cookie将会被自动存储/携带在该session对象中

- 创建一个session对象：session=requests.Session()
- 使用session对象进行模拟登录post请求的发送(cookie会被存储在session对象中)
- session对象对个人主页对应的get请求进行发送(携带cookie)



#### 7.代理

- 代理服务器

作用：

- 突破自生IP访问的权限，隐藏自生真是ip

相关的代理网站

- 快代理
- 西祠代理
- www.goubanjia.com
- http://ip.yqie.com/proxyhttps/

代理IP的类型

- http类型

- https类型

  代理IP透明度

  - ​    透明：服务器知道此次请求知道使用代理，也知道真实的本机IP
  - 匿名：知道使用了代理，但是不知道真实ip
  - 高匿：不知道使用了代理，更不知道真实的IP

#### 异步爬虫

同步爬虫时可以发现在进行get请求时往往会发生阻塞

- 目的：

  - 爬虫时进行高性能数据爬取

- 方法

  - 多线程，多进程
  - 好处：可以为相关阻塞的操作单独开启线程或进程 ，阻塞操作就可以异步执行
  - 弊端：无法无限制的开启多线程或多进程

  线程池，进程池

  - 好处：可以降低系统的开销
  - 弊端：池中线程或进程的数量是有限制的







#### 

#### selenium

selenium模块的基本使用

---便捷的获取到网站中动态加载出来的数据

---便捷实现模拟登录

什么是selenium模块？

- 基于浏览器自动化的一个模块

selenium 的使用流程：

- 环境安装
- 下载一个浏览器的驱动程序
  - 下载路径：http://chromedriver.storage.googleapis.com/index.html

- 实例化一个浏览器对象
- 让浏览器发起一个指定url对应的请求bro.get('url')
- 获取浏览器当前页面的的页面源码数据bro.page_source

![image-20220404221727806](https://github.com/zxingq/down/raw/main/img/image-20220404221727806.png)

设置无头浏览器：

```python
from selenium.webdriver.chrome.options import Options

chrom_options=Options()
chrom_options.add_argument('--headless')
chrom_options.add_argument('--disable-gpu')
bro=webdriver.Chrome(options=chrom_options)

```

实现规避检测：

```python
#实现规避检测
from selenium.webdriver import ChromeOptions

option=ChromeOptions()
option.add_experimental_option('excludeSwitches',['enable-automation'])
bro=webdriver.Chrome(chrome_options=chrom_options,options=option)

```





```python
selenium案例：古诗文登录
from selenium import webdriver
from time import sleep
import requests
from lxml import etree
from hashlib import md5
from PIL import Image

class Chaojiying_Client(object):

    def __init__(self, username, password, soft_id):
        self.username = username
        password =  password.encode('utf8')
        self.password = md5(password).hexdigest()
        self.soft_id = soft_id
        self.base_params = {
            'user': self.username,
            'pass2': self.password,
            'softid': self.soft_id,
        }
        self.headers = {
            'Connection': 'Keep-Alive',
            'User-Agent': 'Mozilla/4.0 (compatible; MSIE 8.0; Windows NT 5.1; Trident/4.0)',
        }

    def PostPic(self, im, codetype):
        """
        im: 图片字节
        codetype: 题目类型 参考 http://www.chaojiying.com/price.html
        """
        params = {
            'codetype': codetype,
        }
        params.update(self.base_params)
        files = {'userfile': ('ccc.jpg', im)}
        r = requests.post('http://upload.chaojiying.net/Upload/Processing.php', data=params, files=files, headers=self.headers)
        return r.json()

    def ReportError(self, im_id):
        """
        im_id:报错题目的图片ID
        """
        params = {
            'id': im_id,
        }
        params.update(self.base_params)
        r = requests.post('http://upload.chaojiying.net/Upload/ReportError.php', data=params, headers=self.headers)
        return r.json()


bro=webdriver.Chrome()
#将浏览器设为全屏
bro.maximize_window()
bro.get('https://so.gushiwen.cn/user/login.aspx?from=http://so.gushiwen.cn/user/collect.aspx')
#对当前页面进行截图
bro.save_screenshot('aa.png')
#对当前页面的验证码图片进行xpath定位
img_code=bro.find_element('xpath','//img[@id="imgCode"]')
print(img_code)
#图片坐标
locations = img_code.location
print(locations)
#图片大小
sizes = img_code.size
print(sizes)
# 构造指数的位置
rangle = (int(locations['x']),int(locations['y']),int(locations['x'] + sizes['width']),int(locations['y'] + sizes['height']))
print(rangle)
a=Image.open('aa.png')
farm=a.crop(rangle)
farm.save('verification.png')
print("图片截取成功!")
result = Chaojiying_Client('17687012990', 'zxq119712', '930964')  # 用户中心>>软件ID 生成一个替换 96001
im = open('./verification.png', 'rb').read()  # 本地图片文件路径 来替换 a.jpg 有时WIN系统须要//
Code_Pic=result.PostPic(im, 1004)
#上面的返回的是一个字典，利用键值的特点显示出值即为验证码的数据
result1=str.upper(Code_Pic['pic_str'])
print(result1)
#将本地的图片进行上传
user=bro.find_element('id','email')
user.send_keys('17687012990')
sleep(1)
pwd=bro.find_element('id','pwd')
pwd.send_keys('zxq119712')
sleep(1)
ver=bro.find_element('id','code')
ver.send_keys(result1)
sleep(2)
but=bro.find_element('id','denglu')
but.click()


```



### scrapy框架

--什么是框架：

- 就是集成了很多功能并且具有很强通用性的项目模板

- scrapy
  - 爬虫封装好的一个明星框架。功能：高性能的持久化存储，异步的数据下载，高性能的数据解析
  - 创建一个工程：scapy startproject xxxPro(工程名)
  - cd  xxxProscrapy
  - 在spiders子目录中创建一个文件夹
    - -scrapy genspider spiderName www.xxx.com

  - 执行工程：
    - scrapy crawl spiderName

##### **''.join(content)将列表转换为字符串**

##### 五大基本组成

Scrapy框架主要由五大组件组成，它们分别是调度器(Scheduler)、下载器(Downloader)、爬虫（Spider）和实体管道(Item Pipeline)、Scrapy引擎(Scrapy Engine)。下面我们分别介绍各个组件的作用。

(1)、调度器(Scheduler):

调度器，说白了把它假设成为一个URL（抓取网页的网址或者说是链接）的优先队列，由它来决定下一个要抓取的网址是 什么，同时去除重复的网址（不做无用功）。用户可以自己的需求定制调度器。

(2)、下载器(Downloader):

下载器，是所有组件中负担最大的，它用于高速地下载网络上的资源。Scrapy的下载器代码不会太复杂，但效率高，主要的原因是Scrapy下载器是建立在twisted这个高效的异步模型上的(其实整个框架都在建立在这个模型上的)。

(3)、 爬虫（Spider）:

爬虫，是用户最关心的部份。用户定制自己的爬虫(通过定制正则表达式等语法)，用于从特定的网页中提取自己需要的信息，即所谓的实体(Item)。 用户也可以从中提取出链接,让Scrapy继续抓取下一个页面。

(4)、 实体管道(Item Pipeline):

实体管道，用于处理爬虫(spider)提取的实体。主要的功能是持久化实体、验证实体的有效性、清除不需要的信息。

(5)、Scrapy引擎(Scrapy Engine):

Scrapy引擎是整个框架的核心.它用来控制调试器、下载器、爬虫。实际上，引擎相当于计算机的CPU,它控制着整个流程。


整体框架图

 <img src="https://img-blog.csdnimg.cn/20200321114058862.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2NrNzg0MTAxNzc3,size_16,color_FFFFFF,t_70" alt="img" style="zoom: 50%;" /> 

##### 项目创建
blo
```
scrapy startproject 项目名

scrapy genspider 爬虫名 域名
执行工程
scrapy crawl 爬虫名

```

