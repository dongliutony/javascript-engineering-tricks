<div align="center">
  <img height="60" src="https://img.icons8.com/color/344/javascript.png"> 
  <h1>JavaScript Engineering Questions</h1>

---

<span>JS前端开发工程方法，从基础理论到实战应用：测试一下你对Javascript掌握到什么程度了，更新你的知识体系，为你提供一些Javascript的工程参考，或者是为面试提前做准备。我会定期的更新这些问题，并给出我自己的理解。点击展开每道题下方的搜索区域，就可以看到我的答案。工程中的问题通常都有很多解决方案，我提供的答案只是其中一种在当前可行的方案。我会尽量采纳最佳实践，如果行业技术栈有更新，我会相应调整我的答案。让我们一起来做一些有意思的事情！:heart:</span>

欢迎联系我，一起将Javascript最佳工程实践沉淀下来，传播出去! 😊 <br />
<a href="https://www.twitter.com/liudongtony">Twitter</a> || <a href="https://www.linkedin.com/in/dong-liu-45069b30/">LinkedIn</a>
</div>

---

###### 1. 怎么来共享一个拥有客户化配置的网页?

场景描述：我们在开发一个报表网页，允许用户选择不同的参数来生成用户化的报表。现在，用户需要向其他人共享按照自己选择的参数生成的报表。

- A: 共享页面的URL，通过query string params来携带用户参数信息
- B: 按照RESTful原则，根据用户化页面生成unique URL来表示客户化页面资源,共享URL
- C: 将参数存储在JSON中，将URL和JSON共享
- D: 共享页面的URL，并且通过request header来携带用户参数信息

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

最主流的方案是直接共享URL，并且通过Query String参数来携带用户配置参数。这种方案实现简单，不需要在服务器端存储每次共享页面的信息（比如B方案，如果每次生成一个特定的URL,就需要服务器生成、存储、访问这些URL。在大多数场景下，不需要这么复杂的实现）。如果需要隐藏QS参数信息，可以在JS和服务器端做encoding/decoding处理。另外，如果资源的数量多、访问量大，可以使用 short url server。
B方案是可行的，但是在大多数场景下不推荐。缺点是实现复杂，额外占用服务器资源。好处是可以存储历史共享信息。

</p>
</details>

---

###### 2. React组件怎么传入变量

场景描述：使用React组件时，多重父子组件嵌套可以复用组件，实现灵活调整。一个组件什么时候使用Global Store变量？


<details><summary><b>Answer</b></summary>
<p>

#### Answer: 父组件接入store，子组件只从父组件的props中拿变量，并触发dispatch action来修改变量（即单项数据流）。兄弟组件间通过父组件传递变量，并用回调函数修改变量。

注意：如果一个组件，同时从Global store和上级props来获取变量，那么因为props是一个对象，任何地方的调用都有可能修改props，从而使得props中的item被清空或者修改。这往往和我们的预期行为是不匹配的。

</p>
</details>

---

###### 3. 数组的常见操作（使用ES6+的原生方法）

场景描述：为下面的各种应用场景设计工程上可行的处理方式。

A. 找出2个数组的交集，并集，差集
```
// given:
let nums1 = [0, 2, 4, 6, 8, 8];
let nums2 = [1, 2, 3, 4, 5, 6];
// asked for:
[2, 4, 6], [0,2,4,6,8,1,3,5], [0,8]
```
B. 从array of obj映射出 array of value:
```
// given
let employees = [
    { name: 'Tom', age: 42, gender: 'M' },
    { name: 'David', age: 21, gender: 'M'  },
    { name: 'Matt', age: 32, gender: 'M'  },
    { name: 'Mary', age: 22, gender: 'F'  },
    { name: 'Monica', age: 21, gender: 'F'  },
    { name: 'Shally', age: 19, gender: 'F'  },
]
// asked for:
["Tom", "David", "Matt", "Mary", "Monica", "Shally"]
```
C. 清洗数组中的false值（包括false, 0， ""，null, NaN, undefined）
```
// given
let results = [0, 'negative', '', NaN, 9, true, undefined, 'high', false];
// asked for
["negative", 9, true, "high"]
```
D. 数组求和
```
// given
let nums = [1, 2, 3, 4, 5];
// asked for
15
```
E. 数组排序
```
// given
let nums = [3, 1, 2, 4, 5];
// asked for
[1, 2, 3, 4, 5]
```

<details><summary><b>Answer</b></summary>
<p>

#### Answer: 工程上可行的方案，应该是执行效率较高，代码易读，代码可以封装成通用方法。

A. 交集：先对nums1去重，在遍历nums1元素，将nums2也同时包含的元素作为filter条件。
```
let intersect = [...new Set(nums1)].filter(item => nums2.includes(item));
let combined = new Set([...nums1, ...nums2]);
let difference = new Set(nums1.filter(v => !nums2.includes(v)));
```
B. 使用JS内置的Array.from()方法
```
let names = Array.from(employees, ({name}) => name);
```
C. 将Boolean作为filter条件
```
let cleaned = results.filter(Boolean)
```
D. 使用Array.reduce()方法
```
let sum = nums.reduce((x, y) => x + y, 0);
```
E. 使用Array.sort()方法，注意自定义排序函数的使用
```
let sorted = nums.sort((a, b) => a-b); // 如果需要倒序，则排序函数是 b-a
```
</p>
</details>

---

