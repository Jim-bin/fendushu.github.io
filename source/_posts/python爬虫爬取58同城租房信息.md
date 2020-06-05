---
title: python爬虫爬取58同城租房信息
date: 2017-03-04 19:01:53
tags: python
---
python爬取58同城租房信息
<!--more-->

```python
# -*- coding: utf-8 -*-

import requests, random, re, time, csv, codecs
from bs4 import BeautifulSoup

def zu_fang(url):

    try:
        r = requests.get(url, headers=headers)
        r.encoding = 'utf8'
        text = r.text
        soup = BeautifulSoup(text, 'html.parser')
        ul = soup.find('ul', {'class':'listUl'})
        li_list = ul.findAll('li',{'sortid':re.compile("^\d")})

        titles = []
        links = []
        rooms = []
        dizhis = []
        prices = []
        for li in li_list:
            title = li.find('div',{'class':'des'}).find('h2').find('a').text
            link = li.find('div',{'class':'des'}).find('h2').find('a').attrs['href']
            room = li.find('div',{'class':'des'}).find('p',{'class':'room'}).text
            dizhi = li.find('div',{'class':'des'}).find('p',{'class':'add'}).find('a', {'target':'_blank'}).text
            price = li.find('div',{'class':'money'}).find('b').text
            print(title, link, room, dizhi, price)
            print("------------------------------------------")
            titles.append(title)
            links.append(link)
            rooms.append(room)
            dizhis.append(dizhi)
            prices.append(price)
        return titles, links, rooms, dizhis, prices
    except:
        print("爬取错误")
        return None

UserAgent_List = [
	"Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.1 (KHTML, like Gecko) Chrome/22.0.1207.1 Safari/537.1",
	"Mozilla/5.0 (X11; CrOS i686 2268.111.0) AppleWebKit/536.11 (KHTML, like Gecko) Chrome/20.0.1132.57 Safari/536.11",
	"Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/536.6 (KHTML, like Gecko) Chrome/20.0.1092.0 Safari/536.6",
	"Mozilla/5.0 (Windows NT 6.2) AppleWebKit/536.6 (KHTML, like Gecko) Chrome/20.0.1090.0 Safari/536.6",
	"Mozilla/5.0 (Windows NT 6.2; WOW64) AppleWebKit/537.1 (KHTML, like Gecko) Chrome/19.77.34.5 Safari/537.1",
	"Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/536.5 (KHTML, like Gecko) Chrome/19.0.1084.9 Safari/536.5",
	"Mozilla/5.0 (Windows NT 6.0) AppleWebKit/536.5 (KHTML, like Gecko) Chrome/19.0.1084.36 Safari/536.5",
	"Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/536.3 (KHTML, like Gecko) Chrome/19.0.1063.0 Safari/536.3",
	"Mozilla/5.0 (Windows NT 5.1) AppleWebKit/536.3 (KHTML, like Gecko) Chrome/19.0.1063.0 Safari/536.3",
	"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_8_0) AppleWebKit/536.3 (KHTML, like Gecko) Chrome/19.0.1063.0 Safari/536.3",
	"Mozilla/5.0 (Windows NT 6.2) AppleWebKit/536.3 (KHTML, like Gecko) Chrome/19.0.1062.0 Safari/536.3",
	"Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/536.3 (KHTML, like Gecko) Chrome/19.0.1062.0 Safari/536.3",
	"Mozilla/5.0 (Windows NT 6.2) AppleWebKit/536.3 (KHTML, like Gecko) Chrome/19.0.1061.1 Safari/536.3",
	"Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/536.3 (KHTML, like Gecko) Chrome/19.0.1061.1 Safari/536.3",
	"Mozilla/5.0 (Windows NT 6.1) AppleWebKit/536.3 (KHTML, like Gecko) Chrome/19.0.1061.1 Safari/536.3",
	"Mozilla/5.0 (Windows NT 6.2) AppleWebKit/536.3 (KHTML, like Gecko) Chrome/19.0.1061.0 Safari/536.3",
	"Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/535.24 (KHTML, like Gecko) Chrome/19.0.1055.1 Safari/535.24",
	"Mozilla/5.0 (Windows NT 6.2; WOW64) AppleWebKit/535.24 (KHTML, like Gecko) Chrome/19.0.1055.1 Safari/535.24"
]
headers = {'User-Agent':random.choice(UserAgent_List),
            'Accept':"text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8",
            'Accept-Encoding':'gzip',
          }
page = 3
info_list = []
for i in range(1, page+1):
    url = 'http://bj.58.com/chuzu/0/pn' + str(i) + '/?minprice=0_1500'
    print("正在爬取第" + str(i) + "页租房信息")
    titles, links, rooms, dizhis, prices = zu_fang(url)


    for j in range(len(titles)):
        info = []
        info.append(titles[j].replace('\xa0', '').strip())
        info.append(links[j].replace('\xa0', '').strip())
        info.append(rooms[j].replace('\xa0', '').strip())
        info.append(dizhis[j].replace('\xa0', '').strip())
        info.append(prices[j].replace('\xa0', '').strip())

        with open('a.csv',"a",newline="") as f:
            # f.write(codecs.BOM_UTF8)
            csv_writer = csv.writer(f, dialect='excel')
            csv_writer.writerow(info)

    time.sleep(3)

# for i in info_list:
#     for j in i:
#         # print(j)
#         with open('a.csv', 'w') as f:
#             csv_writer = csv.writer(f, dialect='excel')
#             csv_writer.writerow(j.encode(encoding='utf_8'))


```
