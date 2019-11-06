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
## 柯里化
```JavaScript
const func = (a, b) => console.log(a, b);
const curryFunc = a => b => console.log(a, b)
```
```JavaScript
const curryFunc = function (a) {
    if ([...arguments].length === 2) console.log(arguments[0], arguments[1])
    if ([...arguments].length === 1) return function (b) {
        console.log(a, b)
    }
};

curryFunc(1, 2);
curryFunc(1)(2);
```

## 字符串大小写交换
```JavaScript
const stringCaseExchange = (string) => {
    string = string.split('').map(e => {
        if (/[a-z]/.test(e)) return e.toUpperCase();
        if (/[A-Z]/.test(e)) return e.toLowerCase();
        return e
    });
    return string.join('')
};

console.log(stringCaseExchange('fafefaefDWW342FeafwEF'))
```
