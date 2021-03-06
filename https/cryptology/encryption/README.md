# 加密算法

数据加密的基本思想是通过变换信息的表示形式来伪装需要保护的信息。
需要隐藏的信息称为明文，产生的结果称为密文，变换规则称为加密算法。
在明文转换为密文或将密文转换为明文的算法中输入的密码称为密钥。
根据加密算法所使用的加密密钥和解密密钥是否相同，分为对称加密和非对称加密。

| 特性    | 对称加密<br>Symmetric Cryptography | 非对称加密<br>Asymmetric Cryptography |
| ------- | --------------------------------- | ------------------------------------ |
| 加解密密码 | 同一个密码                       | 不同密码,即 公钥 和 私钥               |
| 加解密速度 | 速度快                           | 速度慢                               |
| 安全性     | 安全性低                         | 安全性高                             |
| 常见算法   | DES、AES、RC2、RC4、RC5          | RSA、DSA、ECDSA、ECC                 |