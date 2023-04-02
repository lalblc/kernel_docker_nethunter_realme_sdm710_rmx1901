## 适用于Realme X的Docker Linux内核（已停更）
    因为此内核的源码过旧，并且开启了所有内核选项，导致内核不稳定，所以内核停止维护，并且删除所有的Releases 

# 编译
温馨提示：编译机尽量使用Ubuntu 20.04以上或Kali，其他GNU/Linux均未测试
### 依赖：  
```bash  
apt update && apt upgrade -y  

apt install -y git libssl-dev gcc-arm-linux-gnueabi clang build-essential libncurses5-dev bzip2 make python-is-python3 gcc g++ grep bc curl bison flex openssl lzop ccache unzip libssl-dev zlib1g-dev ninja-build texinfo file ca-certificates ccache wget cmake texinfo ca-certificates zlib1g-dev xz-utils libelf-dev make python libssl-dev build-essential bc bison flex unzip libssl-dev ca-certificates xz-utils mkbootimg cpio device-tree-compiler binutils gcc-aarch64-linux-gnu  

cd ~ && wget https://github.com/llvm/llvm-project/releases/download/llvmorg-13.0.0/clang+llvm-13.0.0-aarch64-linux-gnu.tar.xz && tar -xvf clang+llvm-13.0.0-aarch64-linux-gnu.tar.xz && rm -rf clang+llvm-13.0.0-aarch64-linux-gnu.tar.xz  
```  
### 环境变量：  
```bash
export PATH=/root/clang+llvm-13.0.0-aarch64-linux-gnu/bin:$PATH  
export ARCH=arm64  
export SUBARCH=arm64  
export CROSS_COMPILE=aarch64-linux-gnu-  
export CROSS_COMPILE_ARM32=arm-linux-gnueabi-  
```
### 构建：  
```bash
make clean && make mrproper && rm -rf out && mkdir -p out

make O=out CC=clang-13 RMX1901_defconfig

make -j$(nproc --all) O=out CC=clang-13 ARCH=arm64 \
CROSS_COMPILE=aarch64-linux-gnu- \
CROSS_COMPILE_ARM32=arm-linux-gnueabi- \
AR=llvm-ar \
OBJDUMP=llvm-objdump \
STRIP=llvm-strip \
NM=llvm-nm \
2>&1 | tee error.log
```
最后在out/arch/arm64/boot下取得kernel（Image.gz-dtb）  

如果目录下没有kernel则说明编译时出现了错误，那么请查看kernel原始码目录的error.log找到报错部分并使用搜索引擎查找解决方案
