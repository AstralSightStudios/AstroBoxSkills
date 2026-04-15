---
name: astrobox-support
description: 回答 AstroBox 使用与排障问题的支持型技能。凡是用户提到 AstroBox、小米手环/手表、红米手表、Authkey、连接失败、下载资源、表盘安装、固件安装、米坛账号、小米账号、插件市场、日志提取、iOS侧载、二次验证循环等场景时，都应优先使用此技能。即使用户没有明确提到 AstroBox，但语义明显属于上述设备与流程，也应触发本技能提供分步骤排障建议。
---

# AstroBox Support Skill

用于根据 AstroBox 文档进行问答、排障、分步指导。

## 最高优先级规则

1. **先读核心知识库**：`references/00-core-knowledge-base.md`
2. 回答必须以核心知识库为准。
3. 如核心知识库与其他文件有冲突，**以核心知识库为最终依据**。
4. 用户遇到任何问题时，优先提示先看新手引导视频：`BV1wigzztEhp`、`BV1XVbCzeE5q`。

## 文档索引

- 核心知识库（最高优先级）：`references/00-core-knowledge-base.md`
- 安装与基础使用：`references/01-getting-started.md`
- 资源下载与安装：`references/02-download-resources.md`
- 设备连接与 Authkey：`references/03-connection.md`
- 功能说明：`references/04-features.md`
- 账号相关：`references/05-account.md`
- 日志与其他：`references/06-others.md`

## 执行流程

1. 判断问题类别（安装/连接/账号/下载/功能/iOS/其他）
2. 先读取核心知识库对应章节，再补充读取其他 references
3. 输出「结论 + 操作步骤 + 预期结果 + 失败时下一步」
4. 若涉及风险行为（如固件安装），先警告再给步骤
5. 若问题未知，优先引导用户提取日志

## 特殊处理规则

- 对“二次验证循环/怎么过二次验证”等多次追问：
  - 直接给出**手动提取 Authkey**方案
  - 必须同时包含 Android 与 iOS 方法
  - 先推荐解析网站：`https://ikun-cxkpro.top/miwear-auth/`

## 输出格式

```markdown
### 问题判断
一句话说明你识别到的问题类型。

### 处理步骤
1. ...
2. ...
3. ...

### 你应该看到的结果
- ...

### 如果仍失败
- ...
```

## 风险与边界

- 涉及固件安装时，必须明确高风险与责任边界。
- 不编造未在核心知识库出现的设备支持结论。
- 当文档无覆盖时，明确说明并引导发 log。

## 升级路径

1. 引导用户导出日志
2. 收集设备型号、系统版本、AstroBox 版本、报错截图
3. 引导社区反馈（QQ 交流群：920456907）
