# 史记 · 竖排古籍排版工程

> 本仓库属 **[集贤古籍工程](https://github.com/jixian-guji)**（`jixian-guji` 组织）的样板工程之一。
> 参与排版 / 验收 / 提交规范见工程级 [CONTRIBUTING.md](https://github.com/jixian-guji#readme)。

用 XeLaTeX + `xeCJK` + `flowfram` 排版的《史记》竖排本。成品为筒子页（双半叶）装帧风格：竖排右起、棕色版框与书口、书名章题合并于鱼尾下、钤印、句读圆圈。

## 成品（均在 `成品/`）

| 文件 | 内容 |
|---|---|
| `史记·十二本纪.pdf` | 本纪十二篇 |
| `史记·三十世家.pdf` | 世家三十篇 |
| `史记·八书.pdf` | 八书 |
| `史记·十表.pdf` | 十表 |
| `史记·七十列传.pdf` | 列传七十篇 |
| `史记全书总目_一百三十篇.pdf` | 全书总目（独立成册） |

PDF 已内嵌字体，可直接阅读。

## 目录结构

```
成品/        6 个合订 PDF
源码/
  zhvt-classic.cls      排版模板（通用竖排 cls）
  yshs.png              钤印图
  LICENSE               模板版权声明（原作者所有）
  史记·*.tex            五部合订母本
  目录_*.tex / *_条目.tex  各部总目母本
  史记全书篇目总表*.csv  篇目数据
  分篇tex/              112 篇独立母本（本纪/世家/列传/书/表）
```

## 字体依赖（重编时需要）

均在母本 `zhvt-classic.cls` 中设置，路径为本机安装位置：

| 用途 | 字体 | 获取 |
|---|---|---|
| 正文 | 源明体 GenRyuMin2TW | 开源字体，可自行下载安装 |
| 题注/夹注 | 仿宋 `simfang.ttf` | Windows 系统字体 |

> 若他机路径不同，需修改 cls 中的 `FontSpec` 路径或改用系统字体名调用。

## 重编方法

```bash
xelatex -cnf-line=pool_size=12000000 -interaction=nonstopmode -halt-on-error -jobname=史记·十二本纪 史记·十二本纪.tex
# 两遍编译使 aux 稳定；目录册需从成品书口回查页码后生成
```

`pool_size=12000000` 不可省——本工程 TikZ 记录量大，默认池会溢出。目录页码必须从成品 PDF 书口回查，不能依赖 flowfram 中偏早展开的 `\zhnum{page}`。

## 底本与版权

- 底本 `.txt` 未随仓库分发（现代整理本有著作权），重编请自备对应文本。
- 《史记》原文为公有领域；排版模板版权见 `源码/LICENSE`。
