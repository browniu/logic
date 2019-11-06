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
## 函数柯里化
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

## 冒泡排序
```JavaScript
const bubbleSort = (array) => {
    for (let i = 0; i < array.length; i++) {
        for (let j = 0; j < array.length - i; j++) {
            if (array[j - 1] && array[j - 1] > array[j]) {
                const left = array[j - 1];
                array[j - 1] = array[j];
                array[j] = left
            }
        }
    }
    return array
};

console.log(bubbleSort([4, 6, 2, 1, 5, 3]));

```

## 数组去重
```JavaScript
const cleanCopy = (array) => {
    let box = [];
    for (i of array) if (!box.includes(i)) box.push(i);
    return box
};

console.log(cleanCopy([2, 4, 2, 1]));
```
```JavaScript
const cleanCopyFilter = array => array.filter((v, i, arr) => arr.indexOf(v) === i);
```

## 数组扁平化
```JavaScript
const arrayFlat = array => {
    let result = [];
    array.map(e => {
        if (Array.isArray(e)) result = result.concat(arrayFlat(e));
        else result.push(e)
    });
    return result
};
console.log(arrayFlat([3, 4, 'a', true, [3, ['c', 2], 5]]));
```
```JavaScript
const arrayFlatInNumber = array => array.toString().split(',').map(e => Number(e));
console.log(arrayFlatInNumber([1, 2, [3, [7, 8, 9]], 5, 6]));
```

## 对象深拷贝
```JavaScript
const deepCopy = obj =>{
    let result = Array.isArray(obj)?[]:{}
    for(k in obj){
        if (typeof obj[k] === 'object' && obj[k] !== null) result[k]= deeCopy(obj[k])
        else result[k] = obj[k]
    }
    return result
}
```
## 倒计时
```JavaScript
const yearCounter = year => {
    const now = new Date().getTime();
    const target = new Date(year, 0, 0, 0, 0, 0).getTime();
    const during = (target - now) / 1000;
    const days = Math.floor(during / (60 * 60 * 24));
    const hours = Math.floor(during % (60 * 60 * 24) / (60 * 60));
    const minutes = Math.floor(during % (60 * 60 * 24) % (60 * 60) / 60);
    const seconds = Math.floor(during % (60 * 60 * 24) % (60 * 60) % 60);
    return `距离${year}年还有${days}天${hours}时${minutes}分${seconds}秒`
};

console.log(yearCounter(2021));
```

## QueryString
```JavaScript
const queryToString = query => {
    let result = []
    for (k in query) {
        result.push(`${k}=${query[k]}`)
    }
    return '?' + result.join('&')
};

console.log(queryToString({name: 'xixi', age: 18}))
```
```JavaScript
const stringToQuery = (string) => {
    string = /\?/.test(string) ? string.split('?')[1] : string.split('?')[0]
    string = string.split('&');
    let obj = {}
    string.forEach(e => {
        const key = e.split('=')[0]
        const value = e.split('=')[1]
        obj[key] = value
    })
    return obj
};

console.log(stringToQuery('?name=xixi&age=18'))
```
