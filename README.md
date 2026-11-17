# 华为 H1s-3 / H2-3 工具、地区配置包与教程存档

配套文章：[华为 H1s-3 / H2-3 光猫：开 Telnet、改地区与 SN](https://xiaozou123.cn/huawei-h1s3-h2-3-telnet-region-sn/)

这两台是移动定制的海思平台网关，开 Telnet 的入口按固件版本分四条路：新版调试页加确认码、浏览器控制台脚本、一行网址、老版 webcmcc 接口。仓库只放工具、地区配置包和原帖存档。

## 目录

- `tools/H2Code.exe`：算确认码，新版调试页必用
- `tools/putty.exe`：Telnet 客户端
- `tools/tftpd64.exe`：TFTP 服务端，备份配置时用
- `tools/通用/`：原包里一起带的华为通用工具（ONT 使能、HW Dollar2、配置加解密）。**这三样在 H1s-3 / H2-3 上用不上**，平台不同，留着是为了对照
- `configs/config.tar`：22 个省份的配置模板 `cmcc_smart_<省份>_1_3_1_4_1.xml`
- `configs/board.tar`：5 个通用板型加 10 个 `hi5661y` 板型
- `docs/H1s-3 H2-3 开 Telnet 教程存档.mhtml`：恩山原帖的整页存档，含 2022、2024 两次补充
- `docs/说明.txt`：原工具包的说明

## 文件与 SHA256

| 文件 | 字节 |
|---|---|
| `tools/H2Code.exe` | 409,299 |
| `tools/putty.exe` | 574,976 |
| `tools/tftpd64.exe` | 146,656 |
| `tools/通用/ONT_V300R017C00SPC218.exe` | 3,770,880 |
| `tools/通用/HW_Dollar2.exe` | 161,280 |
| `tools/通用/华为光猫配置文件加解密工具.exe` | 1,794,560 |
| `configs/config.tar` | 2,119,680 |
| `configs/board.tar` | 61,440 |
| `docs/H1s-3 H2-3 开 Telnet 教程存档.mhtml` | 2,812,682 |
| `docs/说明.txt` | 616 |

```
d06121f2178c2e72ab528422ee9449dc442a263b81b638299c2b0ac9a3e0463e  tools/H2Code.exe
a92c1d668f6d060db06535ad346221d23dec11f897d79115673206462906f698  tools/putty.exe
988292db5e71fa50b090ce2bfe66813791d944cde64c19b7f0ecda8892392a15  tools/tftpd64.exe
a637954b61d9c15db42fb346092837d009f404ec466bdc10319b28da7b8ed8be  tools/通用/ONT_V300R017C00SPC218.exe
d3110469d8cccc7ca479105393e047faef74c74cfb34d174deece84153ac1cc8  tools/通用/HW_Dollar2.exe
8f005af234f73a456f5e4a127ed4624c40992445caf264d5f7566cbf3ee80808  tools/通用/华为光猫配置文件加解密工具.exe
6b8f15d0d01f7c4439756de747e7329c4c4b5e6cac6108e5bc323091e5d7cef7  configs/config.tar
1a54c56799ddb74c2da22b2e7a4e3505ca0b7143f89de57bb035924ee14589b9  configs/board.tar
39d72431801215f1787ac49d5b0c86344d5d4b08e44dea5126f1027fcbbe874f  docs/H1s-3 H2-3 开 Telnet 教程存档.mhtml
803f08286008d2019124cbde46bb5944c3744929b03697647e01d6f867fd6ef1  docs/说明.txt
```

## 使用顺序

1. 先用机身标签上的账号登录 `192.168.1.1`，确认后台能开。
2. 按固件版本选入口：先试 `/webcmcc/rc_telnet_debug.html`，404 就退回控制台脚本或一行网址。
3. 新版需要确认码：从 `/webcmcc/gui_device_info.html` 取 GPONSN，用 `H2Code.exe` 算。
4. 登录 Telnet（默认 `root` / `!@qw34er`），先 `cat /config/work/sysinfo.xml` 看清身份参数。
5. 改地区用 `hi_cfm set sysinfo.province <省份拼音>`，然后 `hi_cfm config`、`reboot`。

## 关于配置包

`config.tar` 里是 22 个省份的 `cmcc_smart_*.xml`，`board.tar` 是单板配置。**原帖只给了文件，没写怎么加载**，仓库原样保存，不提供加载方法。日常改地区优先用 `hi_cfm` 命令。

## 免责声明

工具与配置包均来自公开论坛资料，仅供自有设备维修与学习使用。改地区、改 SN/MAC 有断网和变砖风险，操作前先备份 `/config/work/sysinfo.xml` 与 `lastgood.xml`。仓库不含任何真实设备的配置备份。
