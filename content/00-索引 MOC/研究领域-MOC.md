---
title: 哲学研究领域 MOC
aliases:
created: 2026-03-24
tags:
    - 哲学研究领域
    - MOC
---
# 研究领域-MOC

---
## 按字母排序

```dataviewjs
const currentFolder = dv.current().file.folder;
const pathArray = currentFolder.split("/");
pathArray.pop();
const parentPath = pathArray.join("/");
const folderPath = `${parentPath}/03-研究领域`;

dv.list(
    dv.pages(`"${folderPath}"`)
        .sort(p => p.file.name, 'asc')
        .file.link
)
```

## 统计信息

```dataviewjs
const currentFolder = dv.current().file.folder;
const pathArray = currentFolder.split("/");
pathArray.pop();
const parentPath = pathArray.join("/");
const folderPath = `${parentPath}/03-研究领域`;

dv.paragraph(`**研究领域总数**：${dv.pages(`"${folderPath}"`).length}`);
```
