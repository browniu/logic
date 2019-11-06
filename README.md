# logic
经典逻辑应用

## 指定位数和范围的随机不重复整数组
```JavaScript
const randomArrayInLength = (n, [min, max] = [0, 10]) => new Promise(resolve => {
    let result = [];
    const geneItem = () => {
        const item = Math.floor(Math.random() * (max - min + 1) + min);
        result.push(item);
        result = [...new Set(result)];
        if (result.length >= n) resolve(result);
        else (geneItem())
    };
    geneItem()
});

randomArrayInLength(10).then(res => console.log(res));
```
