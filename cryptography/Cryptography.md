# 密码学

## 对称密钥加密

对称密钥算法（Symmetric-key algorithm）又称为对称加密、私钥加密、共享密钥加密，是密码学中的一类加密算法。

常见的对称加密算法有DES、3DES、AES、Blowfish、IDEA、RC5、RC6。

对称加密的速度比公钥加密快很多，在很多场合都需要对称加密。

- DES
    - 数据加密标准（Data Encryption Standard，缩写为 DES）是一种对称密钥加密块密码算法。
    - DES是一个标准。使用的实际算法也称为DES或有时称为DEA（Data Encryption Algorithm，数字加密算法）。 
    - DES现在已经不是一种安全的加密方法，主要因为它使用的56位密钥过短。
- 3DES
    - 三重数据加密算法（Triple Data Encryption Algorithm，缩写为TDEA，Triple DEA），或称3DES（Triple DES），是一种对称密钥加密块密码，相当于是对每个数据块应用三次数据加密标准（DES）算法。
- AES
    - 高级加密标准（Advanced Encryption Standard，缩写：AES），在密码学中又称Rijndael加密法。
    
## 公钥加密（非对称加密）

公钥加密也称非对称加密是密码学的一种算法，它需要两个密钥，一个是公钥（公开），另一个是私钥（保密）
- 公钥用于加密，私钥用于解密 
- 私钥用于签名，公钥用于验证

常见的非对称加密算法有RSA、ElGamal、DH、ECC

## 散列函数

散列函数是可以用来将任意大小的数据映射到固定大小的数据的任何函数。散列函数返回的值称为散列值，散列码，摘要或简单的散列。

常用函数有：MD5 SHA-1 SHA-2 SHA-3 BLAKE2
 
## 数据签名

数字签名（Digital Signature，又称公钥数字签名）是一种类似写在纸上的普通的物理签名，但是使用了公钥加密领域的技术实现，用于鉴别数字信息的方法。

常见数据签名算法：
- 基于RSA的签名方案，例如RSA-PSS
- DSA及其椭圆曲线变体ECDSA

### DSA

数字签名算法（DSA）是用于数字签名的联邦信息处理标准。

### ECDSA

在密码学中，椭圆曲线数字签名算法（ECDSA）提供了使用椭圆曲线加密(ECC)的数字签名算法（DSA）的变体。

### ECC

椭圆曲线密码学（Elliptic Curve Cryptography，缩写：ECC）是一种基于椭圆曲线数学的公开密钥加密算法。

## 公钥加密标准

公钥加密标准（Public Key Cryptography Standards, PKCS），此一标准的设计与发布皆由RSA信息安全公司所制定。

| 标准 | 名称 |
| -------- | -------- |
| PKCS #1 | RSA密码编译标准（RSA Cryptography Standard） |
| PKCS #7 | 密码消息语法标准（Cryptographic Message Syntax Standard）|
| PKCS #8 | 私钥消息表示标准（Private-Key Information Syntax Standard）|
| PKCS #10 | 证书申请标准（Certification Request Standard） |
| PKCS #12 | 个人消息交换标准（Personal Information Exchange Syntax Standard） |

查看[公钥加密标准](https://zh.wikipedia.org/wiki/公钥密码学标准)

## 公钥证书（数字证书）

在密码学中，公钥证书（也称为数字证书或身份证书）是用于公开密钥基础建设的电子文件，用来证明公钥拥有者的身份。
此文件包含了公钥信息、拥有者身份信息（主体）、以及数字证书认证机构（发行者）对这份文件的数字签名，以保证这个文件的整体内容正确无误。

### 存储形式

电子证书可以二进制或Base64形式存储，常见的二进制文件扩展名有 .cer、.crt、.der，Base64的文件扩展名则通常是 .pem。如果把证书和私钥一起存储，则可以使用PKCS#12（.p12）格式。

## X.509

X.509 是密码学里公钥证书的格式标准。X.509证书用于许多Internet协议，包括TLS / SSL，它是HTTPS的基础。

### 证书文件扩展名

X.509有多种常用的扩展名。不过其中的一些还用于其它用途，就是说具有这个扩展名的文件可能并不是证书，比如说可能只是保存了私钥。

- .pem –（隐私增强型电子邮件）DER编码的证书再进行Base64编码的数据存放在"-----BEGIN CERTIFICATE-----"和"-----END CERTIFICATE-----"之中
- .cer, .crt, .der – 通常是DER二进制格式的，但Base64编码后也很常见。
- .p7b, .p7c – PKCS#7 SignedData structure without data, just certificate(s) or CRL(s)
- .p12 – PKCS#12格式，包含证书的同时可能还有带密码保护的私钥
- .pfx – PFX，PKCS#12之前的格式（通常用PKCS#12格式，比如那些由IIS产生的PFX文件）

PKCS#7 是签名或加密数据的格式标准，官方称之为容器。由于证书是可验真的签名数据，所以可以用SignedData结构表述。 .P7C文件是退化的SignedData结构，没有包括签名的数据。

PKCS#12 由PFX进化而来的用于交换公共的和私有的对象的标准格式。

### PEMWriter
```
@Test
public void test() throws Exception {
    KeyPair keyPair = KeyUtil.getRSAKeyPair();
    PrivateKey privateKey = keyPair.getPrivate();
    System.out.println(privateKey.getFormat());
    System.out.println(privateKey.getAlgorithm());

    StringWriter stringWriter = new StringWriter();
    JcaPEMWriter jcaPEMWriter = new JcaPEMWriter(stringWriter);
    jcaPEMWriter.writeObject(privateKey);
    jcaPEMWriter.close();
    String key1 = stringWriter.toString();
    System.out.println("key1：\n" + key1);

    JcaPKCS8Generator jcaPKCS8Generator = new JcaPKCS8Generator(privateKey, null);

    stringWriter = new StringWriter();
    jcaPEMWriter = new JcaPEMWriter(stringWriter);
    jcaPEMWriter.writeObject(jcaPKCS8Generator);
    jcaPEMWriter.close();
    String key2 = stringWriter.toString();
    System.out.println("key2：\n" + key2);

}
 
// 输出为
PKCS#8
RSA
key1：
-----BEGIN RSA PRIVATE KEY-----
MIIEowIBAAKCAQEAxWEynnIUmJ6fm1kft01+oj5Spq3D6pVSSnJKaciuWqUkKXYJ
7l7UPNmalIpEpMqXoYDBgrTcM2/XaFZzJZiNFl+Fz3EaSpl6X0T/9pBaIdBrFO14
ot7U4V3kIrQCoxttf/aWgsk1MiQlXnc2g2g0M3DM58BWENPxpt/kXCywmnsCbsio
0HDddGn2NC+rBzsDiA4OpP/B/y4yeI8I1FTwxNZqQ+DSSjMGj8V6GeL67/fGQalW
7of9WoYtuRmD6E07qq39FLbzbvSCqBNyE0Q/TfIXhtczDAoYZMNhTwHewbfohv1t
GTf5A7y0C+LWSBAYxtDS9hsWotffcaX74t05mQIDAQABAoIBAB6uyCNk2QpLmESa
M2m3iIC4nvkNqJfCHB96ClLM8Tuikc9HK+6L+8K00giWwOp8GtuujAZhTpzJXUs5
Kx+0SfRpJ4AylRN1LdZ6/65IzNYWU9sWOktZR+77vT/ey00nMZuzjbypghU4FL4N
WqJNU9YOSjAZkFd/1wAprFJe2Ro+UDCr//P1z4b3M8CJlxjFtMYH8kixqJ05fucR
JkoDnKFz06uzO+DyD+460GDQHBHxemG5UphcFe8K9cKHE3uQyDFO7YOcaE/IKEWJ
o+ck1ujVUKbnjy+DLjgHpfo+oRIYxpRAFgd19eJWF17Ij4GGzd5lnbeWhcmPJCDU
BFkT6g0CgYEA+944Xcg0QeCktX0U1S2Tu3ySK3fBXL5BBPqCgkSYsWh20yf57Nqt
vA+5xrq2VL6HhEdu+xPs3sYTeIceEuZr7fYbyCsneUrft+aZSL+zLg0omYnWEK2H
tb0X8CKyKlNB/VIVTucR/2bJkoQY97b4XuKAcGG25ONBlfx46cpNWW0CgYEAyJ4k
AzENCLb2jh98MPZZOcqMDkfZhE8KHBIXK8m3BGbyeWNOYOenZKOFRkl4YEKMs3OP
iq6bsKWgOeqg4qcFugfkrPlXy4BYtlWNwBhKFcpon4w8eoLJBw0QvXI6WbgfHxog
4cFMOvoIE5GNd2nKZyiObHzT4TxLPjuCagxxkV0CgYBctkQRYWy7AzIeDFjqz8gd
r5EupvpqZS4R4xS/VvjN9SIoQALjiOuC2lcMLBaJw0inDJRxn7gFmOv55eLQGjmI
cptvZ1M0drc7PosWGFqgjP9w5SgDI51c7KovHtZudg9IbDqjvLMHTJLOeAmoxZVP
eBjHRXDJeE3gI/tuM6WdUQKBgQCYriowN6N4z25Dadjllob/gZQnxizYEiNai7YQ
wDrGYecF1Tswav0tjXl/raiscdmNNVS4Mf0RamvPyC5bcMvd8eXqcvWLTgm18tSn
rpSrktkfG+ZnQqPl9t6Xn5ii8YrV69e8mJUAiYueAPdOOzgsXGRQUowabf3Bxh6R
wRipjQKBgDWsF0egI3V6hO/L8yRS9aJIgyjPyrnu+/hwhzq/CrdY2h4G+cd6kXzT
fWgvHgUGCAVFebCjcbgKFTuoovOFP/5T2c8FzDqs47lCP4ZHq03naULBfTAAAb0c
AwTaJMZR5wWdZHx6QnLHAHsACDL7GF9wsjumpk74IuD1pWLrLwXM
-----END RSA PRIVATE KEY-----

key2：
-----BEGIN PRIVATE KEY-----
MIIEvQIBADANBgkqhkiG9w0BAQEFAASCBKcwggSjAgEAAoIBAQDFYTKechSYnp+b
WR+3TX6iPlKmrcPqlVJKckppyK5apSQpdgnuXtQ82ZqUikSkypehgMGCtNwzb9do
VnMlmI0WX4XPcRpKmXpfRP/2kFoh0GsU7Xii3tThXeQitAKjG21/9paCyTUyJCVe
dzaDaDQzcMznwFYQ0/Gm3+RcLLCaewJuyKjQcN10afY0L6sHOwOIDg6k/8H/LjJ4
jwjUVPDE1mpD4NJKMwaPxXoZ4vrv98ZBqVbuh/1ahi25GYPoTTuqrf0UtvNu9IKo
E3ITRD9N8heG1zMMChhkw2FPAd7Bt+iG/W0ZN/kDvLQL4tZIEBjG0NL2Gxai199x
pfvi3TmZAgMBAAECggEAHq7II2TZCkuYRJozabeIgLie+Q2ol8IcH3oKUszxO6KR
z0cr7ov7wrTSCJbA6nwa266MBmFOnMldSzkrH7RJ9GkngDKVE3Ut1nr/rkjM1hZT
2xY6S1lH7vu9P97LTScxm7ONvKmCFTgUvg1aok1T1g5KMBmQV3/XACmsUl7ZGj5Q
MKv/8/XPhvczwImXGMW0xgfySLGonTl+5xEmSgOcoXPTq7M74PIP7jrQYNAcEfF6
YblSmFwV7wr1wocTe5DIMU7tg5xoT8goRYmj5yTW6NVQpuePL4MuOAel+j6hEhjG
lEAWB3X14lYXXsiPgYbN3mWdt5aFyY8kINQEWRPqDQKBgQD73jhdyDRB4KS1fRTV
LZO7fJIrd8FcvkEE+oKCRJixaHbTJ/ns2q28D7nGurZUvoeER277E+zexhN4hx4S
5mvt9hvIKyd5St+35plIv7MuDSiZidYQrYe1vRfwIrIqU0H9UhVO5xH/ZsmShBj3
tvhe4oBwYbbk40GV/Hjpyk1ZbQKBgQDIniQDMQ0ItvaOH3ww9lk5yowOR9mETwoc
EhcrybcEZvJ5Y05g56dko4VGSXhgQoyzc4+KrpuwpaA56qDipwW6B+Ss+VfLgFi2
VY3AGEoVymifjDx6gskHDRC9cjpZuB8fGiDhwUw6+ggTkY13acpnKI5sfNPhPEs+
O4JqDHGRXQKBgFy2RBFhbLsDMh4MWOrPyB2vkS6m+mplLhHjFL9W+M31IihAAuOI
64LaVwwsFonDSKcMlHGfuAWY6/nl4tAaOYhym29nUzR2tzs+ixYYWqCM/3DlKAMj
nVzsqi8e1m52D0hsOqO8swdMks54CajFlU94GMdFcMl4TeAj+24zpZ1RAoGBAJiu
KjA3o3jPbkNp2OWWhv+BlCfGLNgSI1qLthDAOsZh5wXVOzBq/S2NeX+tqKxx2Y01
VLgx/RFqa8/ILltwy93x5epy9YtOCbXy1KeulKuS2R8b5mdCo+X23pefmKLxitXr
17yYlQCJi54A9047OCxcZFBSjBpt/cHGHpHBGKmNAoGANawXR6AjdXqE78vzJFL1
okiDKM/Kue77+HCHOr8Kt1jaHgb5x3qRfNN9aC8eBQYIBUV5sKNxuAoVO6ii84U/
/lPZzwXMOqzjuUI/hkerTedpQsF9MAABvRwDBNokxlHnBZ1kfHpCcscAewAIMvsY
X3CyO6amTvgi4PWlYusvBcw=
-----END PRIVATE KEY-----
```

## 小结

以上内容均是网络内容摘录，参考地址如下：
- [Cryptography](https://en.wikipedia.org/wiki/Cryptography)
- [密码学](https://zh.wikipedia.org/wiki/密码学)
- [notes-on-cryptography-ciphers](https://rakhesh.com/infrastructure/notes-on-cryptography-ciphers-rsa-dsa-aes-rc4-ecc-ecdsa-sha-and-so-on/)