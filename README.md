# Cercis 读者文档（cercis-docs）

> 愿瑟希斯捍卫你的思想。 / *May Cerces safeguard your thoughts.*

这里放**面向读者**的文档：数据格式规范、模板说明、教程、合成示例导览。
写给"要用 Cercis 管数据的人"（研究生、博士后、技术员、PI），也写给"要给 Cercis 写插件的人"。

**这里不含任何真实研究数据**：例子都是虚构的，合成数据由脚本生成。
开发内部文档（需求文档、决策记录、里程碑）不在这个仓库，也不随开源发布。

## 从哪读起

| 你是 | 从这篇开始 | 然后 |
|------|-----------|------|
| 第一次听说 Cercis | [01 快速上手](01-快速上手.md) | [05 教程：田间一天](05-教程-田间一天.md) |
| 想知道数据长什么样 | [02 数据格式规范](02-数据格式规范.md) | [03 模板与术语](03-模板与术语.md) |
| 已经有一堆 Excel 要搬进来 | [01 快速上手](01-快速上手.md) 的"导入"一节 | [07 给 R 与 AI 用](07-给R与AI用.md) |
| 两台设备来回跑（实验室/田里） | [06 教程：两台设备](06-教程-两台设备.md) | [04 项目文件夹结构](04-项目文件夹结构.md) |
| 想用平板/手机在田里看和录 | [10 平板手机怎么用](10-平板手机怎么用.md) | [06 教程：两台设备](06-教程-两台设备.md) |
| 要写插件 | [08 插件开发](08-插件开发.md) | [cercis-ui](https://github.com/epigrove/cercis-ui)（界面规范） |
| 想先看一份真实可跑的数据 | [09 合成示例与验收](09-合成示例与验收.md) | [cercis-examples](https://github.com/epigrove/cercis-examples) |

## 相关仓库

| 仓库 | 是什么 |
|------|--------|
| [cercis](https://github.com/epigrove/cercis) | 总介绍（门面） |
| [cercis-core](https://github.com/epigrove/cercis-core) | 内核：数据存取 + AI 友好（Rust 库 + `cercis` 命令行） |
| [cercis-kits-basic](https://github.com/epigrove/cercis-kits-basic) | 基础工具包（随 app 交付） |
| [cercis-kits-research](https://github.com/epigrove/cercis-kits-research) | 科研工具包（走插件市场，按需下载） |
| [cercis-apps](https://github.com/epigrove/cercis-apps) | 各平台界面与插件宿主 |
| [cercis-ui](https://github.com/epigrove/cercis-ui) | 插件界面规范 |
| [cercis-examples](https://github.com/epigrove/cercis-examples) | 合成示例与黄金对照验收 |
| **cercis-docs**（本仓库） | 读者文档 |

## 三条要记住的红线

1. **数据只增不改**：更正不是覆盖，而是新增一条更正记录；原值永久保留。
2. **写入必须走工具**：插件与 AI 都通过内核通道写数据（自动留痕、自动校验），不直接编辑 CSV。
3. **文件夹即数据库**：不用 Cercis、只用 Excel / R / 文本编辑器，也能读懂并使用这些数据。

## 许可

本仓库文档：**CC BY 4.0**（署名即可转载，见 [LICENSE](LICENSE)）。
代码仓库（cercis-core 等）为 **Apache-2.0**。
