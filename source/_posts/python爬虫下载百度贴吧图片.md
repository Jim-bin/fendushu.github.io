---
title: python爬虫下载百度贴吧图片
date: 2017-03-04 18:32:13
tags: python
---
利用python的requests模块下载百度贴吧图片
<!--more-->

```python
# -*- coding: utf-8 -*-
import requests
from bs4 import BeautifulSoup

url = 'http://tieba.baidu.com/p/4468445702'
html = requests.get(url)
html.encoding = 'utf-8'
text = html.text

bsop = BeautifulSoup(text,'html.parser')
img_list = bsop.find('div',{'id':'post_content_87286618651'}).findAll('img')
img_src = img_list[0].attrs['src']

print(img_src)
img = requests.get(img_src)
with open('1.jpg', 'ab') as f:
    f.write(img.content)
    f.close()
```