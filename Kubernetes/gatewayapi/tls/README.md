## 快速开始
```text
kubectl apply -f .

本地配置hosts，打开网页验证
```

## 证书
```shell
# 生成私钥
openssl genrsa -out rsa.key 2048

# 生成 csr
openssl req -new -key rsa.key -out rsa.csr

# 生成证书
openssl x509 -req -days 365 -in rsa.csr -signkey rsa.key -out rsa.crt
```

## 参考文档
```text
// 自签证书
https://www.orcy.net.cn/340.html

```