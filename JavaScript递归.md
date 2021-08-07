# JavaScript递归

### 1. 概念

就是函数自己调用自己本身，或者在自己函数调用的下级函数中调用自己。

> **注意：**使用递归函数一定要注意，处理不当就会进入死循环。递归函数只有在特定的情况下使用 ，比如阶乘问题。

### 2. 递归的思路

写一个函数 `pow(x, n)`，它可以计算 `x` 的 `n` 次方。换句话说就是，`x` 乘以自身 `n` 次

#### 2.1 迭代思路：使用 `for` 循环

```js
function pow(x, n) {
  let result = 1;

  // 再循环中，用 x 乘以 result n 次
  for (let i = 0; i < n; i++) {
    result *= x;
  }

  return result;
}

alert( pow(2, 3) ); // 8
```

#### 2.2 递归思路：简化任务，调用自身

```js
function pow(x, n) {
  if (n == 1) {
    return x;
  } else {
    return x * pow(x, n - 1);
  }
}

alert( pow(2, 3) ); // 8
```

**递归的分支：**

![image-20210612110248799](https://calvin-typora-image.oss-cn-hangzhou.aliyuncs.com/img/20210612110250.png)

**递归步骤：**

`pow` 递归地调用自身 直到 `n == 1`

<img src="https://calvin-typora-image.oss-cn-hangzhou.aliyuncs.com/img/20210612110409.png" alt="image-20210612110407173" style="zoom: 33%;" />

### 3. 案例

#### 3.1 求和

编写一个函数，输入值参数n，求n到1的和

```js
// 求 1-100 的和
var sum = 0;

function sumNum (n) {
  if ( n == 1 ) return 1;
  return n + sumNum(n-1);
}

console.log(sumNum(100)); // 5050
```

#### 3.2 斐波拉契数列

1,1,2,3,5,8,13,21,34,55,89...求第 n 项

```js
// 递归
// 1,1,2,3,5,8,13,21,34,55,89...求第 n 项
function Fibonacci (n) {
  if ( n == 1 ) return 1;
  if ( n == 2 ) return 1;
  return Fibonacci( n - 2 ) + Fibonacci ( n - 1 );
}

// 非递归
function FibonacciTwo (n) {
  let a = 0;
  let b = 1;
  let c = a + b;
  for ( let i = 3 ; i <= n ; i++ ) {
    a = b ;
    b = c ;
    c = a + b;
  }
  return c;
}

console.log(Fibonacci(10)); // 55
console.log(FibonacciTwo(10));  // 55
```

#### 3.3 多叉树

Json文件：

```js
headerData: {
                name: '总数据',
                children: [
                    {
                        name: '数据1',
                        children: [
                            {
                                name: '数据11',
                                children: [
                                    {
                                        name: '数据111',
                                    },
                                    {
                                        name: '数据112',
                                    }
                                ]
                            },
                            {
                                name: '数据12',
                                children: [
                                    {
                                        name: '数据121',
                                    },
                                    {
                                        name: '数据122',
                                    }
                                ]
                            },
                            {
                                name: '数据13',
                                children: [
                                    {
                                        name: '数据131',
                                    },
                                    {
                                        name: '数据132',
                                    }
                                ]
                            },
                            {
                                name: '数据14',
                            },

                        ]
                    }
                ]
            }
```

js文件：

```js
$.ajax({
  type: 'get',
  url: '03.json',
  dataType: 'json',
  success:function (data) {
    console.log(data);  // {name: "总数据", children: Array(1)}
    console.log(getLeafCountTree(data));  // 7
  },
  error:function () {
    console.log('失败')
  }
})

var x = {};

console.log(!x.x); // true   x.x -> undefined
// ！可将变量转换成boolean类型
// null、undefined和空字符串取反都为true其余都为false

function getLeafCountTree(json) {
  if (!json.children) return 1;
  // ！可将变量转换成boolean类型，null、undefined和空字符串取反都为true其余都为false
  var leafCount = 0;
  for (let i = 0 ; i < json.children.length ; i ++ ) {
    leafCount = leafCount + getLeafCountTree(json.children[i])
  }
  return leafCount;
}
```

### 4. 递归的数学解释

![image-20210627164730896](https://calvin-typora-image.oss-cn-hangzhou.aliyuncs.com/img/20210627164735.png)