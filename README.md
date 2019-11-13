# logic
经典逻辑应用

## 指定位数和范围的随机不重复整数组
```JavaScript
const randomArrayInLength = (n, [min, max] = [0, 10]) => new Promise(resolve => {
    max = max - min >= n ? max : min+n
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

## 数组迭代
```JavaScript
const arrayAdd = array => array.reduce((all, current) => all + current)
```

## 延时器
```JavaScript
const delay = (time = 500) => new Promise(resolve => setTimeout(() => resolve(), time))
```

## 字符频次
```JavaScript
const chatMap = string => {
    const result = [];
    for (let e of string) {
        let newItem = true;
        for (let i in result) {
            if (result[i][0] === e) {
                result[i][1] = result[i][1] + 1;
                newItem = false
            }
        }
        if (newItem) result.push([e, 1])
    }
    return result.sort((a, b) => b[1] - a[1])
};
```
```JavaScript
const chatsList = string => {
    let result = {};
    string.split('').forEach(e => {
        if (!result.hasOwnProperty(e)) result[e] = 1;
        else result[e] = result[e] + 1
    });
    return result
};
```

## 防抖/截流
```JavaScript
const debounce=(time,func)=>{
    let timer;
    return ()=>{
        clearTimeout(timer)
        setTimeout(func,time)
    }
}
```
```JavaScript
const throttle=(time,func)=>{
    let start =0
    return ()=>{
        let now = Date.now()
        if(now-start>=time){
            start=now
            func()
        }
    }
}
```
```
document.body.onclick=debounce/throttle(500,()=>console.log('click'))
```

## 阶乘
```JavaScript
const cramp = n =>{
    if(n<=1) return n
    return n * cramp(n-1)
}
```

## 斐波纳切
```JavaScript
const fbnq = n => {
    if (n <= 2) return 1;
    return fbnq(n - 1) + fbnq(n - 2)
};
```

## 对象扁平化
```JavaScript
const objFlat = (obj, prefix) => {
    let result = Array.isArray(obj) ? [] : {}
    for (k in obj) {
        const key = !prefix ? k : /^\d$/.test(k) ? `${prefix}[${k}]` : `${prefix}.${k}`
        if (obj[k] instanceof Object) result = Object.assign(result, objFlat(obj[k], key))
        else result[key] = obj[k]
    }
    return result
};
```

## 数组扁平化
```JavaScript
array.flat(Infinity)
```

## 多维排序
```JavaScript
 const attriblesSort = array =>array.sort((a,b)=>{
    if (a.g !== b.g) return b.g - a.g;
    if (a.s !== b.s) return b.s - a.s;
    if (a.b !== b.b) return b.b - a.b;
    if (a.name !== b.name) return b.name > a.name ? -1 : 1
 })
```

## 组合遍历
```JavaScript
const arrayGroupTraverse = (array,target)=>{
    for(i=0; i<array.length; i++){
        for(j=i; j<array.length; j++){
            if(array[i]+array[j]===count) return [i,j]
        }
    }
}
```

## 奶牛繁衍
```JavaScript
const howManyCowsAfterYears = n => new Promise(resolve => {
    let num = 1;
    const circle = () => {
        for (let i = 1; i <= 6; i++) {
            n = n - 1;
            if (i === 3 || i === 5) num = num + 1;
            if (i === 6) num = num - 1;
            if (n <= 0) resolve(num)
        }
        if (n > 0) circle()
    };
    circle()
});
```

## 连续子串
```JavaScript
const findLongestString = string => {
    let str = '';
    let temp = '';
    let result = [];
    for (let e of string) {
        str = str.includes(e) ? str + e : e;
        if (str.length > temp.length) {
            result = [];
            temp = str;
        }
        if (str.length === temp.length) result.push(str)
    }
    return result
};
```

## 快速排序
```JavaScript
const quickSort = array => {
    if (array.length <= 1) return array;
    const left = [];
    const right = [];
    for (let i = 1; i < array.length; i++) {
        if (array[i] > array[0]) right.push(array[i])
        else left.push(array[i])
    }
    return [].concat(quickSort(left), array[0], quickSort(right))
};
```

## 数值交换
```JavaScript
a = a + b
b = a - b
a = a - b
```

## 数组最大值
```JavaScript
Math.max.apply(null,[...])
```

## 哈希字符串
```JavaScript
const hashString = n => {
    const result = []
    for (let i = 0; i < n; i++) {
        const code = Math.floor(Math.random() * ('z'.charCodeAt(0) - 'a'.charCodeAt(0)));
        result.push(String.fromCharCode(code + 'a'.charCodeAt(0)))
    }
    return result.join('')
};
```

## 乱序重排
```JavaScript
const unSortArray = array => new Promise(resolve => {
    const result = [];
    const circle = () => {
        result.push(array.splice(Math.floor(Math.random() * array.length), 1)[0]);
        if (array.length < 1) resolve(result);
        else circle()
    };
    circle()
});
```
