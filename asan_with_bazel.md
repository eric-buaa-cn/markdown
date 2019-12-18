![image-20191019170403767](/Users/eric/Library/Application Support/typora-user-images/image-20191019170403767.png)

https://www.phoronix.com/scan.php?page=news_item&px=MTIzOTU

https://www.usenix.org/sites/default/files/conference/protected-files/enigma_slides_serebryany.pdf

### step 1

Add this line to tools/bazel.rc:

build --copt -fsanitize=address

build --copt -fno-omit-frame-pointer

### step 2

Add -lasan to linkopts in BUILD.bazel，perhaps the -lasan should be the first one:

linkopts = ["-lasan", "-pthread", "-lssl", "-ldl", "-lz", "-lidn", "-lresolv"],

### step 3

Using ASAN_OPTIONS=detect_stack_use_after_return=1to report stack-use-after-return bugs:

ASAN_OPTIONS=detect_stack_use_after_return=1 bazel run :demo

### step 4

> umr.cc (uninitialized memory read)

```cpp
int main(int argc, char* argv[]) {
    int g_arr[100];
    g_arr[0] = 1;
    return g_arr[99];
}
```

clang++-6.0 umr.cc -fsanitize=memory -g

MSAN_SYMBOLIZER_PATH=/usr/lib/llvm-6.0/bin/llvm-symbolizer ./a.out

