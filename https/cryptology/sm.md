# 国密算法

国密即国家[密码局](https://www.oscca.gov.cn)认定的国产密码算法。国密的标准文档见此[密码行业标准](http://www.gmbz.org.cn/main/bzlb.html)。

2018年11月，我国SM2/3/9密码算法正式成为ISO/IEC国际标准，以正文形式随`ISO/IEC14888-3:2018`最新一版发布。

2020年1月1日，《中华人民共和国密码法》正式施行，要求我国关键信息基础设施使用[商用密码](https://sca.gov.cn/sca/zxfw/2016-11/18/content_1002410.shtml)保护,密码分为核心密码、普通密码和商用密码，实行分类管理。核心密码、普通密码用于保护国家秘密信息，属于国家秘密，由密码管理部门依法实行严格统一管理。<mark>商用密码用于保护不属于国家秘密的信息，公民、法人和其他组织均可依法使用商用密码保护网络与信息安全</mark>。

| 算法  | 类型       | 公开    |     |     | 使用场景                                                                                   |
| --- | -------- | ----- | --- | --- | -------------------------------------------------------------------------------------- |
| SM1 | 对称算法     | 算法不公开 |     |     | 采用该算法已经研制了系列芯片、智能IC卡、智能密码钥匙、加密卡、加密机等安全产品，广泛应用于电子政务、电子商务及国民经济的各个应用领域（包括国家政务通、警务通等重要领域）  |
| SM2 | 非对称算法    | 算法公开  |     |     |                                                                                        |
| SM3 | 摘要(哈希)算法 | 算法公开  |     |     |                                                                                        |
| SM4 | 对称算法     | 算法公开  |     |     |                                                                                        |
| SM7 | 对称算法     | 算法不公开 |     |     | SM7适用于非接触式IC卡，应用包括身份识别类应用(门禁卡、工作证、参赛证)，票务类应用(大型赛事门票、展会门票)，支付与通卡类应用（积分消费卡、校园一卡通、企业一卡通等） |
| SM9 | 非对称算法    | 算法公开  |     |     |                                                                                        |
| ZUC | 对称算法     | 算法公开  |     |     |                                                                                        |

国密SSL证书是采用我国自主研发的[sm2](https://acg.tv/sm2)公钥算法体系，支持[sm2](https://acg.tv/sm2)、[sm3](https://acg.tv/sm3)、[sm4](https://acg.tv/sm4)等国产密码算法及国密SSL安全协议。

## References

https://github.com/guanzhi/GmSSL

[SM2证书的鉴定方法](https://www.wosign.com/SM2/SM2_cert.htm)

[国密HTTPS云计算应用服务解决方案](https://www.bilibili.com/video/BV1hy4y1S7Q5?from=search&seid=10377569376221755024)
