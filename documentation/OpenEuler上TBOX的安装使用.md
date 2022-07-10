# OpenEuler 上 TBOX 的安装使用

本篇文章是为了确保可在 openEuler 上进行 TBOX 的安装，并测试和使用其模块。

## TBOX 是什么

TBOX 是一个用 c 语言实现的跨平台开发库。其针对各个平台，封装了统一的接口，简化了各类开发过程中常用操作，使你在开发过程中，更加关注实际应用的开发，而不是把时间浪费在琐碎的接口兼容性上面，并且充分利用了各个平台独有的一些特性进行优化。

## 一、安装 TBOX

因为整个 tbox 项目都是由 xmake 这个跨平台的构建工具维护的。编译 tbox 源码，需要先安装 [xmake](https://github.com/xmake-io/xmake) 构建工具。

1.  安装 xmake

```bash
#直接使用脚本安装
bash <(curl -fsSL https://raw.githubusercontent.com/xmake-io/xmake/master/scripts/get.sh)Copy to clipboardErrorCopied

# 或者通过wget
bash <(wget https://raw.githubusercontent.com/xmake-io/xmake/master/scripts/get.sh -O -)
Copy to clipboardErrorCopied

#运行`xmake update`，确保为最新版本。
xmake update
```

2.  下载源码、编译。

```bash
git clone https://gitee.com/tboox/tbox.git
cd tbox
xmake
```

如果你想直接创建一个带有 tbox 的空工程模型，也可以直接执行 `xmake create -t console_box dir_name` 命令来快速集成和编译使用 tbox。

在 openEuler 上安装的过程中， TBOX 有几率出现编译问题。

```c
[ydyk@localhost ~]$ cd tbox/
[ydyk@localhost tbox]$ xmake
checking for platform ... linux
checking for architecture ... x86_64
……
checking for libc_strlcpy ... no
checking for libc_wcscasestr ... no
checking for libm_sincos ... ok
checking for posix_pthread_setaffinity_np ... ok
checking for libc_setjmp ... ok
checking for posix_open ... ok
checking for libm_fmod ... ok
checking for libc_strchr ... ok
checking for libc_fwrite ... ok
checking for libc_wcscat ... ok
checking for libc_memcmp ... ok
checking for wchar ... no
……
checking for libc_wcslcpy ... no
……
generating src/tbox/tbox.config.h.in ... ok
[  0%]: ccache compiling.release src/tbox/tbox.c
[  0%]: ccache compiling.release src/tbox/hash/adler32.c
……
[  0%]: ccache compiling.release src/tbox/math/impl/math.c
error: src/tbox/hash/../prefix/type.h:100:9: error: unknown type name ‘__WCHAR_TYPE__’
  100 | typedef __WCHAR_TYPE__              tb_wchar_t;
      |         ^~~~~~~~~~~~~~
src/tbox/hash/../prefix/type.h:157:9: error: unknown type name ‘__tb_volatile__’
  157 | typedef __tb_volatile__  __tb_aligned__(4) tb_int32_t   tb_atomic32_t;
      |         ^~~~~~~~~~~~~~~
src/tbox/hash/../prefix/type.h:157:41: error: expected declaration specifiers or ‘...’ before numeric constant
  157 | typedef __tb_volatile__  __tb_aligned__(4) tb_int32_t   tb_atomic32_t;
      |                                         ^
src/tbox/hash/../prefix/type.h:164:9: error: unknown type name ‘__tb_volatile__’
  164 | typedef __tb_volatile__ __tb_aligned__(8) tb_int64_t    tb_atomic64_t;
      |         ^~~~~~~~~~~~~~~
src/tbox/hash/../prefix/type.h:164:40: error: expected declaration specifiers or ‘...’ before numeric constant
  164 | typedef __tb_volatile__ __tb_aligned__(8) tb_int64_t    tb_atomic64_t;
      |                                        ^
src/tbox/hash/../prefix/type.h:169:9: error: unknown type name ‘tb_atomic64_t’
  169 | typedef tb_atomic64_t                                   tb_atomic_t;
  > in src/tbox/hash/adler32.c
```

如果遇到以上情况，可以重新下载 tbox 进行编译，或者运行 `xmake f -c` 后重新编译。

3.  运行测试

```c
[ydyk@localhost tbox]$ xmake run demo math_random
[demo]: time: 16, average: 800, range: 600 - 1000
[demo]: time: 15, average: 149, range: 100 - 200
[demo]: time: 15, average: 201, range: -600 - 1000
[demo]: time: 16, average: -200, range: -600 - 200
[demo]: time: 16, average: -400, range: -600 - -200
[demo]: time: 15, average: 0.499821, range: 0.000000 - 1.000000
[demo]: time: 17, average: 100.094902, range: 0.000000 - 200.000000
[demo]: time: 15, average: 100.011360, range: -200.000000 - 0.000000
[demo]: time: 16, average: 199.802993, range: -200.000000 - 200.000000
```

## 二、前置知识
本部分对于 TBOX 中比较具有特色的模块进行简单介绍。

**流库**：针对 http、file、socket、data 等流数据，实现统一接口进行读写，并且支持阻塞、非阻塞读写模式。支持中间增加多层 filter，实现流之间数据过滤和变换，实现边读取，内部边进行解压、编码转换、加密等操作，极大的减少了内存使用。在目前的版本当中，可以使用 coroutine 协程模式来实现异步 io 开发。

tbox 目前主要提供以下模块：

- `stream`：通用非阻塞流，用于单路阻塞、非阻塞 io 的处理。适用于通用数据流协议，功能强大，并且内置缓存，但是比较重量级
- `static_stream`：针对静态数据 buffer 优化的静态流，仅用于维护静态的数据 buffer，以及读写、解析操作，比较轻量，效率也更高

我们可以在其上挂接多路 filter，实现流之间数据过滤和变换。目前支持以下几种 filter：

1.  **zip_filter：gzip**、zlib 的压缩和解压缩过滤器
2.  **charset_filter**：字符集编码的过滤器
3.  **chunked_filter：http** chunked 编码的解码过滤器

还有**基于流的传输器**：

1.  **transfer**：基于两路 stream 的传输器，可以用于简单的 http 下载、上传、文件之间的复制等。

## 三、简单使用

这一部分简单介绍一下 stream 模块的使用

### 流的初始化操作

```c
//初始化http流
tb_stream_ref_t stream = tb_stream_init_from_url("https://mirrors.tuna.tsinghua.edu.cn/openeuler/openEuler-20.03-LTS-SP3/ISO/x86_64/openEuler-20.03-LTS-SP3-everything-debug-x86_64-dvd.iso");
//或者通过端口访问
tb_stream_ref_t stream = tb_stream_init_from_http("www.xxxx.com", 80, "/file?args=xxx",tb_false );
```

### 输入端-非阻塞读取模式

```c
if(stream){
    //阻塞打开流
    if(tb_stream_open(stream)){
        tb_byte_t_data[TB_STREAM_BLOCK_MAXN];
        
 //beof判断流是否读取结束     
        while(tb_stream_beof(stream)){
            //非阻塞读取流数据，real位实际读取到的大小，如果失败，则返回-1
            tb_long_t real = tb_stream_read(stream, data, TB_STREAM_BLOCK_MAXN);     

            
            if(!real){
                            //当前读取不到流数据，等待指定时间间隔后再读取
                real = tb_stream_wait(stream, TB_STREAM_WAITREAD, tb_stream_timeout(stream));
               
                //如果还是等待失败，返回-1，等待超时返回0，并对流进行结束读取处理
                tb_check_break(real > 0);
            }
            else if (real < 0) break;
        }
        tb_stream_clos(stream);
    }
    tb_stream_exit(stream);
}
```

### 输入端-非阻塞模式写入

```c
tb_long_t real real = tb_stream_writ(stream, data, size);
```

### 读取和解析

```c
//从数据流中，读取一个大端的16bits数值
tb_uint16_t value;
if (tb_stream_bread_u16_be(stream, &value))
{
    tb_trace_i("%x", value);
}
```

除此之外还支持大端读取、小端读取、本地端读取以及浮点、双精度数值的各端读取。

如果解析的数据量非常大，stream 内置的自动 cache 读写，可以充分优化 io 读写性能，在大量数值解析时候，减少频繁的文件读写操作。

以上只是简单介绍了使用方法，实际实现和使用中可以根据需求进行自定义流。

## 参阅

- [GitHub - tboox/tbox: 🎁 A glib-like multi-platform c library](https://github.com/tboox/tbox)
- [流库 - 《TBOX 1.5.x 使用教程》 - 书栈网 · BookStack](https://www.bookstack.cn/read/tboox-1.5.x/流库.md)
- [tbox 数据位操作接口的使用 (tboox.org)](https://tboox.org/cn/2016/08/12/bits-operation/)

