#配置双Python环境：
- 首先查看Python目录：whereis  Python
- 然后删除Python2：rm -rf python
- 创建Python3链接到原python2的目录上：ln -s /usr/bin/python3 /usr/bin/python
- 然后运行python2和python3：python和python2
- 最后装上pip2和pip3：sudo apt-get install python3-pip python-pip

# 传统爬虫
1.代码：
```python
from bs4 import BeautifulSoup
import requests
import time as tm
import hashlib
import re
from pymongo import MongoClient

def get_str_sha(str):
    sha = hashlib.sha1(str)
    return sha.hexdigest()
user_id = "201703401"
passwd = "201703401"
LoginUrl = "http://221.233.24.23/eams/login.action"
Url = "http://221.233.24.23/eams/stdDetail.action"
client = MongoClient("192.168.244.137",27017)
db = client["mydb"]
col = db["students"]

Header = {
        "User-Agent" : "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/67.0.3396.99 Safari/537.36",
       # "Cookie" : "semester.id=48; JSESSIONID=94C5B1089F6A9634033AC62808407116.node132; adc-ck-jwxt_pools=IEALAKAK; GSESSIONID=94C5B1089F6A9634033AC62808407116.node132",
        }

s = requests.Session()
req = s.get(LoginUrl)
html = req.text

res = re.search("CryptoJS.SHA1\(\'(.*)\' ",html)
opasswd = res.group(1)
passwd = get_str_sha((opasswd+passwd).encode("utf-8"))
print(passwd)
tm.sleep(2)
Data = {
    "username" : user_id,
    "password" : passwd,
    "encodedPassword:" : "",
    "session_locale" : "zh_CN",
}
req = s.post(LoginUrl,data=Data)
print(req.text)

InfoUrl = "http://221.233.24.23/eams/stdDetail.action"
req = s.get(InfoUrl)
html = req.text
soup = BeautifulSoup(html,"lxml")
trs = soup.find_all("tr")
Infos = {}
keys = []
vals = []
print(trs)
for tr in trs[1:-1]:
    tds = tr.find_all("td")
    if len(tds) < 2:
        continue
    print("---------------------------------------------------")
    key1 = tds[0].getText()[:-1]
    val1 = tds[1].getText()
    key2 = tds[2].getText()[:-1]
    val2 = tds[3].getText()
    keys.append(key1)
    keys.append(key2)
    vals.append(val1)
    vals.append(val2)
for i in range(len(vals)-1):
    Infos[keys[i]] = vals[i]
print(Infos)
col.insert_one(Infos)
#print(key1+val1+"\t"+key2+val2)
'''
for idx, td in enumerate(tds):
if idx in [ 4]:
continue
print(td.getText())
'''

```
解释：
```
将数据上传到数据库：col.insert_ine(Infos)(插入文件到数据库中)

```
