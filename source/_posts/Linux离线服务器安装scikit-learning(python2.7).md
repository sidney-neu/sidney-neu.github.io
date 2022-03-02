---
title: Linux离线服务器安装scikit-learning(python2.7)
date: 2018-10-19 17:20:00
categories:
	-Linux
	-others
---

1.提前下载pip

[https://files.pythonhosted.org/packages/93/ab/f86b61bef7ab14909bd7ec3cd2178feb0a1c86d451bc9bccd5a1aedcde5f/pip-19.1.1.tar.gz](https://files.pythonhosted.org/packages/93/ab/f86b61bef7ab14909bd7ec3cd2178feb0a1c86d451bc9bccd5a1aedcde5f/pip-19.1.1.tar.gz)

2.将pip传输到Linux服务器并解压：

```
tar zxf pip-19.1.1.tar.gz
cd pip-19.1.1
python setup.py install
```


3.使用wheel安装。如果没有wheel需要事先安装，安装方法与pip相同

[https://files.pythonhosted.org/packages/1d/b0/f478e80aeace42fe251225a86752799174a94314c4a80ebfc5bf0ab1153a/wheel-0.33.4.tar.gz](https://files.pythonhosted.org/packages/1d/b0/f478e80aeace42fe251225a86752799174a94314c4a80ebfc5bf0ab1153a/wheel-0.33.4.tar.gz)

4.确定下载对应的whl文件类型：

```
python
import pip._internal
print(pip._internal.pep425tags.get_supported())
[('cp27', 'cp27m', 'manylinux1_x86_64'), ('cp27', 'cp27m', 'linux_x86_64'), ('cp27', 'none', 'manylinux1_x86_64'), ('cp27', 'none', 'linux_x86_64'), ('py2', 'none', 'manylinux1_x86_64'), ('py2', 'none', 'linux_x86_64'), ('cp27', 'none', 'any'), ('cp2', 'none', 'any'), ('py27', 'none', 'any'), ('py2', 'none', 'any'), ('py26', 'none', 'any'), ('py25', 'none', 'any'), ('py24', 'none', 'any'), ('py23', 'none', 'any'), ('py22', 'none', 'any'), ('py21', 'none', 'any'), ('py20', 'none', 'any')]
```

或者

```
import pip; 
print(pip.pep425tags.get_supported())
```


根据上面的显示('cp27', 'cp27m', 'manylinux1_x86_64')可以下载：

numpy-1.16.4-cp27-cp27m-manylinux1_x86_64.whl

[https://files.pythonhosted.org/packages/20/2c/4d64f1cd4d2170b91d24ae45725de837bd40c34c9c04c94255c0f51c513d/numpy-1.16.4-cp27-cp27m-manylinux1_x86_64.whl](https://files.pythonhosted.org/packages/20/2c/4d64f1cd4d2170b91d24ae45725de837bd40c34c9c04c94255c0f51c513d/numpy-1.16.4-cp27-cp27m-manylinux1_x86_64.whl)

scipy-1.2.0-cp27-cp27m-manylinux1_x86_64.whl

[https://files.pythonhosted.org/packages/2c/9a/8cfd681d4a970ff0174dcb93d16c70103c430c64264a9d9078c8abda2b9f/scipy-1.2.0-cp27-cp27m-manylinux1_x86_64.whl](https://files.pythonhosted.org/packages/2c/9a/8cfd681d4a970ff0174dcb93d16c70103c430c64264a9d9078c8abda2b9f/scipy-1.2.0-cp27-cp27m-manylinux1_x86_64.whl)

scikit_learn-0.20.3-cp27-cp27m-manylinux1_x86_64.whl

[https://files.pythonhosted.org/packages/43/70/9f689f629518b70d7000316faa7a58eac3029ad1ed2b3115a6e30f53797c/scikit_learn-0.20.3-cp27-cp27m-manylinux1_x86_64.whl](https://files.pythonhosted.org/packages/43/70/9f689f629518b70d7000316faa7a58eac3029ad1ed2b3115a6e30f53797c/scikit_learn-0.20.3-cp27-cp27m-manylinux1_x86_64.whl)

5.使用pip安装对应的whl文件

```
pip install numpy-1.16.4-cp27-cp27m-manylinux1_x86_64.whl
pip install scipy-1.2.0-cp27-cp27m-manylinux1_x86_64.whl
pip install scikit_learn-0.20.3-cp27-cp27m-manylinux1_x86_64.whl
```


安装完成。

测试程序

```
from sklearn import linear_model
reg = linear_model.RidgeCV(alphas=[0.1, 1.0, 10.0], cv=3)
reg.fit([[0, 0], [0, 0], [1, 1]], [0, .1, 1])
print reg.alpha_
```


如果输出结果则安装成功。

 

ps：如果有错误输出

```
***/python2.7/site-packages/sklearn/externals/joblib/_multiprocessing_helpers.py:38: UserWarning: [Errno 38] Function not implemented.  joblib will operate in serial mode
  warnings.warn('%s.  joblib will operate in serial mode' % (e,))
```

解决方法参考（https://www.boris.co/2012/02/server-ubuntu-11.html）：

在root用户下：

```
mkdir /dev/shm

vi /etc/fstab
在/etc/fstab的文件末尾添加：
tmpfs /dev/shm    tmpfs   defaults,noexec,nosuid     0     0
```

保存文件，然后从新挂载：

重新运行测试程序即可。

```
mount -a
```

重新运行测试程序即可。