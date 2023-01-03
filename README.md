# 适用于Realme X的Docker Linux内核（Test）  
如果在使用Docker或编译内核过程中出现问题，请在搜索引擎中寻找错误的解决方案，并向我们反馈   
## 反馈邮箱:
```
maox153@gmail.com
```

#依赖  
```bash  
apt update && apt upgrade -y  

apt install -y git libssl-dev gcc-arm-linux-gnueabi clang build-essential libncurses5-dev bzip2 make python-is-python3 gcc g++ grep bc curl bison flex openssl lzop ccache unzip libssl-dev zlib1g-dev ninja-build texinfo file ca-certificates ccache wget cmake texinfo ca-certificates zlib1g-dev xz-utils libelf-dev make python libssl-dev build-essential bc bison flex unzip libssl-dev ca-certificates xz-utils mkbootimg cpio device-tree-compiler binutils  

cd ~ && wget https://github.com/llvm/llvm-project/releases/download/llvmorg-13.0.0/clang+llvm-13.0.0-aarch64-linux-gnu.tar.xz && tar -xvf clang+llvm-13.0.0-aarch64-linux-gnu.tar.xz && rm -rf clang+llvm-13.0.0-aarch64-linux-gnu.tar.xz  
```  
