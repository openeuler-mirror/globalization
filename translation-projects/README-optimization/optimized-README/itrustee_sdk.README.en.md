iTrustee SDK
============

Getting Started
---------------
Before setup your own project, please download libboundscheck software for secure function library.

Decompress the openeuler-libboundscheck-master.zip package, then put this software to `thirdparty/open_source` path.

Ensure that the header file path is `thirdparty/open_source/libboundscheck/include`.

You can download this software at https://gitee.com/openeuler/libboundscheck.

Build demo project:

```sh
$ cd test/CA/helloworld/cloud
$ make
$ cd test/TA/helloworld/cloud
$ make
```


Copy build result CA executable file and TA binary(xxx.sec) to `/vendor/bin/`.

The path `/vendor/bin/` may be changed as your opinion, but make sure it’s consistent with the path defined in your TA's source code `/vendor/bin/teec_hello`.

For more details please refer "iTrustee SDK.chm".