---
tags:
  - MOC
  - 哲学概念
title: 哲学核心概念 MOC
---

# 哲学核心概念 MOC

---
## 按拼音首字母分组

```dataviewjs
const currentFolder = dv.current().file.folder;
const pathArray = currentFolder.split("/");
pathArray.pop();
const parentPath = pathArray.join("/");
const folder = `${parentPath}/02-核心概念`;
const files = dv.pages(`"${folder}"`);

// 汉字拼音首字母映射表
const pinyinMap = {
    '阿': 'A', '爱': 'A', '安': 'A', '奥': 'A',
    '本': 'B', '被': 'B', '表': 'B', '剥': 'B', '不': 'B',
    '此': 'C', '存': 'C',
    '大': 'D', '道': 'D', '德': 'D', '第': 'D', '对': 'D',
    '俄': 'E',
    '反': 'F', '范': 'F', '非': 'F', '感': 'G', '高': 'G', '公': 'G', '广': 'G',
    '和': 'H', '荷': 'H', '荒': 'H', '集': 'J', '几': 'J', '家': 'J', '禁': 'J',
    '经': 'J', '绝': 'J', '恐': 'K', '快': 'K',
    '理': 'L', '力': 'L', '历': 'L', '流': 'L', '伦': 'L', '罗': 'L', '逻': 'L',
    '迷': 'M', '目': 'M',
    '内': 'N', '能': 'N', '宁': 'N',
    '普': 'P',
    '七': 'Q', '欺': 'Q', '潜': 'Q', '全': 'Q', '权': 'Q',
    '人': 'R',
    '三': 'S', '伤': 'S', '上': 'S', '审': 'S', '生': 'S', '实': 'S', '世': 'S',
    '事': 'S', '适': 'S', '属': 'S', '数': 'S', '思': 'S', '四': 'S',
    '他': 'T', '太': 'T', '同': 'T',
    '唯': 'W', '我': 'W', '无': 'W', '物': 'W',
    '西': 'X', '先': 'X', '想': 'X', '向': 'X', '象': 'X', '小': 'X', '形': 'X',
    '幸': 'X', '虚': 'X',
    '一': 'Y', '异': 'Y', '意': 'Y', '因': 'Y', '印': 'Y', '语': 'Y', '原': 'Y',
    '原': 'Y', '在': 'Z', '正': 'Z', '知': 'Z', '中': 'Z', '钟': 'Z', '主': 'Z',
    '自': 'Z', '宗': 'Z', '尊': 'Z', '最': 'Z'
};

// 获取拼音首字母
function getPinyinInitial(str) {
    if (!str) return "#";
    const char = str.charAt(0);
    // 如果是英文字母，直接返回大写
    if (/[a-zA-Z]/.test(char)) {
        return char.toUpperCase();
    }
    // 查表
    if (pinyinMap[char]) {
        return pinyinMap[char];
    }
    // 其他情况返回 #
    return "#";
}

// 按拼音首字母分组
const grouped = {};
for (const file of files) {
    const title = file.title || file.file.name;
    const initial = getPinyinInitial(title);
    if (!grouped[initial]) {
        grouped[initial] = [];
    }
    grouped[initial].push({
        title: title,
        aliases: file.aliases,
        proposer: file.提出者,
        school: file.归属学派,
        link: file.file.link
    });
}

// 排序并输出
const sortedKeys = Object.keys(grouped).sort();
for (const key of sortedKeys) {
    const items = grouped[key].sort((a, b) => a.title.localeCompare(b.title, 'zh-CN'));
    dv.header(3, key);
    dv.table(
        ["概念", "别名", "提出者", "归属学派"],
        items.map(item => [
            item.link,
            item.aliases || "-",
            item.proposer || "-",
            item.school || "-"
        ])
    );
}
```

## 按归属学派分组

```dataviewjs
const currentFolder = dv.current().file.folder;
const pathArray = currentFolder.split("/");
pathArray.pop();
const parentPath = pathArray.join("/");
const folder = `${parentPath}/02-核心概念`;
const files = dv.pages(`"${folder}"`);

// 按学派分组
const grouped = {};
const noSchool = [];

for (const file of files) {
    const school = file.归属学派;
    const item = {
        title: file.title || file.file.name,
        aliases: file.aliases,
        proposer: file.提出者,
        link: file.file.link
    };
    
    if (school) {
        // 处理多个学派的情况（用 / 或 , 分隔）
        const schools = String(school).split(/[/,，]/).map(s => s.trim().replace(/\[\[|\]\]/g, ''));
        for (const s of schools) {
            if (s) {
                if (!grouped[s]) grouped[s] = [];
                grouped[s].push(item);
            }
        }
    } else {
        noSchool.push(item);
    }
}

// 排序并输出
const sortedKeys = Object.keys(grouped).sort((a, b) => a.localeCompare(b, 'zh-CN'));
for (const key of sortedKeys) {
    const items = grouped[key].sort((a, b) => a.title.localeCompare(b.title, 'zh-CN'));
    dv.header(3, key);
    dv.list(items.map(item => `${item.link} ${item.aliases ? `(${item.aliases})` : ""}`));
}

if (noSchool.length > 0) {
    dv.header(3, "其他");
    dv.list(noSchool.map(item => item.link));
}
```

## 完整列表

```dataviewjs
const currentFolder = dv.current().file.folder;
const pathArray = currentFolder.split("/");
pathArray.pop();
const parentPath = pathArray.join("/");
const folder = `${parentPath}/02-核心概念`;
const files = dv.pages(`"${folder}"`).sort(f => f.title || f.file.name, 'asc');

dv.table(
    ["概念", "别名", "提出者", "归属学派"],
    files.map(f => [
        f.file.link,
        f.aliases || "-",
        f.提出者 || "-",
        f.归属学派 || "-"
    ])
);
```

## 统计信息

```dataviewjs
const currentFolder = dv.current().file.folder;
const pathArray = currentFolder.split("/");
pathArray.pop();
const parentPath = pathArray.join("/");
const folder = `${parentPath}/02-核心概念`;
const files = dv.pages(`"${folder}"`);
dv.paragraph(`共收录 **${files.length}** 个核心概念`);
```

---

#哲学 #MOC
