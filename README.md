该脚本来源于 `glibc/script/build-many-glibcs`，本项目仅为对其进行 Github Workflow 封装

## Basic Info

该脚本的主要功能是构建glibc和交叉编译工具链。根据脚本中的代码，最终编译产物的位置可以通过以下参数进行配置：

- --prefix: 用于指定glibc安装的prefix，默认是/usr。

- --host-libraries-prefix: 用于指定主机库（如gmp、mpfr、mpc等）安装的prefix，默认是$(topdir)/install/host-libraries。

- --compiler-prefix: 用于指定交叉编译器安装的prefix，默认是$(topdir)/install/compilers。

- --glibc-prefix: 用于指定glibc安装的prefix，默认是$(topdir)/install/glibcs。

例如，如果你想要将glibc安装到/opt/glibc，可以将--glibc-prefix设置为/opt/glibc。如果你想要将交叉编译器安装到/opt/cross-compiler，可以将--compiler-prefix设置为/opt/cross-compiler。

具体来说，脚本会创建以下目录：

- $(topdir)/src: 源代码目录。
- $(topdir)/build: 构建目录。
- $(topdir)/install/host-libraries: 主机库的安装目录。
- $(topdir)/install/compilers: 交叉编译器的安装目录。
- $(topdir)/install/glibcs: glibc的安装目录。
通过修改上述参数，你可以自定义最终编译产物的位置。

## Target

选择想要编译的target主要取决于你的目标硬件平台和操作系统。这个脚本支持多种硬件平台和操作系统，包括常见的x86、ARM、MIPS等架构，以及Linux、GNU、Hurd等操作系统。

在脚本中，target通常是通过arch和os_name参数来指定的。例如：

arch='x86_64', os_name='linux-gnu' 表示x86_64架构的Linux系统。
arch='arm', os_name='linux-gnueabi' 表示ARM架构的EABI Linux系统。
arch='mips', os_name='linux-gnu' 表示MIPS架构的Linux系统。
arch='powerpc', os_name='linux-gnu' 表示PowerPC架构的Linux系统。

要选择你想要编译的target，你需要知道你的目标硬件平台和操作系统。一旦你知道了这些信息，你就可以在脚本中选择相应的arch和os_name参数。

例如，如果你想要编译一个用于ARM架构的EABI Linux系统的glibc，你应该这样指定：

arch='arm', os_name='linux-gnueabi'

 

如果你想要编译一个用于x86_64架构的Linux系统的glibc，你应该这样指定：

arch='x86_64', os_name='linux-gnu'

 

请注意，这个脚本还支持其他一些架构和操作系统，具体可以查看脚本中的add_config函数，以获取完整的支持列表。如果你想要编译的target不在列表中，你可能需要添加一个新的配置到脚本中。