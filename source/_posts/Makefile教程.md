---
title: Makefile教程
date: 2022-03-29 21:48:00
categories:
	-Linux

---

### Makefile简述

什么是 makefile？或许很多Winodws 的程序员都不知道这个东西，因为那些Windows 的IDE 都为你做了这个工作。一个全面的C语言程序员需要了解makefile ，特别在Unix 下的软件编译就自己写makefile 了，会不会写makefile，从一个侧面说明了一个人是否具备完成大型工程的能力。

一个项目的功能代码、头文件、依赖库可能存在与不同的路径下，并且很多时候不同模块之间也会存在依赖关系。Makefile就可以指定编译规则和编译顺序，实现项目的自动化编译，提高软件开发效率。在Makefile下甚至可以执行shell命令，同时Makefile遵循于IEEE 1003.2-1992 标准的（POSIX.2）。

一般来说，无论是C、C++、还是pas，首先要把源文件编译成中间代码文件，在Windows下也就是.obj 文件，UNIX 下是.o 文件，即Object File，这个动作叫做编译（compile）。然后再把大量的Object File 合成执行文件，这个动作叫作链接（link）。

编译时，编译器需要的是语法的正确，函数与变量的声明的正确。对于后者，通常是你需要告诉编译器头文件的所在位置（头文件中应该只是声明，而定义应该放在C/C++文件中），只要所有的语法正确，编译器就可以编译出中间目标文件。一般来说，每个源文件都应该对应于一个中间目标文件（O 文件或是OBJ 文件）。

链接时，主要是链接函数和全局变量，所以，我们可以使用这些中间目标文件（O 文件或是OBJ 文件）来链接我们的应用程序。链接器并不管函数所在的源文件，只管函数的中间目标文件（Object File），在大多数时候，由于源文件太多，编译生成的中间目标文件太多，而在链接时需要明显地指出中间目标文件名，这对于编译很不方便，所
以，我们要给中间目标文件打个包，在Windows 下这种包叫“库文件”（Library File)，也就是.lib 文件，在UNIX 下，是Archive File，也就是.a 文件。

### Makefile的主要内容

Makefile重要包含五部分内容：显式规则、隐晦规则、变量定义、文件指示和注释。

1、显式规则。显式规则说明了，如何生成一个或多的的目标文件。这是由Makefile 的书写者明显指出，要生成的文件，文件的依赖文件，生成的命令。

2、隐晦规则。由于我们的make 有自动推导的功能，所以隐晦的规则可以让我们比较粗糙地简略地书写Makefile，这是由make 所支持的。

3、变量的定义。在Makefile 中我们要定义一系列的变量，变量一般都是字符串，这个有点你C 语言中的宏，当Makefile 被执行时，其中的变量都会被扩展到相应的引用位置上。

4、文件指示。其包括了三个部分，一个是在一个Makefile 中引用另一个Makefile，就像C 语言中的include 一样；另一个是指根据某些情况指定Makefile 中的有效部分，就像C 语言中的预编译#if 一样；还有就是定义一个多行的命令。有关这一部分的内容，我会在后续的部分中讲述。

5、注释。Makefile 中只有行注释，和UNIX 的Shell脚本一样，其注释是用“#”字符，这个就像C/C++中的“//”一样。如果你要在你的Makefile 中使用“#”字符，可以用反斜框进行转义，如：“\#”。

需要注意的是如果Makefile的命令与target不在同一行，需要以[Tab]键开始。

### Makefile的命名

默认的情况下，make 命令会在当前目录下按顺序找寻文件名为“GNUmakefile”、“makefile”、“Makefile”的文件。在这三个文件名中，最好使用“Makefile”这个文件名，因为，这个文件名第一个字符为大写，这样有一种显目的感觉。最好不要用“GNUmakefile”，这个文件是GNU 的make 识别的。有另外一些make只对全小写的“makefile”文件名敏感，但是基本上来说，大多数的make 都支持“makefile”和“Makefile”这两种默认文件名。
当然，你可以使用别的文件名来书写Makefile，比如：“Make.Linux”，如果要指定特定的Makefile，你可
以使用make 的“-f”和“--file”参数，如：make -f Make.Linux 或make --file Make.Linux。

### Makefile的规则

关于Makefile编译的基本规则一般有以下几点：

1）如果这个工程没有编译过，那么我们的所有C 文件都要编译并被链接。

2）如果这个工程的某几个C 文件被修改，那么我们只编译被修改的C 文件，并链接目标程序。

3）如果这个工程的头文件被改变了，那么我们需要编译引用了这几个头文件的C 文件，并链接目标程序。

Makefile的编译规则的一般格式如下面的代码块所示，target是目标文件，也可以是Object File，也可以是执行文件。还可以是一个标签（Label），对于标签这种特性，在后续的“伪目标”章节中会有叙述。prerequisites 是生成那个target 所依赖的文件。command 是生成target需要执行的生成规则命令，也可以是任意的Shell 命令。

```
target ... : prerequisites ...
	command
	...
	...
```

举一个简单的例子：

```
#实例1
hello:main.o test.o
	gcc -o hello main.o test.o
main.o:main.c struct.h
	gcc -c main.c
test.o:test.c test.h struct.h
	gcc -c test.c
clean:
	rm hello main.o test.o 
```

当一行过长的时候，可以使用反斜杠换行符（\）。

### Makefile的工作流程

在默认的方式下，我们在项目路径下输入make 命令，Makefile的工作流程如下：

1、make 会在当前目录下找名字叫“Makefile”或“makefile”的文件。

2、如果找到，它会找文件中的第一个目标文件（target），在上面的例子中，他会找到“hello”这个文件，并把这个文件作为最终的目标文件。

3、如果hello文件不存在，或是hello所依赖的后面的.o 文件的文件修改时间要比edit 这个文件新，他就会执行后面所定义的命令来生成hello这个文件。

4、如果hello所依赖的.o 文件也存在，那么make 会在当前文件中找目标为.o 文件的依赖性，如果找到则再根据那一个规则生成.o 文件。（这有点像一个堆栈的过程）
5、当然，你的C 文件和H文件都存在，于是make 会生成.o 文件，然后再用.o 文件声明make 的最终任务，也就是生成执行文件hello了。

在寻找依赖的过程中，如果出现错误，例如被依赖的文件找不到，那么make 就会直接退出，并报错，对于是定义的错误，还是编译不成功的错误，make 根本不理。

在实例一种obj文件[*.o]的个数为两个，如果有很多个obj文件，就需要用变量记录，一般这个变量是OBJECTS,  OBJS，OBJ等等,当有新的.o文件需要加入，我们只要修改OBJ变量就可以了。

	#实例2
	OBJ = main.o test.o
	hello:$(OBJ)
	gcc -o hello $(OBJ)
	main.o:main.c struct.h
		gcc -c main.c
	test.o:test.c test.h struct.h
		gcc -c test.c
	clean:
		rm hello $(OBJ)

### Makefile的自动推导

make是一个很强大的工具，他可以根据依赖关系走动推导文件依赖和编译命令，于是我们不需要对每个[*.o]书写完全的命令，Makefile可以自动推导：只要make看到一个[.o]文件，他就会自动寻找响应的[.c]文件加入到依赖中。例如make看到test.o就会寻找test.c的依赖文件，同时推测gcc -c test.c的命令。因此实例2可以进一步优化：

```
#实例3
OBJ = main.o test.o
hello:$(OBJ)
gcc -o hello $(OBJ)
main.o:struct.h
test.o:test.h struct.h
.PHONY:clean
clean:
	rm hello $(OBJ)
```

这种方法就是make的隐晦规则，[.PHONY]表示clean是一个伪目标文件，不需要像上面的hello一样进行依赖查找。基于自动推导的方法，这个make还可以进一步简化，这种方法可以让依赖变得更简单，但是整体看起来很凌乱。

```
#实例3
OBJ = main.o test.o
hello:$(OBJ)
gcc -o hello $(OBJ)
$(OBJ):struct.h
test.o:test.h
.PHONY:clean
clean:
	rm hello $(OBJ)
```

关于清空目标文件的规则，我们也可以进行优化：在rm 命令前面加了一个减号，表示当某些文件出现问题的时候，不做处理继续运行。clean 的规则不要放在文件的开头，不然，这就会变成make 的默认目标，相信谁也不愿意这样。不成文的规矩是——clean从来都是放在文件的最后。

```
#实例4
...
...
clean:
	-rm hello $(OBJ)
```

### Makefile的引用另一个Makefile

在 Makefile 使用include 关键字可以把别的Makefile 包含进来，这很像C 语言的#include，被包含的文件会原模原样的放在当前文件的包含位置。include 的语法是：

```
include <filename>
```

filename 可以是当前操作系统Shell 的文件模式（可以保含路径和通配符）在 include 前面可以有一些空字符，但是绝不能是[Tab]键开始。include和\<filename>可以用一个或多个空格隔开。举个例子，你有这样几个Makefile：a.mk、b.mk、c.mk，还有一个文件叫foo.make，以及一个$(bar)，其包含了e.mk 和f.mk，那么，下面的语句：

```
include foo.make *.mk $(bar)
```

等价于：

```
include foo.make a.mk b.mk c.mk e.mk f.mk
```

make 命令开始时，会寻找include 所指出的其它Makefile文件，并把其内容安置在当前的位置。就好像C/C++的#include 指令一样。如果文件都没有指定绝对路径或是相对路径的话，make首先会在当前目录下寻找，如果当前目录下没有找到，那么，make 还会在下面的几个目录下找：

1、如果执行make命令时，有[-I]或[--include-dir]参数，那么make 就会在这个参数所指定的目录下去寻找。
2、如果目录\<prefix>/include（一般是：/usr/local/bin 或/usr/include）存在的话，make 也会去找。

如果有include的文件没有找到，make 会生成一条警告信息，但不会出现错误。它会继续载入其它的文件，一旦完成makefile 的读取，make 会再重试这些没有找到，或是不能读取的文件，如果还是不行，make 才会出现一条致命信息。如果你想让make 不理那些无法读取的文件，而继续执行，你可以在include 前加一个减号“-”。

```
-include foo.make a.mk b.mk c.mk e.mk f.mk
```

### Makefile的环境变量

如果你的当前环境中定义了环境变量MAKEFILES，那么，make 会把这个变量中的值做一个类似于include 的动作。这个变量中的值是其它的Makefile，用空格分隔。只是，它和include 不同的是，从这个环境变中引入的Makefile 的“目标”不会起作用，如果环境变量中定义的文件发现错误，make 也会不理。
在这里我还是建议不要使用这个环境变量，因为只要这个变量一旦被定义，那么当你使用make 时，所有的Makefile 都会受到它的影响，这绝不是你想看到的。在这里提这个事，只是为了告诉大家，也许有时候你的Makefile 出现了怪事，那么你可以看看当前环境中有没有定义这个变量。

### makefile项目的编译过程

GNU 的make 工作时，一个项目中的整体执行步骤入下（想来其它的make 也是类似）：

1、读入所有的Makefile。

2、读入被include 的其它Makefile。

3、初始化文件中的变量。

4、推导隐晦规则，并分析所有规则。

5、为所有的目标文件创建依赖关系链。

6、根据依赖关系，决定哪些目标要重新生成。

7、执行生成命令。

1-5 步为第一个阶段，6-7 为第二个阶段。第一个阶段中，如果定义的变量被使用了，那么，make 会把其展开在使用的位置。但make并不会完全马上展开，make 使用的是拖延战术，如果变量出现在依赖关系的规则中，那么仅当这条依赖被决定要使用了，变量才会在其内部展开。

### Makefile中的通配符

[~]	 如果是“~/test”，这就表示当前用户的$HOME 目录下的test 目录.

[\*]	[\*.c]表示所以后缀为c 的文件,[\\\*]来表示真实的\*字符.需要特别注意的是，[\*.o]的值不会展开，这一点与shell是不一样的。例如;

```
objects = *.o
```

objects 的值就是“\*.o”，不能展开成多个[.o]的文件名的集合。如果你想要objects中的值展开成文件名的集合，需要执行以下命令:

```
objects := $(wildcard *.o)
```

[$?]	显示最后命令的退出状态，0表示没有错误，其他表示有错误

### Makefile指定源文件路径-vpath

在一些大的工程中，有大量的源文件，我们通常的做法是把这许多的源文件分类，并存放在不同的目录中。所以，当make 需要去找寻文件的依赖关系时，你可以在文件前加上路径，但最好的方法是把一个路径告诉make，让make 在自动去找。

Makefile 文件中的特殊变量“VPATH”就是完成这个功能的，如果没有指明这个变量，make 只会在当前的目录中去找寻依赖文件和目标文件。如果定义了这个变量，那么，make 就会在当当前目录找不到的情况下，到所指定的目录中去找寻文件了。

```
VPATH = src:../headers
```


上面的的定义指定两个目录，“src”和“../headers”，make 会按照这个顺序进行搜索。目录由“冒号”分隔。（当然，当前目录永远是最高优先搜索的地方）。

另一个设置文件搜索路径的方法是使用make的“vpath”关键字（注意，它是全小写的），这不是变量，这是一个make 的关键字，这和上面提到的那个VPATH 变量很类似，但是它更为灵活。它可以指定不同的文件在不同的搜索目录中。这是一个很灵活的功能。它的使用方法有三种：

1、为符合模式\<pattern>的文件指定搜索目录\<directories>。

```
vpath <pattern> <directories>
```

2、清除符合模式\<pattern>的文件的搜索目录。

```
vpath <pattern>
```

3、清除所有已被设置好了的文件搜索目录。

```
vpath
```

vapth使用方法中的\<pattern>需要包含“%”字符。“%”的意思是匹配零或若干字符，例如，“%.h”表示所有以“.h”结尾的文件。\<pattern>指定了要搜索的文件集，而\<directories>则指定了\<pattern>的文件集的搜索的目录。例如：

该语句表示，要求make 在“../headers”目录下搜索所有以“.h”结尾的文

```
vpath %.h ../headers
```

该语句表示，要求make 在“../headers”目录下搜索所有以“.h”结尾的文件（如果某文件在当前目录没有找到的话）.

我们可以连续地使用vpath语句，以指定不同搜索策略。如果连续的vpath 语句中出现了相同的\<pattern>，或是被重复了的\<pattern>，那么，make 会按照vpath 语句的先后顺序来执行搜索。如：

其表示“.c”结尾的文件，先在“foo”目录，然后是“blish”，最后是“bar”
目录。
vpath %.c foo:bar
vpath % blish
而上面的语句则表示“.c”结尾的文件，先在“foo”目录，然后是“bar”
目录，最后才是“blish”目录。

```
vpath %.c foo
vpath % blish
vpath %.c bar
```

其表示“.c”结尾的文件，先在“foo”目录，然后是“blish”，最后是“bar”目录。

而上面的语句则表示“.c”结尾的文件，先在“foo”目录，然后是“bar”
目录，最后才是“blish”目录。

```
vpath %.c foo:bar
vpath % blish
```

而上面的语句则表示“.c”结尾的文件，先在“foo”目录，然后是“bar”目录，最后才是“blish”目录。

### Makefile中的伪目标

正像我们前面例子中的“clean”一样，即然我们生成了许多文件编译文件，我们也应该提供一个清除它们的“目标”以备完整地重编译而用。因为，我们并不生成“clean”这个文件。“伪目标”并不是一个文件，只是一个标签，由于“伪目标”不是文件，所以make 无法生成它的依赖关系和决定它是否要执行。我们只有通过显示地指明这个“目标”才能
让其生效。当然，“伪目标”的取名不能和文件名重名，不然其就失去了“伪目标”的意义了。当然，为了避免和文件重名的这种情况，我们可以使用一个特殊的标记“.PHONY”来显示地指明一个目标是“伪目标”，向make 说明，不管
是否有这个文件，这个目标就是“伪目标”。

```
.PHONY: clean
clean:
	rm *.o hello
```

伪目标一般没有依赖的文件。但是，我们也可以为伪目标指定所依赖的文件。伪目标同样可以作为“默认目标”放在第一个。举例来说如果你的Makefile 需要一口气生成若干个可执行文件，但你只想简单地敲一个make 完事，并且，所有的目标文件都写在一个Makefile 中，那么你可以使用“伪目标”这个特性。

```
all : prog1 prog2 prog3
.PHONY : all

prog1 : prog1.o utils.o
	gcc -o prog1 prog1.o utils.o

prog2 : prog2.o
	gcc -o prog2 prog2.o

prog3 : prog3.o sort.o utils.o
	gcc -o prog3 prog3.o sort.o utils.o
```

随便提一句，从上面的例子我们可以看出，目标也可以成为依赖。所以，伪目标同样也可成为依赖。看下面的例子：

```
.PHONY: cleanall cleanobj cleandiff
cleanall : cleanobj cleandiff
	rm program
cleanobj :
	rm *.o
cleandiff :
	rm *.diff
```

“make clean”将清除所有要被清除的文件。“cleanobj”和“cleandiff”这两个伪目标有点像“子程序”的意思。我们可以输入“make cleanall”和“make cleanobj”和“make cleandiff”命令来达到清除不同种类文件的目的。

### Makefile的多目标

Makefile 的规则中的目标可以不止一个，其支持多目标，有可能我们的多个目标同时依赖于一个文件，并且其生成的命令大体类似。于是我们就能把其合并起来。当然，多个目标的生成规则的执行命令是同一个，这可能会可我们带来麻烦，不过好在我们的可以使用一个自动化变量“$@”（关于自动化变量，将在后面讲述），这个变量表示着目前规则中所有的目标的集合，这样说可能很抽象，还是看一个例子吧。

```
bigoutput littleoutput : text.g
	generate text.g -$(subst output,,$@) > $@
```

上述规则等价于：

```
bigoutput : text.g
	generate text.g -big > bigoutput
littleoutput : text.g
	generate text.g -little > littleoutput
```

其中，-$(subst output,,$@)中的“$”表示执行一个Makefile 的函数，函数名为subst，后面的为参数。关于函数，将在后面讲述。这里的这个函数是截取字符串的意思，“$@”表示目标的集合，就像一个数组，“$@”依次取出目标，并执于命令。

### Makefile的静态模式

静态模式可以更加容易地定义多目标的规则，可以让我们的规则变得更加的有弹性和灵活。我们还是先来看一下语法：

```
<targets ...>: <target-pattern>: <prereq-patterns ...>
<commands>
...
...
```

targets 定义了一系列的目标文件，可以有通配符。是目标的一个集合。

target-parrtern 是指明了targets 的模式，也就是的目标集模式。

prereq-parrterns 是目标的依赖模式，它对target-parrtern 形成的模式再进行一次依赖目标的定义。

这样描述这三个东西，可能还是没有说清楚，还是举个例子来说明一下吧。如果我们的\<target-parrtern>定义成“%.o”，意思是我们的\<target>集合中都是以“.o”结尾的，而如果我们的\<prereq-parrterns>定义成“%.c”，意思是对\<target-parrtern>所形成的目标集进行二次定义，其计算方法是，取\<target-parrtern>模式中的“%”（也就是去掉了[.o]这个结尾），并为其加上[.c]这个结尾，形成的新集合。看一个例子：

```
CC=gcc
all: $(objects)

$(objects): %.o: %.c
	$(CC) -c $(CFLAGS) $< -o $@
```

上面的例子中，指明了我们的目标从$object 中获取，“%.o”表明要所有以“.o”结尾的目标，也就是“foo.o bar.o”，也就是变量$object 集合的模式，而依赖模式“%.c”则取模式“%.o”的“%”，也就是“foo bar”，并为其加下“.c”的后缀，于是，我们的依赖目标就是“foo.c bar.c”。而命令中的“$<”和“$@”则是自动化变量，“$<”表示所有的依赖目标集（也就是“foo.c bar.c”），“$@”表示目标集（也就是“foo.o bar.o”）。于是，上面的规则展开后等价于下面的规则：

```
CC=gcc
foo.o : foo.c
	$(CC) -c $(CFLAGS) foo.c -o foo.o
bar.o : bar.c
	$(CC) -c $(CFLAGS) bar.c -o bar.o
```

试想，如果我们的“%.o”有几百个，那种我们只要用这种很简单的“静态模式规则”就可以写完一堆规则，实在是太有效率了。“静态模式规则”的用法很灵活，如果用得好，那会一个很强大的功能。再看一个例子：

```
CC=gcc
files = foo.elc bar.o lose.o
$(filter %.o,$(files)): %.o: %.c
	$(CC) -c $(CFLAGS) $< -o $@
$(filter %.elc,$(files)): %.elc: %.el
	emacs -f batch-byte-compile $<
```

$(filter %.o,$(files))表示调用Makefile 的filter 函数，过滤“$filter”集，只要其中模式为“%.o”的内容。其的它内容，我就不用多说了吧。这个例字展示了Makefile 中更大的弹性。

### Makefile自动生成依赖

在 Makefile 中，我们的依赖关系可能会需要包含一系列的头文件，比如，如果我们的main.c 中有一句“#include "defs.h"”，那么我们的依赖关系应该是：

```
main.o : main.c defs.h
```

但是，如果是一个比较大型的工程，你必需清楚哪些C 文件包含了哪些头文件，并且，你在加入或删除头文件时，也需要小心地修改Makefile，这是一个很没有维护性的工作。为了避免这种繁重而又容易出错的事情，我们可以使用C/C++编译的一个功能。大多数的C/C++编译器都支持一个“-M”的选项，即自动找寻源文件中包含的头文件，并生成一个依赖关系。例如，如果我们执行下面的命令：

```
cc -M main.c
```

其输出是：

```
main.o : main.c defs.h
```

于是由编译器自动生成的依赖关系，这样一来，你就不必再手动书写若干文件的依赖关系，而由编译器自动生成了。需要提醒一句的是，如果你使用GNU 的C/C++编译器，你得用“-MM”参数，不然，“-M”参数会把一些标准库的头文件也包含进来。

gcc -M main.c 的输出是：

```
main.o: main.c defs.h /usr/include/stdio.h /usr/include/features.h \
/usr/include/sys/cdefs.h /usr/include/gnu/stubs.h \
/usr/lib/gcc-lib/i486-suse-linux/2.95.3/include/stddef.h \
/usr/include/bits/types.h /usr/include/bits/pthreadtypes.h \
/usr/include/bits/sched.h /usr/include/libio.h \
/usr/include/_G_config.h /usr/include/wchar.h \
/usr/include/bits/wchar.h /usr/include/gconv.h \
/usr/lib/gcc-lib/i486-suse-linux/2.95.3/include/stdarg.h \
/usr/include/bits/stdio_lim.h
```

gcc -MM main.c 的输出则是：

```
main.o: main.c defs.h
```

那么，编译器的这个功能如何与我们的Makefile 联系在一起呢。因为这样一来，我们的Makefile也要根据这些源文件重新生成，让Makefile自已依赖于源文件？这个功能并不现实，不过我们可以有其它手段来迂回地实现这一功能。GNU 组织建议把编译器为每一个源文件的自动生成的依赖关系放到一个文件中，为每一个“name.c”的文件都生成一个“name.d”的Makefile 文件，[.d]文件中就存放对应[.c]文件的依赖关系。

于是，我们可以写出[.c]文件和[.d]文件的依赖关系，并让make 自动更新或自成[.d]文件，并把其包含在我们的主Makefile 中，这样，我们就可以自动化地生成每个文件的依赖关系了。

这里，我们给出了一个模式规则来产生[.d]文件：

```
%.d: %.c
@set -e; rm -f $@; \
$(CC) -M $(CPPFLAGS) $< > $@.$$$$; \
sed 's,\($*\)\.o[ :]*,\1.o $@ : ,g' < $@.$$$$ > $@; \
rm -f $@.$$$$
```

这个规则的意思是，所有的[.d]文件依赖于[.c]文件，“rm -f $@”的意思是删除所有的目标，也就是[.d]文件，第二行的意思是，为每个依赖文件“$<”，也就是[.c]文件生成依赖文件，“$@”表示模式“%.d”文件，如果有一个C 文件是name.c，那么“%”就是“name”，“$$$$”意为一个随机编号，第二行生成的文件有可能是“name.d.12345”，第三行使用sed 命令做了一个替换，关于sed 命令的用法请参看相关的使用文档。第四行就是删除临时文件。

总而言之，这个模式要做的事就是在编译器生成的依赖关系中加入[.d]文件的依赖，即把依赖关系：

```
main.o : main.c defs.h
```

转成：

```
main.o main.d : main.c defs.h
```

于是，我们的[.d]文件也会自动更新了，并会自动生成了，当然，你还可以在这个[.d]文件中加入的不只是依赖关系，包括生成的命令也可一并加入，让每个[.d]文件都包含一个完赖的规则。一旦我们完成这个工作，接下来，我们就要把这些自动生成的规则放进我们的主Makefile 中。我们可以使用Makefile 的“include”命令，来引入别的
Makefile 文件（前面讲过），例如：

```
sources = foo.c bar.c
include $(sources:.c=.d)
```


上述语句中的“$(sources:.c=.d)”中的“.c=.d”的意思是做一个替换，把变量$(sources)所有[.c]的字串都替换成[.d]，关于这个“替换”的内容，在后面我会有更为详细的讲述。当然，你得注意次序，因为include是按次来载入文件，最先载入的[.d]文件中的目标会成为默认目标。

### Makefile的命令

#### 书写命令

每条规则中的命令和操作系统Shell 的命令行是一致的。make 会一按顺序一条一条的执行命令，每条命令的开头必须以[Tab]键开头，除非，命令是紧跟在依赖规则后面的分号后的。在命令行之间中的空格或是空行会被忽略，但是如果该空格或空行是以Tab 键开头的，那么make会认为其是一个空命令。
我们在UNIX 下可能会使用不同的Shell，但是make 的命令默认是被“/bin/sh”——UNIX 的标准Shell解释执行的。除非你特别指定一个其它的Shell。Makefile 中，“#”是注释符，很像C/C++中的“//”，其后的本行字符都被注释。

#### 显示命令

通常，make 会把其要执行的命令行在命令执行前输出到屏幕上。当我们用“@”字符在命令行前，那么，这个命令将不被make 显示出来，最具代表性的例子是，我们用这个功能来像屏幕显示一些信息。如：

```
@echo 正在编译XXX 模块......
```

如果 make 执行时，带入make 参数“-n”或“--just-print”，那么其只是显示命令，但不会执行命令，这个功能很有利于我们调试我们的Makefile，看看我们书写的命令是执行起来是什么样子的或是什么顺序的。

而make参数“-s”或“--slient”则是全面禁止命令的显示。

#### 命令执行

当依赖目标新于目标时，也就是当规则的目标需要被更新时，make会一条一条的执行其后的命令。需要注意的是，如果你要让上一条命令的结果应用在下一条命令时，你应该使用分号分隔这两条命令。比如你的第一条命令是cd 命令，你希望第二条命令得在cd 之后的基础上运行，那么你就不能把这两条命令写在两行上，而应该把这两条命令写在一行上，用分号分隔。如：

```
#示例一：
exec:
	cd /home/hchen
	pwd
#示例二：
exec:
	cd /home/hchen; pwd
```

当我们执行“make exec”时，第一个例子中的cd 没有作用，pwd 会打印出当前的Makefile 目录，而第二个例子中，cd 就起作用了，pwd会打印出“/home/hchen”。

make一般是使用环境变量SHELL中所定义的系统Shell来执行命令，默认情况下使用UNIX 的标准Shell——/bin/sh 来执行命令。但在MS-DOS下有点特殊，因为MS-DOS 下没有SHELL环境变量，当然你也可以指定。如果你指定了UNIX 风格的目录形式，首先，make会在SHELL 所指定的路径中找寻命令解释器，如果找不到，其会在当前盘符中的当前目录中寻找，如果再找不到，其会在PATH环境变量中所定义的所有路径中寻找。MS-DOS 中，如果你定义的命令解释器没有找到，其会给你的命令解释器加上诸如“.exe”、“.com”、“.bat”、“.sh”等后缀。

#### 命令错误

每当命令运行完后，make 会检测每个命令的返回码，如果命令返回成功，那么make 会执行下一条命令，当规则中所有的命令成功返回后，这个规则就算是成功完成了。如果一个规则中的某个命令出错了（命令退出码非零），那么make 就会终止执行当前规则，这将有可能终止所有规则的执行。有些时候，命令的出错并不表示就是错误的。例如mkdir 命令，我们一定需要建立一个目录，如果目录不存在，那么mkdir 就成功执行，万事大吉，如果目录存在，那么就出错了。我们之所以使用mkdir 的意思就是一定要有这样的一个目录，于是我们就不希望mkdir 出错而终止规则的运行。为了做到这一点，忽略命令的出错，我们可以在Makefile 的命令行前加一个减号“-”（在Tab 键之后），标记为不管命令出不出错都认为是成功的。如：

```
clean:
	-rm -f *.o
```

还有一个全局的办法是，给make 加上“-i”或是“--ignore-errors”参数，那么，Makefile 中所有命令都会忽略错误。而如果一个规则是以“.IGNORE”作为目标的，那么这个规则中的所有命令将会忽略错误。这些是不同级别的防止命令出错的方法，你可以根据你的不同喜欢设置。还有一个要提一下的make 的参数的是“-k”或是“--keep-going”，这个参数的意思是，如果某规则中的命令出错了，那么就终目该规则的执行，但继续执行其它规则。
四、

#### 命令的嵌套执行

在一些大的工程中，我们会把我们不同模块或是不同功能的源文件放在不同的目录中，我们可以在每个目录中都书写一个该目录的Makefile，这有利于让我们的Makefile 变得更加地简洁，而不至于把所有的东西全部写在一个Makefile 中，这样会很难维护我们的Makefile，这个技术对于我们模块编译和分段编译有着非常大的好处。例如，我们有一个子目录叫subdir，这个目录下有个Makefile 文件，来指明了这个目录下文件的编译规则。那么我们总控的Makefile 可以这样书写：

```
subsystem:
cd subdir && $(MAKE)
```

其等价于：

```
subsystem:
$(MAKE) -C subdir
```

定义$(MAKE)宏变量的意思是，也许我们的make 需要一些参数，所以定义成一个变量比较利于维护。这两个例子的意思都是先进入“subdir”目录，然后执行make 命令。

我们把这个Makefile 叫做“总控Makefile”，总控Makefile 的变量可以传递到下级的Makefile 中（如果你显示的声明），但是不会覆盖下层的Makefile 中所定义的变量，除非指定了“-e”参数。

如果你要传递变量到下级Makefile 中，那么你可以使用这样的声明：

```
export <variable ...>
```

如果你不想让某些变量传递到下级Makefile 中，那么你可以这样声明：

```
unexport <variable ...>
```

如示例一：

```
export variable = value
```

其等价于：

```
variable = value
export variable
```

其等价于：

```
export variable := value
```

其等价于：

```
variable := value
export variable
```

示例二：

```
export variable += value
```

其等价于：

```
variable += value
export variable
```

如果你要传递所有的变量，那么，只要一个export 就行了。后面什么也不用跟，表示传递所有的变量。
需要注意的是，有两个变量，一个是SHELL，一个是MAKEFLAGS，这两个变量不管你是否export，其总是要传递到下层Makefile 中，特别是MAKEFILES 变量，其中包含了make 的参数信息，如果我们执行“总控Makefile”时有make 参数或是在上层Makefile 中定义了这个变量，那么MAKEFILES 变量将会是这些参数，并会传递到下层Makefile 中，这是一个系统级的环境变量。但是 make 命令中的有几个参数并不往下传递，它们是“-C”,“-f”,“-h”“-o”和“-W”（有关Makefile 参数的细节将在后面说明），如果你不想往下层传递参数，那么，你可以这样来：

```
subsystem:
cd subdir && $(MAKE) MAKEFLAGS=
```

还有一个在“ 嵌套执行”中比较有用的参数，“-w”或是“--print-directory”会在make 的过程中输出一些信息，让你看到目前的工作目录。比如， 如果我们的下级make 目录是“/home/hchen/gnu/make”，如果我们使用“make -w”来执行，那么当进入该目录时，我们会看到：

```
make: Entering directory `/home/hchen/gnu/make'.
```

而在完成下层make 后离开目录时，我们会看到：

```
make: Leaving directory `/home/hchen/gnu/make'
```

当你使用“-C”参数来指定make 下层Makefile 时，“-w”会被自动打开的。如果参数中有“-s”（“--slient”）或是“--no-print-directory”，那么，“-w”总是失效的。

### Makefile的变量

#### 变量基础

变量在声明时需要给予初值，而在使用时，需要给在变量名前加上“$”符号，但最好用小括号“（）”或是大括号“{}”把变量给包括起来。如果你要使用真实的“$”字符，那么你需要用“$$”来表示。

#### 变量中的变量

先看第一种方式，也就是简单的使用“=”号，在“=”左侧是变量，右侧是变量的值，右侧变量的值可以定义在文件的任何一处，也就是说，右侧中的变量不一定非要是已定义好的值，其也可以使用后面定义的值。如：

```
foo = $(bar)
bar = $(ugh)
ugh = Huh?
all:
	echo $(foo)
```

但这种形式也
有不好的地方，那就是递归定义，如：

```
CFLAGS = $(CFLAGS) -O
```

或：

```
A = $(B)
B = $(A)
```

这会让make 陷入无限的变量展开过程中去，当然，我们的make 是有能力检测这样的定义，并会报错。还有就是如果在变量中使用函数，那么，这种方式会让我们的make 运行时非常慢，更糟糕的是，他会
使用得两个make 的函数“wildcard”和“shell”发生不可预知的错误。

为了避免上面的这种方法，我们可以使用make 中的另一种用变量来定义变量的方法。这种方法使用的是“:=”操作符，如：

```
x := foo
y := $(x) bar
x := later
```

其等价于：

```
y := foo bar
x := later
```

值得一提的是，这种方法，前面的变量不能使用后面的变量，只能使用前面已定义好了的变量。如果是这样：

#### 高级变量

这里介绍两种变量的高级使用方法，第一种是变量值的替换。我们可以替换变量中的共有的部分，其格式是“$(var:a=b)”或是“${var:a=b}”，其意思是，把变量“var”中所有以“a”字串“结尾”的“a”替换成“b”字串。这里的“结尾”意思是“空格”或是“结束符”。
还是看一个示例吧：

```
foo := a.o b.o c.o
bar := $(foo:.o=.c)
```

所以我们的“$(bar)”的值就是“a.c b.c c.c”。

另外一种变量替换的技术是以“静态模式”（参见前面章节）定义的，
如：

```
foo := a.o b.o c.o
bar := $(foo:%.o=%.c)
```

这依赖于被替换字串中的有相同的模式，模式中必须包含一个“%”字符，这个例子同样让$(bar)变量的值为“a.c b.c c.c”。

第二种高级用法是——“把变量的值再当成变量”。先看一个例子：

```
x = y
y = z
a := $($(x))
```

在这个例子中，$(x)的值是“y”，所以$($(x))就是$(y)，于是$(a)的值就是“z”。（注意，是“x=y”，而不是“x=$(y)”）

使用“+=”操作符，可以模拟为下面的这种例子：

```
objects = main.o foo.o bar.o utils.o
objects := $(objects) another.o
```

所不同的是，用“+=”更为简洁。
如果变量之前没有定义过，那么，“+=”会自动变成“=”，如果前面有
变量定义，那么“+=”会继承于前次操作的赋值符。如果前一次的是
“:=”，那么“+=”会以“:=”作为其赋值符，如：

```
variable := value
variable += more
```

等价于：

```
variable := value
variable := $(variable) more
```

但如果是这种情况：

```
variable = value
variable += more
```

由于前次的赋值符是“=”，所以“+=”也会以“=”来做为赋值，那么岂不会发生变量的递补归定义，这是很不好的，所以make 会自动为我们解决这个问题，我们不必担心这个问题。

#### overwrite指示符

如果有变量是通常make 的命令行参数设置的，那么Makefile 中对这个变量的赋值会被忽略。如果你想在Makefile 中设置这类参数的值，那么，你可以使用“override”指示符。其语法是：

```
override <variable> = <value>
override <variable> := <value>
```

当然，你还可以追加：

```
override <variable> += <more text>
```

#### 环境变量

make 运行时的系统环境变量可以在make 开始运行时被载入到Makefile 文件中，但是如果Makefile 中已定义了这个变量，或是这个变量由make 命令行带入，那么系统的环境变量的值将被覆盖。（如果make 指定了“-e”参数，那么，系统环境变量将覆盖Makefile 中定义的变量）。
因此，如果我们在环境变量中设置了“CFLAGS”环境变量，那么我们就可以在所有的Makefile 中使用这个变量了。这对于我们使用统一的编译参数有比较大的好处。如果Makefile 中定义了CFLAGS，那么则会使用Makefile 中的这个变量，如果没有定义则使用系统环境变量的值，一个共性和个性的统一，很像“全局变量”和“局部变量”的特性。当 make 嵌套调用时（参见前面的“嵌套调用”章节），上层Makefile中定义的变量会以系统环境变量的方式传递到下层的Makefile 中。当然，默认情况下，只有通过命令行设置的变量会被传递。而定义在文件中的变量，如果要向下层Makefile 传递，则需要使用exprot 关键字来声明。（参见前面章节）当然，我并不推荐把许多的变量都定义在系统环境中，这样，在我们执行不用的Makefile 时，拥有的是同一套系统变量，这可能会带来更多的麻烦。

### Makefile中的函数

#### shell函数

shell函数也不像其它的函数。顾名思义，它的参数应该就是操作系统Shell 的命令。它和反引号“`”是相同的功能。这就是说，shell函数把执行操作系统命令后的输出作为函数返回。于是，我们可以用操作系统命令以及字符串处理命令awk，sed 等等命令来生成一个变量，如：

```
contents := $(shell cat foo)
files := $(shell echo *.c)
```

注意，这个函数会新生成一个Shell 程序来执行命令，所以你要注意其运行性能，如果你的Makefile 中有一些比较复杂的规则，并大量使用了这个函数，那么对于你的系统性能是有害的。特别是Makefile的隐晦的规则可能会让你的shell函数执行的次数比你想像的多得多。

### Makefile的规则检测

有时候，我们不想让我们的makefile 中的规则执行起来，我们只想检查一下我们的命令，或是执行的序列。于是我们可以使用make 命令的下述参数：
“-n”
“--just-print”
“--dry-run”
“--recon”
不执行参数，这些参数只是打印命令，不管目标是否更新，把规则和连带规则下的命令打印出来，但不执行，这些参数对于我们调试makefile 很有用处。
“-t”

“--touch”
这个参数的意思就是把目标文件的时间更新，但不更改目标文件。也就是说，make 假装编译目标，但不是真正的编译目标，只是把目标变成已编译过的状态。
“-q”
“--question”
这个参数的行为是找目标的意思，也就是说，如果目标存在，那么其什么也不会输出，当然也不会执行编译，如果目标不存在，其会打印出一条出错信息。
“-W \<file>”
“--what-if=\<file>”
“--assume-new=\<file>”
“--new-file=\<file>”

这个参数需要指定一个文件。一般是是源文件（或依赖文件），Make会根据规则推导来运行依赖于这个文件的命令，一般来说，可以和“-n”参数一同使用，来查看这个依赖文件所发生的规则命令。另外一个很有意思的用法是结合“-p”和“-v”来输出makefile 被执行时的信息（这个将在后面讲述）。

### Makefile的参数

下面列举了所有GNU make 3.80 版的参数定义。其它版本和产商的make 大同小异，不过其它产商的make 的具体参数还是请参考各自的产品文档。
“-b”
“-m”
这两个参数的作用是忽略和其它版本make 的兼容性。
“-B”
“--always-make”
认为所有的目标都需要更新（重编译）。
“-C \<dir>”
“--directory=\<dir>”

指定读取makefile 的目录。如果有多个“-C”参数，make 的解释是后面的路径以前面的作为相对路径，并以最后的目录作为被指定目录。如：“make –C ~hchen/test –C prog”等价于“make –C ~hchen/test/prog”。
“—debug[=\<options>]”

输出make 的调试信息。它有几种不同的级别可供选择，如果没有参数，那就是输出最简单的调试信息。下面是\<options>的取值：
a —— 也就是all，输出所有的调试信息。（会非常的多）
b —— 也就是basic，只输出简单的调试信息。即输出不需要重编译的目标。
v —— 也就是verbose，在b 选项的级别之上。输出的信息包括哪个makefile 被解析，不需要被重编译的依赖文件（或是依赖目标）等。
i —— 也就是implicit，输出所以的隐含规则。
j —— 也就是jobs，输出执行规则中命令的详细信息，如命令的PID、返回码等。
m —— 也就是makefile，输出make 读取makefile，更新makefile，
执行makefile 的信息。
“-d” 相当于“--debug=a”。
“-e”
“--environment-overrides”  指明环境变量的值覆盖makefile 中定义的变量的值。

“-f=\<file>”
“--file=\<file>”
“--makefile=\<file>”
指定需要执行的makefile。
“-h”
“--help”
显示帮助信息。
“-i”
“--ignore-errors”
在执行时忽略所有的错误。

“-I \<dir>”
“--include-dir=\<dir>”
指定一个被包含makefile 的搜索目标。可以使用多个“-I”参数来指定
多个目录。
“-j [\<jobsnum>]”
“--jobs[=\<jobsnum>]”
指同时运行命令的个数。如果没有这个参数，make 运行命令时能运
行多少就运行多少。如果有一个以上的“-j”参数，那么仅最后一个“-j”
才是有效的。（注意这个参数在MS-DOS 中是无用的）

“-k”
“--keep-going”
出错也不停止运行。如果生成一个目标失败了，那么依赖于其上的目
标就不会被执行了。
“-l <\load>”
“--load-average[=<load]”
“—max-load[=\<load>]”
指定 make 运行命令的负载。
“-n”
“--just-print”
“--dry-run”
“--recon”
仅输出执行过程中的命令序列，但并不执行。
“-o \<file>”
“--old-file=\<file>”
“--assume-old=\<file>”

不重新生成的指定的\<file>，即使这个目标的依赖文件新于它。
“-p”
“--print-data-base”
输出makefile 中的所有数据，包括所有的规则和变量。这个参数会让一个简单的makefile 都会输出一堆信息。如果你只是想输出信息而不想执行makefile，你可以使用“make -qp”命令。如果你想查看执行makefile 前的预设变量和规则，你可以使用“make –p –f /dev/null”。这个参数输出的信息会包含着你的makefile 文件的文件名和行号，所以，用这个参数来调试你的makefile 会是很有用的，特别是当你的环境变量很复杂的时候。

“-q”
“--question”
不运行命令，也不输出。仅仅是检查所指定的目标是否需要更新。如果是0 则说明要更新，如果是2 则说明有错误发生。
“-r”
“--no-builtin-rules”
禁止make 使用任何隐含规则。
“-R”
“--no-builtin-variabes”
禁止make 使用任何作用于变量上的隐含规则。

“-s”
“--silent”
“--quiet”
在命令运行时不输出命令的输出。
“-S”
“--no-keep-going”
“--stop”
取消“-k”选项的作用。因为有些时候，make 的选项是从环境变量
“MAKEFLAGS”中继承下来的。所以你可以在命令行中使用这个参数
来让环境变量中的“-k”选项失效。
“-t”
“--touch”
相当于UNIX 的touch命令，只是把目标的修改日期变成最新的，也
就是阻止生成目标的命令运行。
“-v”
“--version”
输出make 程序的版本、版权等关于make 的信息。

“-w”
“--print-directory”
输出运行makefile 之前和之后的信息。这个参数对于跟踪嵌套式调用
make 时很有用。
“--no-print-directory”
禁止“-w”选项。
“-W \<file>”
“--what-if=\<file>”
“--new-file=\<file>”
“--assume-file=\<file>”

假定目标\<file>需要更新，如果和“-n”选项使用，那么这个参数会输
出该目标更新时的运行动作。如果没有“-n”那么就像运行UNIX 的
“touch”命令一样，使得\<file>的修改时间为当前时间。
“--warn-undefined-variables”
只要make 发现有未定义的变量，那么就输出警告信息。

### Makefile的自动化变量

$@
表示规则中的目标文件集。在模式规则中，如果有多个目标，那么，"$@"就是匹配于目标中模式定义的集合。
$%
仅当目标是函数库文件中，表示规则中的目标成员名。例如，如果一个目标是"foo.a(bar.o)"，那么，"$%"就是"bar.o"，"$@"就是"foo.a"。如果目标不是函数库文件（Unix 下是[.a]，Windows 下是[.lib]），那么，其值为空。
$<
依赖目标中的第一个目标名字。如果依赖目标是以模式（即"%"）定义的，那么"$<"将是符合模式的一系列的文件集。注意，其是一个一个取出来的。

$?
所有比目标新的依赖目标的集合。以空格分隔。
$^
所有的依赖目标的集合。以空格分隔。如果在依赖目标中有多个重复的，那个这个变量会去除重复的依赖目标，只保留一份。
$+
这个变量很像"$^"，也是所有依赖目标的集合。只是它不去除重复的依赖目标。
$*

这个变量表示目标模式中"%"及其之前的部分。如果目标是"dir/a.foo.b"，并且目标的模式是"a.%.b"，那么，"$\*"的值就是"dir/a.foo"。这个变量对于构造有关联的文件名是比较有较。如果目标中没有模式的定义，那么"$\*"也就不能被推导出，但是，如果目标文件的后缀是make 所识别的，那么"$\*"就是除了后缀的那一部分。
例如：如果目标是"foo.c"，因为".c"是make 所能识别的后缀名，所以，"$\*"的值就是"foo"。这个特性是GNU make 的，很有可能不兼容于其它版本的make，所以，你应该尽量避免使用"$\*"，除非是在隐含规则或是静态模式中。如果目标中的后缀是make 所不能识别的，那么"$*"就是空值。

$(@D)
表示"$@"的目录部分（不以斜杠作为结尾），如果"$@"值是"dir/foo.o"，那么"$(@D)"就是"dir"，而如果"$@"中没有包含斜杠的话，其值就是"."（当前目录）。
$(@F)
表示"$@"的文件部分，如果"$@"值是"dir/foo.o"，那么"$(@F)"就是"foo.o"，"$(@F)"相当于函数"$(notdir $@)"。
"$(\*D)"
"$(\*F)"
和上面所述的同理，也是取文件的目录部分和文件部分。对于上面的那个例子，"$(\*D)"返回"dir"，而"$(\*F)"返回"foo"
"$(%D)"

"$(%F)"
分别表示了函数包文件成员的目录部分和文件部分。这对于形同
"archive(member)"形式的目标中的"member"中包含了不同的目录很
有用。
"$(<D)"
"$(<F)"
分别表示依赖文件的目录部分和文件部分。
"$(^D)"
"$(^F)"

分别表示所有依赖文件的目录部分和文件部分。（无相同的）
"$(+D)"
"$(+F)"
分别表示所有依赖文件的目录部分和文件部分。（可以有相同的）
"$(?D)"
"$(?F)"
分别表示被更新的依赖文件的目录部分和文件部分。最后想提醒一下的是，对于"$<"，为了避免产生不必要的麻烦，我们最好给$后面的那个特定字符都加上圆括号，比如，"$(< )"就要比"$<"要好一些。还得要注意的是，这些变量只使用在规则的命令中，而且一般都是"显式规则"和"静态模式规则"（参见前面"书写规则"一章）。其在隐含
规则中并没有意义。

### Makefile的函数库文件的成员

一个函数库文件由多个文件组成。你可以以如下格式指定函数库文件
及其组成：
archive(member)
这个不是一个命令，而一个目标和依赖的定义。一般来说，这种用法基本上就是为了"ar"命令来服务的。如：

```
foolib(hack.o) : hack.o
	ar cr foolib hack.o
```

如果要指定多个member，那就以空格分开，如：
foolib(hack.o kludge.o)
其等价于：
foolib(hack.o) foolib(kludge.o)

你还可以使用Shell的文件通配符来定义，如：
foolib(*.o)

### 致谢

最最后，我还想介绍一下make 程序的设计开发者。
首当其冲的是： Richard Stallman
开源软件的领袖和先驱，从来没有领过一天工资，从来没有使用过Windows 操作系统。对于他的事迹和他的软件以及他的思想，我无需说过多的话，相信大家对这个人并不比我陌生，这是他的主页：
http://www.stallman.org/ 。

第二位是：Roland McGrath
个人主页是：http://www.frob.com/~roland/ ，下面是他的一些事迹：
1） 合作编写了并维护GNU make。
2） 和 Thomas Bushnell一同编写了GNU Hurd。
3） 编写并维护着GNU C library。
4） 合作编写并维护着部分的GNU Emacs。

在此，向这两位开源项目的斗士致以最真切的敬意。