# Python爬取站长之家图片(正则表达式)

## 1.导入爬虫请求库

```python
import requests
import re
import os
```

## 2.创建本地存放下载图片的文件夹

```python
download = "pic"

# 若已经创建，则调用；若没有，则创建
if  not os.path.exists(download):
    os.mkdir(download)
```

## 3.请求的网址

```Python
url = "https://sc.chinaz.com/tupian/shanshuifengjing.html"
```

## 4.使用requests向url发请求,response接收响应

```python
response = requests.get(url)
```

## 5.编写正则

```
pattern = r'<img src2="(.*)" alt=".*">'
imgUrlList = re.findall(pattern,response.content.decode('utf-8'))
```

## 6.遍历每一张图片的路径

```python
i=1
for imgUrl in imgUrlList:
```

## 7.向每一个图片发请求，响应为每个图片的二进制内容

```python
with open("{}/{}.jpg".format(download,i),'wb') as file:
```

## 8.将图片的二进制内容写入到本地生成文件

```python
file.write(  requests.get("https:"+imgUrl).content   )
    print("第{}张图片下载完成".format(i))
    i+=1
```



## 附件：完整代码

```python
#导入爬虫请求库
import requests
import re
import os

# 本地创建存放图片的文件夹
download = "pic"
if  not os.path.exists(download):
    os.mkdir(download)

    # 请求的网址
url = "https://sc.chinaz.com/tupian/shanshuifengjing.html"

# 使用requests向url发请求,response接收响应
response = requests.get(url)

# 编写正则表达式
pattern = r'<img src2="(.*)" alt=".*">'
imgUrlList = re.findall(pattern,response.content.decode('utf-8'))

# 遍历每一张图片的路径
i=1
for imgUrl in imgUrlList:

    # 向每一个图片发请求，响应为每个图片的二进制内容
    with open("{}/{}.jpg".format(download,i),'wb') as file:
        
        # 将图片的二进制内容写入到本地生成文件
        file.write(  requests.get("https:"+imgUrl).content   )
    print("第{}张图片下载完成".format(i))
    i+=1
```

