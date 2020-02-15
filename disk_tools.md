## disk tools

<https://www.slideshare.net/brendangregg/linux-performance-analysis-and-tools/>

### dstat

![dstat in action](https://www.opsdash.com/blog/images/disk-monitoring-dstat.gif)

<https://www.2daygeek.com/install-dstat-resource-statistics-process-performance-monitoring-tool-on-linux/>

### atop

![atop in action](https://www.opsdash.com/blog/images/disk-monitoring-atop.gif)

### iotop

![iotop in action](https://www.opsdash.com/blog/images/disk-monitoring-iotop.gif)

* 显示读写磁盘的进程
> sudo iotop -o

### iostat
iostat（I/O statistics）是磁盘负载统计工具，从属于sysstat软件包。
缺点：它不能对某个进程进行分析，仅能对系统做整体分析。

![iostat in action](https://www.opsdash.com/blog/images/disk-monitoring-iostat.gif)

* 显示磁盘统计信息，每2秒显示一次
> iostat -d 2
```txt
Linux 4.9.0-39-custom (ubuntu)  12/21/2019      _x86_64_        (24 CPU)

Device:            tps    kB_read/s    kB_wrtn/s    kB_read    kB_wrtn
sda               1.50         0.58         9.85     933982   15799808
```
tps: 该设备每秒的传输（读或写）次数
kB_read/s: 每秒从设备读取的数据量
kB_wrtn/s: 每秒向设备写入的数据量
kB_read: 记取的数据总量
kB_wrtn: 写入的数据总量

* 显示磁盘使用率，单位M，每2秒显示一次
> iostat -dmx 2
```txt
Linux 4.9.0-39-custom (ubuntu)  12/21/2019      _x86_64_        (24 CPU)

Device:         rrqm/s   wrqm/s     r/s     w/s    rMB/s    wMB/s avgrq-sz avgqu-sz   await r_await w_await  svctm  %util
sda               0.00     0.83    0.03    1.47     0.00     0.01    13.91     0.02   10.04    2.78   10.17   5.57   0.83
```
注:当系统调用需要读取数据的时候，VFS将请求发到各个FS，如果FS发现不同的读取请求读取的是相同Block的数据，FS会将这个请求合并merge
rrqm/s: read request merge per second，每秒进行merge的读操作数目
wrqm/s: write request merge per second, 每秒进行merge的写操作数目
%util: I/O时间占比。若%util接近100%，说明产生的I/O请求太多，I/O系统应该满负荷

* 显示CPU信息，每2秒显示一次
> iostat -c 2
```txt
Linux 4.9.0-39-custom (ubuntu)  12/21/2019      _x86_64_        (24 CPU)

avg-cpu:  %user   %nice %system %iowait  %steal   %idle
           0.46    0.00    0.16    0.10    0.00   99.29
```
%user: CPU在用户态下的时间占比
%nice: CPU在带NICE值的用户态下的时间占比
%system: CPU在系统态下的时间占比
%iowait: CPU等待输入输出完成的时间占比
%idle: CPU空闲时间占比

若%iowait值过高，说明磁盘I/O存在瓶颈。
若%idle值过高，说明CPU较空闲。

* 显示磁盘分区信息，每2秒显示一次
> iostat -p 2
> iostat -p sda 2

<https://www.xaprb.com/blog/2010/01/09/how-linux-iostat-computes-its-results/>

### ioping

![ioping in action](https://www.opsdash.com/blog/images/disk-monitoring-ioping.gif)

### nmon

![enter image description here](https://i.stack.imgur.com/BJYjH.png)



<https://www.opsdash.com/blog/disk-monitoring-linux.html>

<https://askubuntu.com/questions/3561/how-do-i-monitor-disk-activity-on-a-specific-drive>

<https://www.networkworld.com/article/3330497/linux-commands-for-measuring-disk-activity.html>

<https://unix.stackexchange.com/questions/55212/how-can-i-monitor-disk-io>

<https://www.linuxtechi.com/monitor-linux-systems-performance-iostat-command/>

