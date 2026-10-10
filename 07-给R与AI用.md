# 07 给 R 与 AI 用

Cercis 的设计前提：**统计、建模、绘图交给 R/Python/SPSS**，它只负责把数据整理干净、说清来源。

## 给 R / Python

数据就是 CSV，直接读即可：

```r
d <- read.csv("我的试验/tables/records.csv", fileEncoding = "UTF-8", na.strings = "")
```

要更省事（列名 → 中文标签、允许值、单位、导出说明书）用科研工具包的导出：

```bash
# 长表导出（CSV）+ 说明书（含数据版本指纹）
cercis-plugin-research-io export <项目> --table records --out exports/records --format csv --readme

# 宽表（一样本一行、指标成列）
cercis-plugin-research-io export <项目> --table observations --out exports/wide \
    --format csv --wide trait_id --value value_num --readme

# SPSS：语法文件 + 值编码（分类列按允许值顺序落 1/2/3，附 VALUE LABELS）
cercis-plugin-research-io export-spss <项目> --table observations --out exports/spss --encode-values

# R 脚本：因子、标签、缺失值都替你写好
cercis-plugin-research-io export-r <项目> --table observations --out exports/r
```

导出的 `*.README.md` 里写着：**这一版数据的指纹**、当时用的模板与术语包、筛掉了什么行、缺失值怎么表示。
半年后（或审稿人问起）照着它就能复现。

## 给 AI（Codex / Claude Code 这些宿主）

内核会按 AI 契约**同源生成**三样东西：

| 文件 | 给谁看 | 内容 |
|---|---|---|
| `AGENTS.md` / `CLAUDE.md` | AI 冷启动 | 这项目有什么表、字段、规则、常用命令、禁止事项 |
| `_labnote/ai_contract.json` | 机器 | 结构化契约（表、命令、规则、红线） |
| `_labnote/skill/cercis/` | AI 宿主 | **Agent 技能包**：装到 Codex / Claude Code 的操作手册（不含任何数据） |

生成与安装：

```bash
cercis agents <项目>                    # 刷新上面三样
cercis skill  <项目> --install codex    # 把技能包装到 ~/.codex/skills/
cercis skill  <项目> --install claude   # 装到 Claude Code
```

**还没建库就想先把 AI 教会？** 用通用技能包（不依赖任何项目，命令与红线是一样的）：

```bash
cercis skill --generic --install codex     # 或 --install claude
cercis skill --generic --out ~/某目录       # 只想看看它写了什么
```

有具体项目后，再用上面的 `cercis skill <项目> --install …` 覆盖成**带你项目表结构**的那一版。

装好之后，新开一个 AI 会话，它就能"**只凭技能包 + 项目里的文件**"走通：
查数 → 试运行导入 → 确认写入 → 导出。

### AI 的权限边界（重要）

- **只读默认**：AI 想写入必须由你确认；
- **写入只能走 `cercis` 命令**：它不能直接编辑 CSV；
- **加密区域读不了**：密文对 AI 不可读；要分析就先 `cercis share export` 解密导出，用完清理；
- **不联网也能用**：AI 读的是项目内的文件与技能包。

## 一条最小示例（AI 视角）

```bash
cercis manifest-cmd <项目>                                  # 先读清单：有哪些表、多少行
cercis query <项目> --table records --filter stage eq 抽穗期 --json
cercis append-many <项目> --table records --from 草稿.csv --dry-run --json   # 先试运行
cercis append-many <项目> --table records --from 草稿.csv --source-ref 草稿.csv
cercis note <项目> --action export --summary "导出给 R 复算" --source-ref exports/records
```
