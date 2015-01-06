
# 使用 iptables 实现透明代理 (目前仅HTTP成功) #


## 目标： ##
我想在我的 OpenWrt 上用 iptables + cow 实现透明代理

## 一些前提： ##
OpenWrt IP地址: 192.168.1.1
cow监听: 0.0.0.0:8898
cow已配置正确，使用浏览器设置代理 192.168.1.1:8898 能正确的翻墙

## 实现过程： ##
使用的 iptables 命令：
```bash
iptables -t nat -A PREROUTING -p tcp –dport 80 -j DNAT –to 192.168.1.1:8898
iptables -t nat -A PREROUTING -p tcp –dport 443 -j DNAT –to 192.168.1.1:8898
```

## 命令解释： ##
一个数据包进入路由，将要被NAT的时候，如果它的目的端口是80(HTTP)或443(HTTPS)，将该包扔给192.168.1.1:8898
`-t nat` 要对nat表中的规则进行操作
`-A` 添加规则，相应的，要删除一条规则，应使用`-D`
`PREROUTING` 指定PREROUTING链，也就是在数据包进入路由之前触发规则
`-p tcp` 匹配TCP协议
`–dport 80` 匹配目的端口，相应的，如果要匹配源端口，应使用`–sport`
`-j DNAT` 指定行为，DNAT的意思是修改它的目的地址
`–to 192.168.1.1:8898` 扔给192.168.1.1:8898

## 结果： ##
访问HTTP网站时代理成功了，但是访问HTTPS网站时失败了

## 一个猜想： ##
可能是cow不支持证书，导致访问HTTPS网站失败