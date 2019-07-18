# JWT

## 简介

>JWT，全称是Json Web Token， 是JSON风格轻量级的授权和身份认证规范，可实现无状态、分布式的Web应用授权；官网：[官网：https://jwt.io](https://jwt.io)

## 数据格式

### JWT包含三个部分的内容

* Header：头部，通常头部有两部分信息
  * 声明类型，这里是JWT
  * 加密算法，自定义
  
  我们会对头部进行base64加密（可解密），得到第一部分数据

* Payload：载荷，就是有效数据，一般包含下面信息
  * 用户身份信息（注意，这里因为采用base64加密，可解密，因此不要存放敏感信息）
  * 注册声明：如token的签发时间，过期时间，签发人等
这部分也会采用base64加密，得到第二部分数据
* Signature：签名，是整个数据的认证信息。一般根据前两步的数据，再加上服务的的密钥（secret）（不要泄漏，最好周期性更换），通过加密算法生成。用于验证整个数据完整和可靠性