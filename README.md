
# gscan-quic

一个 IP 可用性扫描工具

## 当前支持

- [x] QUIC
- [x] SNI
- [ ] TLS
- [ ] SOCKS4/SOCKS4A/SOCKS5
- [ ] PING

## 简单说明

因为支持多种类型的IP扫描, 所以 IP 段文件也是分开放的, 具体在 config.json 文件可以看到

**IP段文件格式如下：**
> (文件里除了注释符 # 以外, 最好不要出现其他特殊字符)

    #注释

    IPStart1-IPEnd1
    IPStart2-IPEnd2
    ...
    IPStartN-IPEndN

    # 下面几种都是支持的, 遇到错误IP格式是会跳过的
    # 但是一定是一行一个IP或一个IP段, 参考下面的格式

    1.9.23.0            
    1.9.23.0/24
    1.9.0.0/16
    
    1.9.22.0-1.9.23.0/24
    
    1.9.22.0/24-1.9.33.0/24
    
    1.9.22.0-255
    1.9.22.0-1.9.22.0
    1.9.22.0-1.9.22.255
    1.9.22.0-1.9.33.255

    1.9.22.111-1.9.22.111       会自动精简成1.9.22.111
    1.9.22.0/24-1.9.22.0/24     会自动精简成1.9.22.0/24

    # 支持 ipv6 格式

    2001:db8::1
    2001:db8::1/128

    # 支持 gop 的 "xxx","xxx" 和 goa 的 xxx|xxx 格式

    "1.9.22.0", "1.9.22.1","1.9.22.2",
    1.9.22.0|1.9.22.1|

    # IP段也是会自动去重的

    1.9.22.0-255
    1.9.0.0/16
    1.9.22.0-255
    1.9.22.0/24
    1.9.22.0-255
    1.9.22.0-1.9.22.100
    1.9.22.0-1.9.22.255
    1.9.0.0/16
    3.3.3.0/24
    3.3.0.0/16
    3.3.3.0-255
    1.1.1.0/24
    1.9.0.0/16

    # 上面几个经过去重只会留下
    3.3.0.0/16
    1.9.0.0/16
    1.1.1.0/24

> **注意:**

* 默认是有输出个数限制的, 可以设置配置文件里的 RecordLimit

* 在扫描过程中是可以中断的, 只要按 <kbd>Ctrl</kbd>+<kbd>C</kbd> 就可以中断, 扫过的IP是会保留的

* 扫描IP段是随机的

## 配置说明

参考 config.json 文件

每次更新时最好覆盖掉 config.json 文件

支持 gop 形式的个人配置 config.user.json, 所以为了防止每次修改, 可以自己新建一个.

## 下载
到 https://github.com/Kisesy/gscan_quic/releases 下载编译好的

## 感谢

改自 yinqiwen 大神的 https://github.com/yinqiwen/gscan 在此感谢
