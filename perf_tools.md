Linux Performance Analysis
uptime
dmesg | tail
vmstat 1
mpstat -P ALL 1
pidstat 1
iostat -xm 1
free -g
sar -n DEV 1
sar -n TCP,ETCP 1

<https://doris.incubator.apache.org/documentation/en/developer-guide/debug-tool.html#preparing>

<https://gperftools.github.io/gperftools/pprof_remote_servers.html>




### 场景一：内存泄露 & 内存错误
> ASan

### Linux Performance Tools: perf
> perf是Linux下的系统性能调优工具。
> <https://perf.wiki.kernel.org/index.php/Main_Page>
>
> <https://perf.wiki.kernel.org/index.php/Tutorial>
>
> 

```txt
perf list
perf list sw
perf list hw
perf list cache

perf stat command
perf top -a
perf top -e cpu-clock
perf record command
perf report
perf report --no-children -s dso,sym,srcline -g address
sudo perf script | ~/bin/FlameGraph/stackcollapse-perf.pl | ~/bin/FlameGraph/flamegraph.pl > mem_leak.svg
```

<http://sandsoftwaresound.net/perf/perf-tutorial-hot-spots/>

<https://computing.llnl.gov/tutorials/performance_tools/>

https://fenbf.github.io/AwesomePerfCpp/

http://146.229.165.181/portal/Upload/tutorials/perf.tool/PerfTool.pdf



stack collapse-perl.pl: <https://github.com/brendangregg/FlameGraph/blob/master/stackcollapse-perf.pl>

flamegraph.pl: <https://github.com/brendangregg/FlameGraph/blob/master/flamegraph.pl>



![image-20191228231930762](/Users/eric/Library/Application Support/typora-user-images/image-20191228231930762.png)



### ~~gprof~~

> g++ -std=c++11 -pg cpuload.cpp -o cpuload
> ./cpuload
> gprof cpuload
>
> gprof does not support profiling multi-threaded applications and also cannot profile shared libraries.

### ~~OProfile~~
> OProfile has some common with perf

### Valgrind
> for debugging and profiling
> valgrind with vgdb (valgrind gdb server)
> <https://memcheck.wordpress.com/>

#### memcheck
> Valgrind Memcheck is a tool that detects memory leaks and memory errors, such as:
> * Accesses memory it shouldn't (areas not yet allocated, areas that have been freed, areas past the end of heap blocks, inaccessible areas of the stack)
> * Uses uninitialised values in dangerous ways
> * Leaks memory
> * Does bad frees of heap blocks (double frees, mismatched frees)
> * Passes overlapping source and destination memory blocks to memcpy() and related functions

```txt
g++ -o xxx -g -Og --std=c++11 xxx.cpp
valgrind --leak-check=full --track-origins=yes ./xxx
```

#### cachegrind


#### massif
> heap profiler

### Google Performance Tools

https://github.com/ahorn/benchmarks/wiki/Profiling-with-google-perftools



```shell
#!/bin/bash

# build the program; For our demo program, we specify -DWITHGPERFTOOLS to enable the gperftools specific #ifdefs
g++ -std=c++11 -DWITHGPERFTOOLS -lprofiler -g ../cpuload.cpp -o cpuload

# run the program; generates the profiling data file (profile.log in our example)
./cpuload

# convert profile.log to callgrind compatible format
pprof --callgrind ./cpuload profile.log > profile.callgrind

# open profile.callgrind with kcachegrind
kcachegrind profile.callgrind
```



### gdb

> gdb a.out
>
> start
>
> Ctrl-x-a goes into TUI



### rr

> rr

### gcc asan
> g++ -o mem_leak -g --std=c++11 -fsanitize=address -fno-omit-frame-pointer mem_leak.cpp
> 

#### heaptrack
> <https://milianw.de/blog/heaptrack-a-heap-memory-profiler-for-linux.html>



<https://fenbf.github.io/AwesomePerfCpp/>

<http://sandsoftwaresound.net/perf/perf-tutorial-hot-spots/>

<http://icps.u-strasbg.fr/~bastoul/local_copies/lee.html>

<https://computing.llnl.gov/tutorials/performance_tools/>

<https://perf.wiki.kernel.org/index.php/Tutorial>



### nm

#### addr2line

### readelf

### objdump

