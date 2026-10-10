# Cercis reader documentation (cercis-docs)

**English** | [中文](README.zh-CN.md)

> May Cerces safeguard your thoughts.

This repository holds the **reader-facing** documentation: the data format specification, template
and terminology notes, tutorials and a tour of the synthetic example.
It is written for people who want to keep their data in Cercis (graduate students, postdocs,
technicians, PIs) and for people who want to write plugins for it.

**No real research data here**: every example is fictional and the synthetic dataset is generated
by a script. Internal development documents (requirement document, decision log, milestones) are
not in this repository and are not published.

> **A note on language**: the documents themselves are currently written in Chinese; an English
> translation is planned. Issues and pull requests that improve or translate a page are welcome.

## Where to start

| You are | Start with | Then |
|---------|-----------|------|
| hearing about Cercis for the first time | [01 Quick start](01-快速上手.md) | [05 Tutorial: a day in the field](05-教程-田间一天.md) |
| curious what the data looks like | [02 Data format](02-数据格式规范.md) | [03 Templates and terminology](03-模板与术语.md) |
| sitting on a pile of Excel files | the "import" section of [01 Quick start](01-快速上手.md) | [07 Working with R and AI](07-给R与AI用.md) |
| moving between two devices (lab and field) | [06 Tutorial: two devices](06-教程-两台设备.md) | [04 Project folder layout](04-项目文件夹结构.md) |
| wanting to read and record on a tablet or phone | [10 Using a tablet or phone](10-平板手机怎么用.md) | [06 Tutorial: two devices](06-教程-两台设备.md) |
| writing a plugin | [08 Plugin development](08-插件开发.md) | [cercis-ui](https://github.com/epigrove/cercis-ui) (UI specification) |
| wanting a real dataset to poke at | [09 Synthetic example](09-合成示例与验收.md) | [cercis-examples](https://github.com/epigrove/cercis-examples) |

## Related repositories

| Repository | What it is |
|------------|-----------|
| [cercis](https://github.com/epigrove/cercis) | project overview (front door) |
| [cercis-core](https://github.com/epigrove/cercis-core) | kernel: storage + AI-friendliness (Rust library + `cercis` CLI) |
| [cercis-kits-basic](https://github.com/epigrove/cercis-kits-basic) | basic kit (ships with the app) |
| [cercis-kits-research](https://github.com/epigrove/cercis-kits-research) | research kit (through the plugin marketplace, on demand) |
| [cercis-apps](https://github.com/epigrove/cercis-apps) | apps and plugin host |
| [cercis-ui](https://github.com/epigrove/cercis-ui) | plugin UI specification |
| [cercis-examples](https://github.com/epigrove/cercis-examples) | synthetic example and golden-reference acceptance |
| **cercis-docs** (this repository) | reader documentation |

## Three rules to remember

1. **Data is append-only**: a correction does not overwrite anything — it adds a correction
   record, and the original value stays forever.
2. **Writes go through the tool**: plugins and AI write through kernel commands (automatic log,
   automatic validation) and never edit the CSV files directly.
3. **The folder is the database**: without Cercis, Excel, R or a text editor can still read and
   use the data.

## License

This repository's documentation: **CC BY 4.0** (reuse with attribution; see [LICENSE](LICENSE)).
The code repositories (`cercis-core` and friends) are **Apache-2.0**.
