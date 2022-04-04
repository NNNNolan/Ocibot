# Ocibot
基于NET6 oci-dotnet-sdk 多甲骨文IP切换tgbot

## 更新

1.添加webapi 支持第三方调用更换API

## 首先创建Bot配置文件夹
```
mkdir -p  /root/ocibotConfig/BotConfig
```

## 然后进BotConfig文件夹创建Bot.json 文件
```
{
  //你的TGID
  "BotAdminID": "",
  //socks or http 代理类型 值只有socks 或者http 不用代理可以不填
  "ProxyType": "",
  //代理地址 如果是Http类型需要添加http://ip
  //socks 只需要填写IP
  "ProxyHost": "",
  //代理端口
  "ProxyProt": "",
  //代理帐号 没有可不填
  "ProxyUser": "",
   //代理密码 
  "ProxyPwd": "",
  //TOGBOT token
  "BotToken": ""
}

```


## 首先创建oci配置文件夹 用于存放甲骨文API配置以及秘钥
```
mkdir -p  /root/ocibotConfig/OracleConfig
```
##OracleConfig  文件说明

###一个甲骨文帐号一个配置和秘钥存放在OracleConfig中 文件名称要以 `_config`结尾 如首尔_config
```
[DEFAULT]
user=xxx
fingerprint=xxxxx
tenancy=xxxxx
region=xxxx
key_file=./OracleConfig/秘钥文件.pem

```
###注意配置文件中的key_file=./OracleConfig/ 是不变的 只用修改秘钥名称

###bot启动是会读取以 `_config`结尾的的文件判断有多少个甲骨文帐号


## 配置完成后我们返回ocibotConfig 文件夹 拉取镜像启动bot即可
```
cd /root/ocibotConfig 
```
###arm需要将latest 更换为arm 即可
```
sudo docker run   --name ocibot   -p 6060:6060  -d  -v  "$(pwd)"/BotConfig:/app/BotConfig \
-v  "$(pwd)"/OracleConfig:/app/OracleConfig \
-it --privileged=true  nolanhzy/ocibot:latest
```



