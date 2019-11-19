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
const curry = (f, args1 = []) => (...args2) => f.length === args1.concat(args2).length ? f(...args1.concat(args2)) : curry(f, args1.concat(args2));

const add = curry((a, b, c, d) => a + b + c + d);
console.log(add(1, 2, 3, 4));
console.log(add(1)(2, 3)(4));
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


## 对象深拷贝
```JavaScript
const deepClone = object => {
    let result = Array.isArray(object) ? [] : {};
    for (let k in object) {
        object[k] instanceof Object ? result[k] = deepClone(object[k]) : result[k] = object[k]
    }
    return result
};
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

## QueryString/ParamsString
```JavaScript
const stringParams = params => {
    let result = [];
    for (let k in params) {
        let string = k + '=' + params[k].toString();
        if (Array.isArray(params[k])) string = params[k].map(v => k + '=' + v).join('&');
        if (params[k] === undefined) string = k;
        result.push(string)
    }
    return '?' + result.join('&')
};
```
```JavaScript
onst paramsString = url => {
    let result = [];
    url = decodeURI(url);
    url = /\?/.test(url) ? url.split('?')[1] : url.split('?')[0];
    const params = url.split('&');
    params.forEach(v => {
        const key = v.split('=')[0];
        let val = v.split('=')[1];
        val = Number(val).toString() !== 'NaN' ? Number(val) : val === undefined ? true : val
        if (result.hasOwnProperty(key)) {
            if (Array.isArray(result[key])) result[key].push(val);
            else result[key] = [result[key], val]
        } else result[key] = val
    });
    return result
};
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
const objectFlat = (object, prefix) => {
    let result = Array.isArray(object) ? [] : {}
    for (let k in object) {
        const key = !prefix ? k : /^[0-9]*$/.test(k) ? `${prefix}[${k}]` : `${prefix}.${k}`;
        object[k] instanceof Object? result = Object.assign(result, objectFlat(object[k], key)) : result[key] = object[k]
    }
    return result
};
```

## 数组扁平化
```JavaScript
const arrayFlat = array => {
    let result = [];
    array.forEach(v => Array.isArray(v) ? result = result.concat(arrayFlat(v)) : result.push(v));
    return result
};
```

```JavaScript
const arrayFlatInNumber = array => array.toString().split(',').map(v => /^[0-9]*$/.test(v) ? Number(v) : v)
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
    let result = [];
    let temp = '';
    let longest = '';
    for (let char of string) {
        temp = temp.includes(char) ? temp + char : char;
        if (temp.length > longest.length) {
            longest = temp;
            result = []
        }
        if (temp.length === longest.length) result.push(temp)
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
```JavaScript
array.sort(()=>Math.random()-0.5)
```

## 字符分布
```JavaScript
const mapChatIndex = string => {
    let result = [];
    for (let i = 0; i < string.length; i++) {
        let char = string.charAt(i);
        let newItem = true;
        result.some(v => {
            if (v.name === char) {
                v.index.push(i);
                newItem = false;
                return true
            }
        });
        newItem && result.push({name: char, index: [i]})
    }
    return result.sort((a, b) => b.index.length - a.index.length)
};
```

## 数组升维
```JavaScript
const dataTree = array => {
    let result = [];
    array.forEach(vA => {
        let newItem = true;
        result.some(vR => {
            if (vA.province === vR.province) {
                vR.city.push({name: vA.city, code: vA.code});
                newItem = false;
                return true
            }
        });
        newItem && result.push({province: vA.province, city: [{name: vA.city, code: vA.code}]})
    });
    return result
};
```

## 二分查找
```JavaScript
const findIndex = (array, target) => {
    array.sort();
    let start = 0;
    let end = array.length - 1;

    while (start <= end) {
        const middle = (start + end) / 2;
        if (target > array[middle]) start = middle + 1;
        if (target < array[middle]) end = middle - 1;
        if (target === array[middle]) return middle
    }
};
```
## 模版引擎
```JavaScript
const renderTemp = (temp, data) => temp.replace(/{{(.*?)}}/g, (m, k) => data[k] || m);
```

## 子串包含
```JavaScript
const isContain = (a, b) => {
    for (let i = 0; i < a.length; i++) {
        if (a.slice(i, i + b.length) === b) return i
    }
    return -1
};
```
## 原型方法去重
```JavaScript
Array.prototype.clearRepeat = function () {
    let result = [];
    let repeat = [];
    this.forEach(v => result.includes(v) ? repeat.push(v) : result.push(v));
    this.splice(0);
    result.forEach(v => this.push(v));
    return repeat
};
```

## 参数排序
```JavaScript
function argumentsSort(){
    return [...arguments].sort((a,b)=>a-b)
}
```

## 十六进制转RGB
```JavaScript
const toRGB = string => {
    if (!/^#([0-9A-Fa-f]{3}|[0-9A-Fa-f]{6})$/.test(string)) return string
    let result = []
    if (string.length === 4) {
        let newString = []
        for (let i = 1; i < string.length; i++) {
            newString.push(string[i], string[i])
        }
        string = '#' + newString.join('')
    }
    for (let i = 0; i < string.length; i++) {
        if (i % 2 !== 0) {
            result.push(parseInt('0x' + string[i] + string[i + 1]))
        }
    }
    return 'rgb(' + result.join(',') + ')'
};
```
