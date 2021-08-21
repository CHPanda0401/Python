# (四)Python中的CSV存储英雄数据

```python
import csv
import requests

#获取所有英雄id，返回列表
def getHeroIdList():
    heroList = requests.get(herolist_url).json()['hero']
    return [ hero['heroId']    for hero in heroList]

#根据英雄id获取详情的方法
def saveHeroInfo():
    for id in heroIdList:
        heroInfo = requests.get(heroinfo_url.format(id)).json()['hero']
        #csv中写入数据
        with open("lol_data.csv",'a',newline='',encoding='utf-8') as file:
            csv.writer(file).writerow(
                [
                    heroInfo['heroId'],heroInfo['name'],heroInfo['alias'],
                    heroInfo['title'],heroInfo['roles'],heroInfo['hp'],
                    heroInfo['mp'],heroInfo['movespeed'],heroInfo['armor'],
                    heroInfo['attackrange'],heroInfo['hpregen'],heroInfo['attackdamage']
                ]
            )
        print("{}下载完成".format(heroInfo['name']))
if __name__ == '__main__':
    #main函数中的变量是全局变量(其他函数可以随意使用)
    herolist_url="https://game.gtimg.cn/images/lol/act/img/js/heroList/hero_list.js"
    heroinfo_url="https://game.gtimg.cn/images/lol/act/img/js/hero/{}.js"
    heroIdList = getHeroIdList()
    with open("lol_data.csv", 'w', newline='', encoding='utf-8') as file:
        csv.writer(file).writerow(
            [
                'id','名称','英文名','标题','角色','血量','蓝量','移速','护甲','攻击范围','生命回复','攻击伤害'
            ]
        )
    #调用获取详情的方法
    saveHeroInfo()
```

