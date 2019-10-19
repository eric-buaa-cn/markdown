### step 1

Add this line to tools/bazel.rc:

build --copt -fsanitize=address

### step 2

Add -lasan to linkopts in BUILD.bazel，perhaps the -lasan should be the first one:

linkopts = ["-lasan", "-pthread", "-lssl", "-ldl", "-lz", "-lidn", "-lresolv"],