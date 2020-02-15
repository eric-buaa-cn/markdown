Laptop -> Wireless Access Point -> Switch -> Router -> Modem -> Internet Cloud

man 7 ip
man 7 tcp
man 7 socket

## lsof

### Introduction

lsof was created by Victor A. Abell and is a utility that lists open files. As everything in Linux can be considered a file, this means that lsof can gather information on the majority of activity on your machine, including network interfaces and network connections. lsof by default will output a list of all open files and the processes that opened them.

The two main drawbacks of lsof are that it can only display information about the local machine(localhost), and that it requires administrative privileges to print all available data.

### Examples

* Running lsof with -r option puts lsof in repeat mode.
> lsof -r 2

* Make lsof to output IPv4 network connections only.
> lsof -i4

* Output TCP connections of IPv4 protocol.
> lsof -i4TCP

* Output UDP connection of IPv6 protocol.
> lsof -i6UDP

* Logically ADD all options
> lsof -a -nPi -u work

* Using regular expressions.
> lsof -c /^.....$/

* Show all ESTABLISHED IPv4 connections.
> lsof -a -i4 -s TCP:ESTABLISHED

* Find network connections from or to an external host, or with a port range.
> lsof -i @example.host
> lsof -i @example.host:200-250

* Display open files under a given directory.
> lsof +D /etc

### Command Line Options

The lsof binary supports a large number of command line options, including the following:

| Option     | Description                                                  |
| ---------- | ------------------------------------------------------------ |
| -h         | This option present a help screen.                           |
| -a         | This option tells lsof to logically ADD all provided options. |
| -b         | This option tells lsof to avoid kernel functions that might block the returning of results. This is a very specialized option. |
| -l         | If converting a user ID to a login name is working improperly or slowly, you can disable it using the -l parameter. |
| -P         | The -P option prevents the conversion of port numbers to port names for network files. |
| -u list    | The -u option allows you to define a list of login names or user ID numbers whose files will be returned. The -u option supports the ^ character for excluding the matches from the output. |
| -c list    | The -c option selects the listing of files for processes executing the commands that begins with the characters in the list. This supports regular expressions, and also supports the ^ character for executing the matches from the output. |
| -p list    | The -p option allows you to select the files for the processes whose process IDs are in the list. The -p option supports the ^ character for excluding the matches from the output. |
| -g list    | The -g option allows you to select the files for the processes whose optional process group IDs are in the list. The -g option supports the ^ character for excluding the matches from the output. |
| -s         | The -s option allows you to select the network protocols and states that interest you. The -s option supports the ^ character for excluding the matches from the output. The correct form is PROTOCOL:STATE. Possible protocols are UDP and TCP. Some possible TCP states are: CLOSED, SYN-SENT, SYN-RECEIVED, ESTABLISHED, CLOSE-WAIT, LAST-ACK, FIN-WAIT-1, FIN-WAIT-2, CLOSING, and TIME-WAIT. Possible UDP states are Unbound and Idle. |
| +d s       | The +d option tells lsof to search for all open instances of directory s and the files and directories it contains at its top level. |
| +D d       | The +D option tells lsof to search for all optn instances of directory d and all the files and directories it contains to its complete depth. |
| -d list    | The -d option specifies the list of file descriptors to display. It supports the ^ character for excluding the matches from the output. -d 1,^2 means include fd 1, and exclude fd 2. |
| -i4        | This option is used for displaying IPv4 data only.           |
| -i6        | This option is used for displaying IPv6 data only.           |
| -i         | The -i option without any values to tell lsof to display network connections only. |
| -i ADDRESS | The -i option with a value will limit the displayed information to match that value. Some example values are TCP:25 for displaying TCP data that listens to port number 25, @google.com for displaying information related to google.com, :25 for displaying information related to port number 25, :POP3 for displaying information related to the port number that is associated to POP3 in the /etc/services file, etc. You can also combine hostnames and IP address with port numbers and protocols, for example, TCP:172.27.130.12:9001. |
| -t         | The -t option tells lsof to display process identifiers without a header line. This is particularly useful for feeding the output of lsof to the kill command or to a script. Notice that -t automatically selects the -w option. |
| +w/-w      | The +w/-w option enables or disables the supression of warming messages. |
| -r TIME    | The -r option causes the lsof command to repeat every TIME seconds until the command is manually terminated with an interrupt. |
| +r TIME    | The +r command, with the + prefix, acts the same as the -r command, but will exit its loop when it fails to find any open files. |
| -n         | The -n options inhibits the conversion of network numbers to host names for network files. |

<https://www.linode.com/docs/networking/diagnostics/lsof/>

<https://www.akadia.com/services/lsof_quickstart.txt>

<https://www.howtoforge.com/linux-lsof-command/>

<http://www.361way.com/lsof-ss-netstat/4351.html>

https://www.thegeekstuff.com/2012/08/lsof-command-examples

## ss

### 简介

ss(Socket Statistics)命令可以展示socket统计信息，与netstat展示方式类似，但更加高效（ss直接从内核读取信息，而netstat读取 /proc 目录的若干个文件），信息更为丰富（增加了哪些信息）。

### 使用场景

* 展示本地（localhost）所有socket信息
> ss
```txt
Netid  State      Recv-Q Send-Q Local Address:Port                 Peer Address:Port
udp    ESTAB      0      0      172.27.130.12:39629                222.88.95.225:61430
udp    ESTAB      0      0      172.27.130.12:53232                121.14.47.198:61430
tcp    ESTAB      0      0      127.0.0.1:47080                127.0.1.1:8801
tcp    ESTAB      0      0      172.27.130.12:9000                 172.27.130.12:51490
tcp    ESTAB      0      0      172.27.130.12:49156                183.36.111.115:9048
```

* 展示本地（localhost）所有IPv4 socket信息
> ss -4
```txt
Netid  State      Recv-Q Send-Q Local Address:Port                  Peer Address:Port
udp    ESTAB      0      0      172.27.130.12:39629                222.88.95.225:61430
udp    ESTAB      0      0      172.27.130.12:53232                121.14.47.198:61430
```

* 展示本地（localhost）所有IPv6 socket信息
> ss -6
```txt
Netid  State      Recv-Q Send-Q Local Address:Port                 Peer Address:Port
tcp    ESTAB      0      0        ::ffff:172.27.130.12:35540                  ::ffff:172.27.130.12:4182
tcp    ESTAB      0      0        ::ffff:172.27.130.12:56432                  ::ffff:172.27.130.12:5181
```

* 展示本地（localhost）所有IPv4 TCP socket信息
> ss -4t
```txt
State      Recv-Q Send-Q Local Address:Port                 Peer Address:Port
ESTAB      0      0      127.0.0.1:47080                127.0.1.1:8801
ESTAB      0      0      172.27.130.12:9000                 172.27.130.12:51490
```

* 展示本地（localhost）所有IPv6 UDP socket信息
> ss -6u
```txt

```

* 展示LISTEN状态的TCP socket信息
> ss -lt
>
> ss -lt sport = :9000
```txt
State      Recv-Q Send-Q Local Address:Port                 Peer Address:Port
LISTEN     0      128    172.27.130.12:9000                     *:*
```

* 展示所有（LISTEN状态和非LISTEN状态）TCP socket信息
> ss -at
```txt
State      Recv-Q Send-Q    Local Address:Port                     Peer Address:Port
LISTEN     0      128       172.27.130.12:9000                                *:*
ESTAB      0      0         172.27.130.12:9000                    172.27.130.12:51490
```

* 展示所有（LISTEN状态和非LISTEN状态）TCP socket信息，同时显示pid信息
> ss -atp
```txt
State      Recv-Q Send-Q    Local Address:Port                     Peer Address:Port
LISTEN     0      128       172.27.130.12:9000                                *:*                     users:(("java",pid=20003,fd=202))
ESTAB      0      0         172.27.130.12:51490                   172.27.130.12:9000                  users:(("java",pid=20140,fd=503))
```

* 展示socket统计信息
> ss -s
```txt
Total: 376 (kernel 0)
TCP:   111 (estab 49, closed 8, orphaned 0, synrecv 0, timewait 2/0), ports 0

Transport Total     IP        IPv6
*	  0         -         -
RAW	  0         0         0
UDP	  12        12        0
TCP	  103       54        49
INET	  115       66        49
FRAG	  0         0         0
```

* 展示时解析地址和端口号
> ss -r
```txt
State      Recv-Q Send-Q    Local Address:Port                     Peer Address:Port
ESTAB      0      0          bigdata-dev2:ssh                     172.18.101.55:61645
```

* 展示时不解析地址和端口号
> ss -n
```txt
State      Recv-Q Send-Q      Local Address:Port                     Peer Address:Port
ESTAB      0      0           172.27.130.12:50916                   172.27.130.12:29092
```

* 展示socket内存信息
> ss -4tm
```txt
State      Recv-Q Send-Q    Local Address:Port                     Peer Address:Port
ESTAB      0      0             127.0.1.1:9702                        127.0.0.1:41076
	 skmem:(r0,rb2227051,t0,tb3939840,f0,w0,o0,bl0)
```

* 展示TCP内部信息
> ss -4ti
```txt
State      Recv-Q Send-Q    Local Address:Port                     Peer Address:Port
ESTAB      0      0             127.0.0.1:47080                       127.0.1.1:8801
bbr wscale:7,7 rto:204 rtt:0.15/0.017 ato:40 mss:65483 cwnd:11 bytes_acked:1638424 bytes_received:287240 segs_out:19797 segs_in:9900 send 38416.7Mbps lastsnd:14264 lastrcv:14264 lastack:14264 rcv_rtt:452784 rcv_space:43810
```

* 基于TCP状态展示socket信息
> ss -t state listening
```txt
Recv-Q Send-Q         Local Address:Port                          Peer Address:Port
0      128            172.27.130.12:9000                                     *:*
```

> ss -t state time-wait
```txt
Recv-Q Send-Q         Local Address:Port                          Peer Address:Port
0      0                  127.0.1.1:epmd                             127.0.0.1:44919
```

可用的状态过滤器有：
* established
* syn-sent
* syn-recv
* fin-wait-1
* fin-wait-2
* time-wait
* closed
* close-wait
* last-ack
* listening
* closing

一些通配状态过滤器有：
* all (上面的所有状态过滤器)
* connected (除了listening和closed的所有状态过滤器)
* synchronized (除了syn-sent的所有connected状态过滤器)

* 基于源端口范围展示socket信息
> ss -t sport le 500
```txt
State      Recv-Q Send-Q    Local Address:Port                     Peer Address:Port
ESTAB      0      0         172.27.130.12:ssh                     172.18.101.55:61645
```

> ss -t sport gt 9000
```txt
State      Recv-Q Send-Q    Local Address:Port                     Peer Address:Port
ESTAB      0      0             127.0.0.1:47080                       127.0.1.1:8801
```

> ss -t '( sport = :ssh )'
```txt
State      Recv-Q Send-Q    Local Address:Port                     Peer Address:Port
ESTAB      0      0         172.27.130.12:ssh                     172.18.101.55:61645
```

* 基于目的端口范围展示socket信息
> ss dport = 8007
```txt
Netid  State      Recv-Q Send-Q     Local Address:Port                      Peer Address:Port
tcp    ESTAB      0      0         172.18.101.56:30200                   172.18.101.55:8007
tcp    ESTAB      0      0         172.18.101.56:39610                    172.18.101.56:8007
```

* 展示Timer信息
> ss -to
```txt
State      Recv-Q Send-Q    Local Address:Port                     Peer Address:Port
ESTAB      0      0         172.27.130.12:9000                    172.27.130.12:51490                 timer:(keepalive,72min,0)
```

* 展示连接到特定机器的socket信息
> ss -t4 dst 172.28.233.140
> ss -t4 src 172.27.130.12
```txt
State      Recv-Q Send-Q    Local Address:Port                     Peer Address:Port
ESTAB      0      0         172.27.130.12:ssh                    172.28.233.140:57752
```



### ifconfig

Used to view TCP/IP configuration.

* 显示MAC地址
> ifconfig

### ping

Used to check connectivity between networking devices.

### arp

Used to view and manage the arp cache.

### traceroute

Used to view the entire path a packet takes to get from one device to another.

### netstat

Used to display TCP/IP statistics and connections.

### route

Used to display and manage the routing table.

### host

DNS lookup

> host www.google.com
>
> The result is as follows:
>
> www.google.com has address 216.58.220.196
> www.google.com has IPv6 address 2001::45ab:e549

### iftop

Iftop is used to display bandwidth usage on network interface.

### nload

Nload is a console application which monitors the network traffic in real time, and outputs the data channel load in the form of a drawing separately for inbound and outbound traffic. It also provides additional info like total amount of transferred data, the minimum and maximum bandwidth, etc.

### nmon

Monitor cpu/memory/disk usage.

### ipcalc

计算IP地址的网段信息

### other tools

masscan

nmap

arp-scan



### 其他

* host name to ip
> ping google.com
> dig google.com
> host google.com

* 展示网络接口
> * ifconfig
> * ip link show
> * netstat -i
> * netstat -ie

* 展示路由表
> * ip route
> * netstat -r

* 域名解析
> * dig hostname
> * nsloopup
> * host

* 抓包工具
> tcpdump

* 网络连通性测试
> ping

* 端口检测
> nmap
<https://securitytrails.com/blog/top-15-nmap-commands-to-scan-remote-hosts>

* Packet Traveling
<https://www.youtube.com/watch?v=rYodcvhh7b8>

* 在IPv6地址上监听1234端口
> nc -6 -l 1234
> lsof -i:1234 -nP
```txt
COMMAND   PID USER   FD   TYPE             DEVICE SIZE/OFF NODE NAME
nc      87000 eric    3u  IPv6 0xbd324f68e879a635      0t0  TCP *:1234 (LISTEN)
```
> nc [::1] 1234

* How to show NIC speed
> ip link show
> ethtool eth0

* TCP state transition diagram

![TCP state transition diagram](https://www.ibm.com/support/knowledgecenter/SSLTBW_2.1.0/com.ibm.zos.v2r1.halu101/dwgl0004.gif)



* socat
> tcp proxy