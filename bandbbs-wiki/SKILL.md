---
name: bandbbs-wiki
description: >
  Index and navigator for the BandBBS Wiki (https://wiki.bandbbs.cn).
  Use this skill whenever the user asks about anything related to BandBBS Wiki,
  米坛社区, AstroBox, BandBurg, Xiaomi wearables, watch faces, 表盘自定义工具,
  smart-band firmware, Mi Band / Xiaomi Watch tutorials, watch face custom tool,
  or anything about the BandBBS community itself.
  This skill provides a structured URL index so you can locate the most relevant
  wiki page and then fetch it with fetch_content or web_search.
  NOTE: If there is a dedicated AstroBox-specific skill available, prefer that skill
  for pure AstroBox questions; use this skill for broader BandBBS Wiki navigation.
---

# BandBBS Wiki Index

This skill gives you a curated index of all pages on https://wiki.bandbbs.cn.
When a user asks a question that might be answered by this wiki, **consult this index first** to find the best matching URL, then use `fetch_content` to retrieve the page and answer the user.

## What is BandBBS Wiki?

BandBBS (米坛社区) is a Chinese community focused on Xiaomi / Mi Band smart wearables.
Their wiki covers:
- **BandBurg** – related tooling ecosystem
- **Watch Face Custom Tool (表盘自定义工具)** – tutorials, AuthKey extraction, troubleshooting
- **Product Wiki** – Xiaomi device specs, platform chips (BES, Hisilicon, Qualcomm, XRING)
- **Community Guides** – app downloads, registration, custom firmware flashing
- **AstroBox** – only use when no dedicated AstroBox skill is available

## URL Index

### 📘 About & Announcements
- https://wiki.bandbbs.cn/About/
- https://wiki.bandbbs.cn/About/team.html
- https://wiki.bandbbs.cn/Announcements/

### 🏰 Guides – BandBurg
- https://wiki.bandbbs.cn/Guides/BandBurg/BandBurg%E4%BD%BF%E7%94%A8%E6%95%99%E7%A8%8B.html (BandBurg 使用教程)

### 🔌 Guides – AstroBox (fallback only)
- https://wiki.bandbbs.cn/Guides/astrobox/AstroboxV1%E5%85%A5%E9%97%A8%E5%AE%89%E8%A3%85%E7%AF%87.html
- https://wiki.bandbbs.cn/Guides/astrobox/AstroboxV1%E8%BF%9E%E6%8E%A5%E7%AF%87.html
- https://wiki.bandbbs.cn/Guides/astrobox/AstroboxV1%E8%B4%A6%E5%8F%B7%E7%AF%87.html
- https://wiki.bandbbs.cn/Guides/astrobox/AstroboxV1%E5%8A%9F%E8%83%BD%E7%AF%87.html
- https://wiki.bandbbs.cn/Guides/astrobox/AstroboxV1%E4%B8%8B%E8%BD%BD%E8%B5%84%E6%BA%90%E5%AE%89%E8%A3%85%E7%AF%87.html
- https://wiki.bandbbs.cn/Guides/astrobox/AstroboxV1%E5%85%B6%E4%BB%96%E7%AF%87.html
- https://wiki.bandbbs.cn/Guides/astrobox/%E4%BD%BF%E7%94%A8AstroBox%E5%AE%89%E8%A3%85%E4%BD%A0%E7%9A%84%E7%AC%AC%E4%B8%80%E4%B8%AA%E8%A1%A8%E7%9B%98.html
- https://wiki.bandbbs.cn/Guides/astrobox-plugins/Omusic%E5%90%8C%E6%AD%A5Cookie.html

### ⚙️ Guides – Advanced
- https://wiki.bandbbs.cn/Guides/advanced/%E4%B8%BA%E4%BD%A0%E7%9A%84%E8%AE%BE%E5%A4%87%E5%88%B7%E5%85%A5%E8%87%AA%E5%AE%9A%E4%B9%89%E5%9B%BA%E4%BB%B6.html (为你的设备刷入自定义固件)

### 🏠 Guides – 米坛社区 (BandBBS Community)
- https://wiki.bandbbs.cn/Guides/bandbbs/%E7%B1%B3%E5%9D%9B%E7%A4%BE%E5%8C%BAapp%E4%B8%8B%E8%BD%BD%E6%95%99%E7%A8%8B.html (米坛社区 app 下载教程)
- https://wiki.bandbbs.cn/Guides/bandbbs/%E7%B1%B3%E5%9D%9B%E7%A4%BE%E5%8C%BA%E6%B3%A8%E5%86%8C%E6%95%99%E7%A8%8B.html (米坛社区注册教程)

### 📱 Guides – Third-Party Apps
- https://wiki.bandbbs.cn/Guides/third-party-apps/%E5%96%B5%E5%96%B5%E7%94%B5%E5%AD%90%E4%B9%A6.html (喵喵电子书)

### ⌚ Guides – Watch Face Custom Tool (表盘自定义工具)
- https://wiki.bandbbs.cn/Guides/watchface_custom_tool/%E4%BD%BF%E7%94%A8%E8%87%AA%E5%AE%9A%E4%B9%89%E5%B7%A5%E5%85%B7%E5%AE%89%E8%A3%85%E5%BF%AB%E5%BA%94%E7%94%A8%26%E8%A1%A8%E7%9B%98.html (使用自定义工具安装快应用 & 表盘)
- https://wiki.bandbbs.cn/Guides/watchface_custom_tool/%E4%BD%BF%E7%94%A8%E8%87%AA%E5%AE%9A%E4%B9%89%E5%B7%A5%E5%85%B7%E8%8E%B7%E5%8F%96Authkey.html (使用自定义工具获取 Authkey)
- https://wiki.bandbbs.cn/Guides/watchface_custom_tool/%E4%BD%BF%E7%94%A8%E8%A1%A8%E7%9B%98%E8%87%AA%E5%AE%9A%E4%B9%89%E5%B7%A5%E5%85%B7%E5%AE%89%E8%A3%85%E4%BD%A0%E7%9A%84%E7%AC%AC%E4%B8%80%E4%B8%AA%E8%A1%A8%E7%9B%98.html (使用表盘自定义工具安装你的第一个表盘)
- https://wiki.bandbbs.cn/Guides/watchface_custom_tool/%E5%BF%AB%E9%80%9F%E4%BA%86%E8%A7%A3%E8%A1%A8%E7%9B%98%E8%87%AA%E5%AE%9A%E4%B9%89%E5%B7%A5%E5%85%B7%E4%BD%BF%E7%94%A8.html (快速了解表盘自定义工具使用)
- https://wiki.bandbbs.cn/Guides/watchface_custom_tool/%E8%A1%A8%E7%9B%98%E8%87%AA%E5%AE%9A%E4%B9%89%E5%B7%A5%E5%85%B7%E5%B8%B8%E8%A7%81%E9%97%AE%E9%A2%98.html (表盘自定义工具常见问题)

### 📖 Product Wiki – Overview
- https://wiki.bandbbs.cn/ProductWiki/
- https://wiki.bandbbs.cn/ProductWiki/%E6%A6%82%E8%A7%88.html (概览)

### 📱 Product Wiki – Xiaomi Devices
- https://wiki.bandbbs.cn/ProductWiki/devices/Xiaomi/
- https://wiki.bandbbs.cn/ProductWiki/devices/Xiaomi/device.html
- https://wiki.bandbbs.cn/ProductWiki/devices/Xiaomi/name.html
- https://wiki.bandbbs.cn/ProductWiki/devices/Xiaomi/xiaomi-wearable-codes.html
- https://wiki.bandbbs.cn/ProductWiki/devices/Xiaomi/Watch/XiaomiWatchS5.html
- https://wiki.bandbbs.cn/ProductWiki/devices/Xiaomi/Watch/example.html

### 🧩 Product Wiki – Platforms / Chips
- https://wiki.bandbbs.cn/ProductWiki/platforms/Bestechnic/BES2700BP.html
- https://wiki.bandbbs.cn/ProductWiki/platforms/Bestechnic/BES2800BP.html
- https://wiki.bandbbs.cn/ProductWiki/platforms/Hisilicon/Hi9200V100.html
- https://wiki.bandbbs.cn/ProductWiki/platforms/Hisilicon/Kirin710L.html
- https://wiki.bandbbs.cn/ProductWiki/platforms/Qualcomm/SnapdragonW5.html
- https://wiki.bandbbs.cn/ProductWiki/platforms/XRING/XRING-T1.html

### 🛠️ Studio & Misc
- https://wiki.bandbbs.cn/Studio/
- https://wiki.bandbbs.cn/Studio/wiki-editor.html
- https://wiki.bandbbs.cn/api-examples.html
- https://wiki.bandbbs.cn/markdown-examples.html
- https://wiki.bandbbs.cn/

## How to Use This Index

1. **Match the user's intent to a section above.**
   - Example: "表盘工具怎么获取 AuthKey?" → Guides – Watch Face Custom Tool → `使用自定义工具获取Authkey.html`
   - Example: "小米 Watch S5 的芯片是什么?" → Product Wiki – Xiaomi Devices / Platforms

2. **Fetch the most relevant page(s) with `fetch_content`.**
   - If the exact page is obvious, fetch it directly.
   - If unsure, fetch the category overview first (e.g., `Guides/` or `ProductWiki/`).

3. **If nothing in the index seems to match, fetch the live sitemap.**
   - Use `fetch_content` on `https://wiki.bandbbs.cn/sitemap.xml`.
   - Parse the URL list for keywords that match the user's question (path segments or decoded Chinese filenames).
   - Select the most promising `<loc>` entry and fetch that page.
   - If multiple URLs look relevant, fetch them in parallel and synthesize the answer.

4. **Answer the user based on the fetched content.**
   - Cite the wiki page URL.
   - If the fetched page doesn't fully answer the question, fetch additional linked pages from the same index or sitemap.

## Quick Reference Mapping

| User asks about... | Likely target URL |
|--------------------|-------------------|
| 表盘自定义工具 教程 / 入门 | `Guides/watchface_custom_tool/快速了解表盘自定义工具使用.html` |
| 表盘自定义工具 常见问题 | `Guides/watchface_custom_tool/表盘自定义工具常见问题.html` |
| AuthKey 获取 | `Guides/watchface_custom_tool/使用自定义工具获取Authkey.html` |
| 刷自定义固件 | `Guides/advanced/为你的设备刷入自定义固件.html` |
| 米坛社区 app 下载 / 注册 | `Guides/bandbbs/米坛社区app下载教程.html` 或 `注册教程.html` |
| 小米设备型号 / 代码对照 | `ProductWiki/devices/Xiaomi/xiaomi-wearable-codes.html` |
| Xiaomi Watch S5 | `ProductWiki/devices/Xiaomi/Watch/XiaomiWatchS5.html` |
| BES2700BP / BES2800BP | `ProductWiki/platforms/Bestechnic/...` |
| Snapdragon W5 | `ProductWiki/platforms/Qualcomm/SnapdragonW5.html` |
