---
title: 核心人物 MOC
created: 2026-03-24
tags:
  - MOC
  - 哲学主要著作
---

# 核心人物 MOC

---
```dataviewjs
const currentFolder = dv.current().file.folder;
// 修复：手动计算向上跳一级的路径
const pathArray = currentFolder.split("/");
pathArray.pop(); 
const parentPath = pathArray.join("/");
const folderPath = `${parentPath}/01-时期与流派`;

// 获取所有文件 (确保路径用双引号包裹以防空格)
const files = dv.pages(`"${folderPath}"`)
  .where(p => p.file.path.endsWith(".md"))
  .sort(p => p.file.name, "asc");

if (files.length === 0) {
    dv.paragraph(`⚠️ 未在路径 "${folderPath}" 中找到任何文件，请检查文件夹名称是否正确。`);
} else {
    const grouped = {};

    for (const page of files) {
      // 提取相对子目录
      // 使用 split 和 filter 避开正则匹配的斜杠坑
      const relativePath = page.file.folder
        .replace(folderPath, "")
        .replace(/^[\\\/]/, ""); // 去掉开头的斜杠

      const groupKey = relativePath || "根目录";

      if (!grouped[groupKey]) {
        grouped[groupKey] = [];
      }

      grouped[groupKey].push({
        link: page.file.link,
        era: page.时代 || page.era || "", // 兼容中英文属性
        aliases: page.file.aliases || page.aliases || []
      });
    }

    // 排序逻辑保持不变
    const sortedKeys = Object.keys(grouped).sort((a, b) => {
      const numA = a.match(/^(\d+)/);
      const numB = b.match(/^(\d+)/);
      return (numA && numB) ? parseInt(numA[1]) - parseInt(numB[1]) : a.localeCompare(b);
    });

    for (const key of sortedKeys) {
      dv.header(3, key.replace(/\//g, " → "));
      
      const rows = grouped[key].map(item => [
        item.link,
        item.era,
        Array.isArray(item.aliases) ? item.aliases.join(", ") : item.aliases
      ]);

      dv.table(["人物", "时代", "别名"], rows);
    }

    dv.paragraph(`---`);
    dv.paragraph(`**共计 ${files.length} 位哲学人物**`);
}
```
