# 适用于Realme X的Docker Linux内核（Test）  
如果在使用Docker或编译内核过程中出现问题，请在搜索引擎中寻找错误的解决方案，并向我们反馈   
### 反馈邮箱:  
1. maox153@gmail.com  
2. 3616439505@qq.com  
3. 2234339463@qq.com  


# 编译
### 依赖  
```bash  
apt update && apt upgrade -y  

apt install -y git libssl-dev gcc-arm-linux-gnueabi clang build-essential libncurses5-dev bzip2 make python-is-python3 gcc g++ grep bc curl bison flex openssl lzop ccache unzip libssl-dev zlib1g-dev ninja-build texinfo file ca-certificates ccache wget cmake texinfo ca-certificates zlib1g-dev xz-utils libelf-dev make python libssl-dev build-essential bc bison flex unzip libssl-dev ca-certificates xz-utils mkbootimg cpio device-tree-compiler binutils gcc-aarch64-linux-gnu  

cd ~ && wget https://github.com/llvm/llvm-project/releases/download/llvmorg-13.0.0/clang+llvm-13.0.0-aarch64-linux-gnu.tar.xz && tar -xvf clang+llvm-13.0.0-aarch64-linux-gnu.tar.xz && rm -rf clang+llvm-13.0.0-aarch64-linux-gnu.tar.xz  
```  
### 环境变量
```bash
export PATH=/root/clang+llvm-13.0.0-aarch64-linux-gnu/bin:$PATH  
export ARCH=arm64  
export SUBARCH=arm64  
export CROSS_COMPILE=aarch64-linux-gnu-  
export CROSS_COMPILE_ARM32=arm-linux-gnueabi-  
```
### 构建
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
