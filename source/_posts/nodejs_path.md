---
title: nodejs path库使用
tags: [nodejs]
date: 2022-06-27
---

1. 获取当前文件夹下的所有文件夹和文件
```
  let dirs = fs.readdirSync(__dirname)
  dirs.forEach(dir => {
    console.log(path.join(__dirname, dir))
});
```
