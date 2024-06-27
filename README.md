# ipmitool

ipmitool usage:
1. BMC(BaceBoard Management Controller)  
BMC通过IPMI（Intelligent Platform Management Interface）协议与网络进行通信，因此它需要一个管理IP地址来实现网络连接。管理员可以通过这个IP地址访问BMC的Web界面或使用命令行工具（如ipmitool）来管理服务器。  
2. 管理IP地址是服务器的BMC用于网络通信的IP地址。这个地址可以通过配置BMC来设定，通常使用ipmitool这个工具来进行配置

1. 机器状态
- 查看开关机状态
```bash
ipmitool -H (管理地址) -I lanplus -U (BMI登录名) -P (BMI密码) power status
```

- 开机
```bash
ipmitool -H (管理地址) -I lanplus -U (BMI登录名) -P (BMI密码) power on
```

- 关机
```bash
ipmitool -H (管理地址) -I lanplus -U (BMI登录名) -P (BMI密码) power off
```

- 重启
```bash
ipmitool -H (管理地址) -I lanplus -U (BMI登录名) -P (BMI密码) power reset
```

2. 用户设置
> 参数解释：
    - [ChannelNo] 字段是可选的，ChannoNo为1或者8；
    - BMC默认有2个用户：user id为1的匿名用户，user id为2的ADMIN用户；
    - <>字段为必选内容；
    - <privilege level>：2为user权限，3为Operator权限，4为Administrator权限；
- 添加用户
```bash 
ipmitool -H (BMC的管理IP地址) -I lanplus -U (BMC登录用户名) -P (BMC 登录用户名的密码) user list [ChannelNo]
```
- 增加用户
```bash 
ipmitool -H (BMC的管理IP地址) -I lanplus -U (BMC登录用户名) -P (BMC 登录用户名的密码) user set name <user id> <username>
```

- 设置密码
```bash 
impitool -H (BMC的管理IP地址) -I lanplus -U (BMC登录用户名) -P (BMC 登录用户名的密码) user set password <user_id> <password>
```

- 设置用户权限
```bash 
impitool -H (BMC的管理IP地址) -I lanplus -U (BMC登录用户名) -P (BMC 登录用户名的密码) user priv <user id> <privilege level> [ChannelNo]
```

- 启用/禁用用户
```bash 
impitool -H (BMC的管理IP地址) -I lanplus -U (BMC登录用户名) -P (BMC 登录用户名的密码) user enable\disable <user_id>
```

3. IP网络设置
> 说明：[ChannelNo] 字段是可选的，ChannoNo为1(Share Nic网络)或者8（BMC独立管理网络）；设置网络参数，必须首先设置**IP为静态**，然后再进行其他设置
- 查看网络信息
```bash 
ipmitool -H (BMC管理IP的地址) -I lanplus -U (BMC登录用户) -P (BMC登录密码) lan print [ChannoNo] 
```

- 修改IP为静态或者DHCP状态
```bash 
impitool -H (BMC管理IP的地址) -I lanplus -U (BMC登录用户) -P (BMC登录密码) lan set <ChannolNo> ipsrc <static/dhcp>
```

- 修改IP地址
```bash 
impitool -H (BMC管理IP的地址) -I lanplus -U (BMC登录用户) -P (BMC登录密码) lan set <ChannolNo> ipaddr <ipaddr>
```

- 修改子网掩码
```bash 
impitool -H (BMC管理IP的地址) -I lanplus -U (BMC登录用户) -P (BMC登录密码) lan set <ChannolNo> netmask <netmask>
```

- 修改默认网关
```bash 
impitool -H (BMC管理IP的地址) -I lanplus -U (BMC登录用户) -P (BMC登录密码) lan set <ChannolNo> defgw ipaddr <默认网关>
```

3. SOL功能 (不是SQL)
