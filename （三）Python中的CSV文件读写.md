# （三）Python中的CSV文件读写

## 1. CSV写入文件内容

[TOC]



```python
# csv:逗号分隔值文件格式
import csv

with open("嘻嘻.csv",'w',newline='',encoding='utf-8') as file:
    #1. 获取csv的写编辑对象
    csvWriter = csv.writer(file)
    #2. 一次写入一行
    # csvWriter.writerow(['姓名','年龄','爱好'])
    #3. 一次写入多行数据
    infoList = [
        ['姓名', '年龄', '爱好'],
        ['张某', 22, '打乒乓球球'],
        ['李某', 18, '踢足球'],
        ['王某', 34, '唱歌、跳舞、打游戏']
    ]
    csvWriter.writerows(infoList)
```

## 2. CSV读取文件内容

```python
import csv

with open("发光的大猫.csv",'r',encoding='utf-8') as file:
    #1. 获取csv的读编辑对象,并且将文件的内容加载进来
    csvReader = csv.reader(file)
    for item in csvReader:
        print(item)
        print(item[0],item[1],item[2])
```



#### 注意：1. 向CSV中写入中文内容，使用office的excel打开中文会乱码，WPS的excel打开不会乱码。

#### 2. CSV写入数据时，会出现多换行的情况,将newline=""设置为空字符。

####                    问题一：如何让如何让office的excel打开也不乱码呢？

#### 答：先用记事本或者其他工具将文件的编码修改为utf-8有bom格式，保存之后，  重新使用office的excel打开，中文不再乱码。

