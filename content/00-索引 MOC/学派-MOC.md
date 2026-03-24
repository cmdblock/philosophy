---
title: 哲学学派 MOC
created: 2026-03-24
tags:
  - MOC
  - 哲学学派
---

# 哲学学派 MOC

## 按时期分类

### 古希腊哲学学派

```dataviewjs
const currentFolder = dv.current().file.folder;
const pathArray = currentFolder.split("/");
pathArray.pop();
const parentPath = pathArray.join("/");
const folderPath = `${parentPath}/04-学派`;

const files = dv.pages(`"${folderPath}"`)
    .where(p => {
        const ancient = ['米利都学派', '毕达哥拉斯学派', '爱利亚学派', '赫拉克利特', '原子论', '多元论', '智者学派', '犬儒学派', '柏拉图学园', '逍遥学派', '伊壁鸠鲁学派', '斯多葛学派', '怀疑主义', '学院派怀疑论', '新柏拉图主义'];
        return ancient.includes(p.file.name);
    })
    .sort(p => p.file.name, 'asc');
    
dv.list(files.map(p => p.file.link));
```

### 中世纪哲学学派

```dataviewjs
const currentFolder = dv.current().file.folder;
const pathArray = currentFolder.split("/");
pathArray.pop();
const parentPath = pathArray.join("/");
const folderPath = `${parentPath}/04-学派`;

const files = dv.pages(`"${folderPath}"`)
    .where(p => {
        const medieval = ['教父哲学', '经院哲学', '犹太亚里士多德主义', '阿维森纳主义'];
        return medieval.includes(p.file.name);
    })
    .sort(p => p.file.name, 'asc');
    
dv.list(files.map(p => p.file.link));
```

### 近代哲学学派

```dataviewjs
const currentFolder = dv.current().file.folder;
const pathArray = currentFolder.split("/");
pathArray.pop();
const parentPath = pathArray.join("/");
const folderPath = `${parentPath}/04-学派`;

const files = dv.pages(`"${folderPath}"`)
    .where(p => {
        const modern = ['唯理主义', '经验主义', '启蒙哲学', '社会契约论', '自由主义', '古典自由主义', '功利主义', '偏好功利主义', '德国古典哲学', '先验唯心主义', '主观唯心主义', '同一哲学', '绝对唯心主义', '唯物主义', '唯物史观', '青年黑格尔派', '唯意志论', '悲观主义', '权力意志', '生命哲学', '浪漫主义', '总体艺术'];
        return modern.includes(p.file.name);
    })
    .sort(p => p.file.name, 'asc');
    
dv.list(files.map(p => p.file.link));
```

### 现当代哲学学派

```dataviewjs
const currentFolder = dv.current().file.folder;
const pathArray = currentFolder.split("/");
pathArray.pop();
const parentPath = pathArray.join("/");
const folderPath = `${parentPath}/04-学派`;

const files = dv.pages(`"${folderPath}"`)
    .where(p => {
        const contemporary = ['马克思主义', '存在主义', '基督教存在主义', '无神论存在主义', '荒诞主义', '存在论', '现象学', '分析哲学', '逻辑主义', '逻辑原子论', '日常语言哲学', '结构主义', '后结构主义', '解构主义', '欧陆哲学', '精神分析学派', '法兰克福学派', '批判理论', '批判理性主义', '正义论', '自由至上主义', '拉康派马克思主义'];
        return contemporary.includes(p.file.name);
    })
    .sort(p => p.file.name, 'asc');
    
dv.list(files.map(p => p.file.link));
```

---

## 所有学派（按拼音排序）

```dataviewjs
const currentFolder = dv.current().file.folder;
const pathArray = currentFolder.split("/");
pathArray.pop();
const parentPath = pathArray.join("/");
const folderPath = `${parentPath}/04-学派`;

const files = dv.pages(`"${folderPath}"`)
    .sort(p => p.file.name, 'asc');
    
dv.list(files.map(p => p.file.link));
```

---

## 统计信息

```dataviewjs
const currentFolder = dv.current().file.folder;
const pathArray = currentFolder.split("/");
pathArray.pop();
const parentPath = pathArray.join("/");
const folderPath = `${parentPath}/04-学派`;

const files = dv.pages(`"${folderPath}"`);
dv.paragraph(`当前收录学派数量：**${files.length}** 个`);
```
