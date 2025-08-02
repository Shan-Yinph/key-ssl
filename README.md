# key-ssl

A cryptographic algorithm toolkit implemented in C++ with OpenSSL library! It implements several commonly used encryption algorithms, perfect for learning cryptography principles or adding encryption/decryption functionality to small projects.

## Core Features

- **Hash Algorithms**: MD5 and SHA256 digest hashing
- **Symmetric Encryption**: DES algorithm with ECB mode encryption/decryption
- **Asymmetric Encryption**: RSA algorithm (2048-bit keys) with key generation, public key encryption, and private key decryption
- **AES Support**: Header file definition for AES encryption class (256-bit, 192-bit, 128-bit)

## Technology Stack

- C++ language
- OpenSSL library
- Windows platform (can support Linux with configuration modifications)

## Installation Dependencies

### OpenSSL Library Installation Guide

#### Windows Platform

It is recommended to install OpenSSL using the vcpkg package manager. Follow these steps:

1. **Install vcpkg**

   ```bash
   # Clone the vcpkg repository
   git clone https://github.com/microsoft/vcpkg.git
   
   # Run the bootstrap script
   .\vcpkg\bootstrap-vcpkg.bat
   ```

2. **Install OpenSSL**

   ```bash
   # Install 32-bit version
   .\vcpkg\vcpkg install openssl:x86-windows
   
   # Install 64-bit version
   .\vcpkg\vcpkg install openssl:x64-windows
   ```

3. **Integrate with Project**

   ```bash
   # Global integration
   .\vcpkg\vcpkg integrate install
   ```

   After integration, Visual Studio will automatically recognize the OpenSSL library.

#### Linux Platform

```bash
# Ubuntu/Debian
sudo apt-get install libssl-dev

# CentOS/RHEL
sudo yum install openssl-devel
```

## Compilation Method

### Windows Platform

1. Open the `key-ssl.sln` solution with Visual Studio
2. Select the appropriate configuration (Debug/Release) and platform (x86/x64)
3. Click "Build" menu and select "Build Solution"

### Linux Platform

```bash
# Install build tools
sudo apt-get install build-essential

# Compile
g++ -std=c++11 -I/path/to/openssl/include -L/path/to/openssl/lib -lssl -lcrypto key-ssl.cpp -o key-ssl
```

## Usage Example

```cpp
// Example code snippet
#include <iostream>
#include "openssl/md5.h"
#include "openssl/sha.h"
#include "openssl/des.h"
#include "openssl/rsa.h"
#include "openssl/pem.h"
#include "aes.h"

int main() {
    // Original plaintext
    std::string srcText = "this is an example";
    std::string encryptText, decryptText, encryptHexText;

    // MD5 hash example
    md5(srcText, encryptText, encryptHexText);
    std::cout << "MD5 hash result: " << encryptHexText << std::endl;

    // DES encryption example
    std::string desKey = "Shiny Space 666";
    encryptText = des_encrypt(srcText, desKey);
    decryptText = des_decrypt(encryptText, desKey);
    std::cout << "DES decryption result: " << decryptText << std::endl;

    // RSA encryption/decryption example
    std::string key[2];
    generateRSAKey(key);
    encryptText = rsa_pub_encrypt(srcText, key[0]);
    decryptText = rsa_pri_decrypt(encryptText, key[1]);
    std::cout << "RSA decryption result: " << decryptText << std::endl;

    return 0;
}
```

## Project Structure

```
key-ssl/
├── .vs/                  # Visual Studio configuration files
├── .vscode/              # VS Code configuration files
├── aes.h                 # AES encryption class header
├── key-ssl.cpp           # Main program file
├── key-ssl.sln           # Visual Studio solution
├── key-ssl.vcxproj       # Visual Studio project file
├── prikey.pem            # Example private key file
├── pubkey.pem            # Example public key file
└── x64/                  # Compilation output directory
    └── Debug/            # Debug version output
        ├── key-ssl.exe   # Executable file
        └── libcrypto-3-x64.dll  # OpenSSL runtime library
```

## Keywords

Encryption algorithm, C++, OpenSSL, MD5, SHA256, DES, RSA, AES, Information Security, Cryptography

## Notes

1. The example key files (prikey.pem and pubkey.pem) are for testing purposes only. Please generate your own keys for actual applications.
2. Ensure the OpenSSL library path is correctly configured in your compilation environment.
3. This project uses OpenSSL version 3.x.
4. OpenSSL dynamic link libraries (such as libcrypto-3-x64.dll) are required during runtime.

## Contribution Guide

If you have any ideas or improvements, please feel free to submit Issues and Pull Requests to help improve this project!