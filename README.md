# Portable Desktop Uninterruptible Power Supply

⭐ 便携桌面不间断电源 ⭐

[![pipeline status](https://gitlab.soraharu.com/XiaoXi/Portable-Desktop-Uninterruptible-Power-Supply/badges/master/pipeline.svg)](https://gitlab.soraharu.com/XiaoXi/Portable-Desktop-Uninterruptible-Power-Supply/-/commits/master)
[![Latest Release](https://gitlab.soraharu.com/XiaoXi/Portable-Desktop-Uninterruptible-Power-Supply/-/badges/release.svg)](https://gitlab.soraharu.com/XiaoXi/Portable-Desktop-Uninterruptible-Power-Supply/-/releases)
[![vercel](https://vercelbadge.soraharu.com/?app=interactivehtmlbom)](https://interactivehtmlbom.soraharu.com/)

🔗 [GitLab (Homepage)](https://gitlab.soraharu.com/XiaoXi/Portable-Desktop-Uninterruptible-Power-Supply) | 🔗 [OSHWHub](https://oshwhub.com/yanranxiaoxi/Portable-Desktop-Uninterruptible-Power-Supply) | 🔗 [GitHub](https://github.com/yanranxiaoxi/Portable-Desktop-Uninterruptible-Power-Supply)

![实拍图](https://downloadserver.soraharu.com:7000/Portable%20Desktop%20Uninterruptible%20Power%20Supply/Image/Product_quality_4.jpg)

## 🤔 这是什么

这是一个便携桌面不间断电源，使用 [立创 EDA](https://lceda.cn/) 进行开发。

本设计采用一颗由 英集芯(INJOINIC) 研发的 IP5306 高集成度锂电池充放电管理芯片作为核心的电池芯片，采用 芯龙(XLSEMI) 推出的 XL6019E1 升压型 DC-DC 电源芯片实现可调输出功能，能够实现在 7V ~ 35V 宽输入电压范围内的稳压输出，主要使用场景为作为功耗较低的桌面、嵌入式设备（如树莓派服务器、智能家居设备）的不间断电源。

## 🍭 使用说明

本设计不间断电源的功能实现逻辑如下：
- `外部 7V ~ 35V 供电` -> `电池输出及 XL6019E1 升压控制关闭` -> `VOUT = VIN - 0.7V（肖特基二极管防倒灌损耗）` -> `（可选择）780X LDO 输出`
- `无外部供电` -> `开启电池输出及 XL6019E1 升压控制` -> `电位器(R5)控制 VOUT 电压` -> `（可选择）780X LDO 输出`

如果需要实现完整的不间断电源功能，需要首先确定用电器需求的电压值，按照 PCB 上标记正确接入 18650 电池（**不要反接电池！**如需使用多节电池，需确保所有电池的电压及电池性能一致，否则可能导致电池组快速老化），在电源输出(OUTPUT)端接入电压表测量输出电压（如无电压输出，需按下 `SW1` 开启放电），调整电位器(`R5`)直到电压表读数为用电器需求的电压值，最后将能够提供对应电压的电源适配器连接到本设计的电源输入(INPUT)端，将电源输出端连接至用电器，即完成配置。

如果需要使用本设计连接多个不同电压的用电器，可以使用位于输出端口旁的两个 780X LDO 焊盘位 `U5` `U6`，焊接对应电压的稳压芯片。

请注意，本设计使用的电池管理芯片所支持的最大电池输出功率为 `12W`，这意味着，如果需要保证不间断电源功能的正常工作，负载用电器的最大功率需要为 `12W` 以内，为了能够在接通外部供电的情况下能够正常为电池组充电，连接到本设计电源输入端的电源适配器需要能够提供不少于 `负载用电器功率 + 10.5W` 的供电功率。

如果确定你的配置十分正确，但是在由外部供电转为内部供电时负载用电器出现重启、供电不稳等状况，可能是由于三极管反应速度过慢或你所购买的 XL6019E1 芯片为盗版芯片（已发现市面存在非 芯龙 生产的盗版芯片），可以尝试在输出端加装大容量高频电解电容器解决。

本 PCB 设计已通过完整功能性测试，且已添加 [嘉立创](https://www.jlc.com/) SMT 定位孔，可直接进行 SMT 贴片生产。但请注意，本设计完整开源并遵循 [GNU General Public License v3.0](https://choosealicense.com/licenses/gpl-3.0/) 开源协议，开源作者不对作品的安全性、完整性作任何承诺，且不对因此产生的任何损失承担后果。

你可以使用本项目的 [焊接助手](https://interactivehtmlbom.soraharu.com/Portable-Desktop-Uninterruptible-Power-Supply.html) 有效地提升手工焊接效率，本助手通过 [InteractiveHtmlBom](https://gitlab.soraharu.com/XiaoXi/InteractiveHtmlBom) 流水线自动化生成。

## 🏃 主要性能参数

- 电池充电功率：10.5W
- 电池最大输出功率：12W
- 最大输入 / 输出电流：4A
- 输入 / 输出电压范围：7V ~ 35V

## 🛠️ 生产电路板

本项目的 Gerber 文件可以从 [Releases](https://gitlab.soraharu.com/XiaoXi/Portable-Desktop-Uninterruptible-Power-Supply/-/releases) 页面获取，并允许在开源许可范围内的商业目的使用。

*建议使用 [嘉立创](https://www.jlc.com/) 生产高品质电路板。

*It is recommended to use [JLCPCB](https://jlcpcb.com/) to produce high-quality circuit boards.

## ⚙️ 部署至 EasyEDA

1. 克隆本项目 [源代码](https://gitlab.soraharu.com/XiaoXi/Portable-Desktop-Uninterruptible-Power-Supply/-/archive/master/Portable-Desktop-Uninterruptible-Power-Supply-master.zip) 到本地
2. 在立创 EDA 标准版编辑器中选择 `文件` -> `打开` -> `立创EDA...`
3. 选择本项目源代码中的 `/EasyEDA/*.json` 文件并分别导入

## 📜 开源许可

基于 [GNU General Public License v3.0](https://choosealicense.com/licenses/gpl-3.0/) 许可进行开源。

本设计已在 [中国版权保护中心](https://www.ccopyright.com.cn/) 登记注册。
