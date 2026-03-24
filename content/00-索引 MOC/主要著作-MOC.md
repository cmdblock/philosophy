---
title: 主要著作 MOC
created: 2026-03-24
tags:
    - MOC
    - 哲学著作
---

# 主要著作 MOC

---

```dataviewjs
const currentFolder = dv.current().file.folder;
const pathArray = currentFolder.split("/");
pathArray.pop();
const parentPath = pathArray.join("/");
const folderPath = `${parentPath}/05-主要著作`;

// 获取所有 markdown 文件
const files = dv.pages(`"${folderPath}"`)
  .where(p => p.file.path.endsWith(".md"))
  .sort(p => p.file.name, "asc");

// 定义时代分组
function getEra(year) {
  if (!year) return "年代不详";
  
  // 提取年份数字
  const yearStr = String(year);
  const yearNum = parseInt(yearStr.replace(/[^-\d]/g, ""));
  
  if (isNaN(yearNum)) return "年代不详";
  
  if (yearNum < -500) return "01-前古典时期";
  if (yearNum < 1) return "02-古典时期（希腊化-罗马）";
  if (yearNum < 500) return "03-晚期古典";
  if (yearNum < 1400) return "04-中世纪";
  if (yearNum < 1600) return "05-文艺复兴";
  if (yearNum < 1700) return "06-17世纪";
  if (yearNum < 1800) return "07-18世纪";
  if (yearNum < 1850) return "08-19世纪上半叶";
  if (yearNum < 1900) return "09-19世纪下半叶";
  if (yearNum < 1950) return "10-20世纪上半叶";
  if (yearNum < 2000) return "11-20世纪下半叶";
  return "12-21世纪";
}

// 按时代分组
const grouped = {};

for (const page of files) {
  const era = getEra(page.出版年份);
  
  if (!grouped[era]) {
    grouped[era] = [];
  }
  
  // 获取标题（优先使用 frontmatter 中的 title）
  const title = page.title || page.file.name;
  
  // 获取作者（保留双链格式）
  let author = page.作者 || "";
  if (author) {
    // 提取双链内容
    const linkContent = String(author).replace(/\[\[|\]\]/g, "");
    
    // 检查是否有别名（|符号）
    if (linkContent.includes("|")) {
      const [path, display] = linkContent.split("|");
      author = dv.fileLink(path.trim(), false, display.trim());
    } else {
      author = dv.fileLink(linkContent, false, linkContent);
    }
  }
  
  // 获取年份
  let year = page.出版年份 || "";
  
  grouped[era].push({
    title: title,
    link: page.file.link,
    author: author,
    year: year,
    aliases: page.aliases || []
  });
}

// 对分组键进行排序
const sortedKeys = Object.keys(grouped).sort();

// 输出分组结果
for (const key of sortedKeys) {
  // 格式化分组标题（去掉数字前缀）
  const displayKey = key.replace(/^\d+-/, "");
  
  dv.header(2, displayKey);
  
  // 按年份排序（如果有的话）
  grouped[key].sort((a, b) => {
    const yearA = parseInt(String(a.year).replace(/[^-\d]/g, "") || "0");
    const yearB = parseInt(String(b.year).replace(/[^-\d]/g, "") || "0");
    return yearA - yearB;
  });
  
  // 创建表格数据
  const rows = grouped[key].map(item => [
    item.link,
    item.author,
    item.year,
    Array.isArray(item.aliases) ? item.aliases.join(", ") : item.aliases
  ]);
  
  dv.table(["著作", "作者", "年代", "别名"], rows);
}

// 显示统计信息
dv.paragraph(`---`);
dv.paragraph(`**共计 ${files.length} 部哲学著作**`);
```
