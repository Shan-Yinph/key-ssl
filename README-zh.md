# key-ssl

一个基于C++和OpenSSL库实现的加密算法工具集！它实现了几种常用的加密算法，不管是学习加密原理，还是小项目里需要加解密功能，都可以用它来试试。

## 核心功能

- **哈希算法**：MD5、SHA256摘要哈希
- **对称加密**：DES算法ECB模式加解密
- **非对称加密**：RSA算法(2048位密钥)的密钥生成、公钥加密和私钥解密
- **AES支持**：提供AES加密类的头文件定义(256位、192位、128位)

## 技术栈

- C++语言
- OpenSSL库
- Windows平台(可通过修改配置支持Linux)

## 安装依赖

### OpenSSL库安装指南

#### Windows 平台

推荐使用vcpkg包管理器安装OpenSSL，步骤如下：

1. **安装vcpkg**

   ```bash
   # 克隆vcpkg仓库
   git clone https://github.com/microsoft/vcpkg.git
   
   # 运行引导脚本
   .\vcpkg\bootstrap-vcpkg.bat
   ```

2. **安装OpenSSL**

   ```bash
   # 安装32位版本
   .\vcpkg\vcpkg install openssl:x86-windows
   
   # 安装64位版本
   .\vcpkg\vcpkg install openssl:x64-windows
   ```

3. **集成到项目**

   ```bash
   # 全局集成
   .\vcpkg\vcpkg integrate install
   ```

   集成后，Visual Studio会自动识别OpenSSL库。

#### Linux 平台

```bash
# Ubuntu/Debian
sudo apt-get install libssl-dev

# CentOS/RHEL
sudo yum install openssl-devel
```

## 编译方法

### Windows 平台

1. 使用Visual Studio打开`key-ssl.sln`解决方案
2. 选择适当的配置(Debug/Release)和平台(x86/x64)
3. 点击"生成"菜单中的"生成解决方案"

### Linux 平台

```bash
# 安装编译工具
sudo apt-get install build-essential

# 编译
g++ -std=c++11 -I/path/to/openssl/include -L/path/to/openssl/lib -lssl -lcrypto key-ssl.cpp -o key-ssl
```

## 使用示例

```cpp
// 示例代码片段
#include <iostream>
#include "openssl/md5.h"
#include "openssl/sha.h"
#include "openssl/des.h"
#include "openssl/rsa.h"
#include "openssl/pem.h"
#include "aes.h"

int main() {
    // 原始明文
    std::string srcText = "this is an example";
    std::string encryptText, decryptText, encryptHexText;

    // MD5哈希示例
    md5(srcText, encryptText, encryptHexText);
    std::cout << "MD5哈希结果: " << encryptHexText << std::endl;

    // DES加密示例
    std::string desKey = "Shiny Space 666";
    encryptText = des_encrypt(srcText, desKey);
    decryptText = des_decrypt(encryptText, desKey);
    std::cout << "DES解密结果: " << decryptText << std::endl;

    // RSA加解密示例
    std::string key[2];
    generateRSAKey(key);
    encryptText = rsa_pub_encrypt(srcText, key[0]);
    decryptText = rsa_pri_decrypt(encryptText, key[1]);
    std::cout << "RSA解密结果: " << decryptText << std::endl;

    return 0;
}
```

## 项目结构

```
key-ssl/
├── .vs/                  # Visual Studio配置文件
├── .vscode/              # VS Code配置文件
├── aes.h                 # AES加密类头文件
├── key-ssl.cpp           # 主程序文件
├── key-ssl.sln           # Visual Studio解决方案
├── key-ssl.vcxproj       # Visual Studio项目文件
├── prikey.pem            # 示例私钥文件
├── pubkey.pem            # 示例公钥文件
└── x64/                  # 编译输出目录
    └── Debug/            # 调试版本输出
        ├── key-ssl.exe   # 可执行文件
        └── libcrypto-3-x64.dll  # OpenSSL运行时库
```

## 关键词

加密算法, C++, OpenSSL, MD5, SHA256, DES, RSA, AES, 信息安全, 密码学

## 注意事项

1. 示例密钥文件(prikey.pem和pubkey.pem)仅供测试使用，实际应用中请重新生成
2. 确保编译环境已正确配置OpenSSL库路径
3. 项目使用的OpenSSL版本为3.x
4. 运行时需要OpenSSL的动态链接库(如libcrypto-3-x64.dll)

## 贡献指南

如果你有好的想法或改进，欢迎提交Issue和Pull Request来一起完善这个项目！

## 感谢

衷心感谢 **YanJuan** 在本项目的构思与早期开发中提供的指导和技术支持。他的经验和见解为这个项目奠定了重要基础。

- [YanJuan](https://github.com/triangleXXX)