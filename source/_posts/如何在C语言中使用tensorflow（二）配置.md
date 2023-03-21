---
title: 如何在C语言中使用tensorflow（二）配置
date: 2020-05-09 11:38:00
categories:
	-AI工程化框架
---

本文主要介绍tensorflow的cpu版本的C语言使用方法。

###  一.硬件配置要求

1.libtensorflow的动态库对GCC版本有要求：

```
GCC > 5.0
```

2.libstdc++.so.6需要支持：    

```
GLIBCXX_3.4.20
GLIBCXX_3.4.21
CXXABI_1.3.8
```

libm.so.6需要支持：

```
GLIBC_2.23
```

### 二.硬件指令集要求（AVX指令集）：

cat /proc/cpuinfo，查看flags信息里面是否有包含AVX或者AVX2.

```
cat /proc/cpuinfo

processor	: 1
vendor_id	: GenuineIntel
cpu family	: 6
model		: 158
model name	: Intel(R) Core(TM) i5-8500 CPU @ 3.00GHz
stepping	: 10
microcode	: 0xb4
cpu MHz		: 3000.000
cache size	: 9216 KB
physical id	: 2
siblings	: 1
core id		: 0
cpu cores	: 1
apicid		: 2
initial apicid	: 2
fpu		: yes
fpu_exception	: yes
cpuid level	: 22
wp		: yes
flags		: fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ss syscall nx pdpe1gb rdtscp lm constant_tsc arch_perfmon nopl xtopology tsc_reliable nonstop_tsc eagerfpu pni pclmulqdq ssse3 fma cx16 pcid sse4_1 sse4_2 x2apic movbe popcnt aes xsave avx f16c rdrand hypervisor lahf_lm 3dnowprefetch ssbd ibrs ibpb stibp fsgsbase smep arat spec_ctrl intel_stibp flush_l1d arch_capabilities
bogomips	: 6000.00
clflush size	: 64
cache_alignment	: 64
address sizes	: 40 bits physical, 48 bits virtual
power management:
```


如果硬件包含AVX指令集，我们就可以使用1.15.0版本，如果不不包含AVX指令集，我们需要使用1.5.0版本。

下载地址如下：

1.5.0：

[https://storage.googleapis.com/tensorflow/libtensorflow/libtensorflow-cpu-linux-x86_64-1.5.0.tar.gz](https://storage.googleapis.com/tensorflow/libtensorflow/libtensorflow-cpu-linux-x86_64-1.5.0.tar.gz)

1.15.0：

[https://storage.googleapis.com/tensorflow/libtensorflow/libtensorflow-cpu-linux-x86_64-1.5.0.tar.gz](https://storage.googleapis.com/tensorflow/libtensorflow/libtensorflow-cpu-linux-x86_64-1.5.0.tar.gz)

将压缩包解压后，会得到一下路径

```
|--lib  #动态库
|--linclude   #头文件
```

加入以上文件加入到项目依赖当中。 