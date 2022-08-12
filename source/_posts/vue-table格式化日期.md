---
title: vue-table格式化日期
date: 2022-08-08 20:21:28
tags: vue
---

对于vue中表格日期格式化
### el-table格式化日期
<!--more-->
```
const timeFormatter = (row, column, cellValue, index) => {
        let format = "YYYY-mm-dd HH:MM:SS"
        let date = new Date(cellValue)
        const dataItem = {
            "Y+": date.getFullYear().toString(),
            "m+": (date.getMonth() + 1).toString(),
            "d+": date.getDate().toString(),
            "H+": date.getHours().toString(),
            "M+": date.getMinutes().toString(),
            "S+": date.getSeconds().toString()
        }
        Object.keys(dataItem).forEach((item) => {
            const ret = new RegExp(`(${item})`).exec(format);
            if(ret){
                format = format.replace(ret[1], ret[1].length === 1? dataItem[item]: dataItem[item].padStart(ret[1].length, "0"))
            }
        });
        return format
    }

```


`:formatter="timeFormatter"`


