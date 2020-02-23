### find
* How to delete file(s) by relative time?

There are some unused dmgs as follows. 
```bash
ls ~/Library/Containers/com.tencent.WeWorkMac/Data/Upgrade -lrt
total 1647024
-rw-------@ 1 eric  staff  68902200 Dec 11 18:59 WXWork_2.8.19.2003.dmg
-rw-------@ 1 eric  staff  68850075 Dec 26 17:09 WXWork_3.0.0.2009.dmg
-rw-------@ 1 eric  staff  68850959 Jan  8 15:49 WXWork_3.0.1.2005.dmg
-rw-------@ 1 eric  staff  76773843 Jan 19 14:19 WXWork_3.0.2.2011.dmg
-rw-------@ 1 eric  staff  76935675 Feb  4 06:21 WXWork_3.0.4.2023.dmg
-rw-------@ 1 eric  staff  76943239 Feb  5 05:44 WXWork_3.0.6.2030.dmg
-rw-------@ 1 eric  staff  76995381 Feb  9 01:22 WXWork_3.0.7.2036.dmg
-rw-------@ 1 eric  staff  76368807 Feb 13 00:47 WXWork_3.0.7.2053.dmg
-rw-------@ 1 eric  staff  76017209 Feb 15 13:31 WXWork_3.0.8.2067.dmg
-rw-------@ 1 eric  staff  77944603 Feb 21 14:33 WXWork_3.0.10.2094.dmg
-rw-------@ 1 eric  staff  77980301 Feb 23 20:53 WXWork_3.0.10.2096.dmg
```
I want to delete the dmg(s) except the latest one.
```bash
find . ! -newer WXWork_3.0.10.2094.dmg | xargs rm
```
