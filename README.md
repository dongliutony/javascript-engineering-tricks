<div align="center">
  <img height="60" src="https://img.icons8.com/color/344/javascript.png"> 
  <h1>JavaScript Engineering Questions</h1>

---

<span>从基础理论到实战应用：测试一下你对Javascript掌握到什么程度了，更新你的知识体系，为你提供一些Javascript的工程参考，或者是为面试提前做准备。我会定期的更新这些问题，并给出我自己的理解。点击展开每道题下方的搜索区域，就可以看到我的答案。工程中的问题通常都有很多解决方案，我提供的答案只是其中一种在当前可行的方案。我会尽量采纳最佳时间，如果行业技术栈有更新，我会相应调整我的答案。让我们一起来做一些有意思的事情！:heart:</span>

欢迎联系我，一起将最佳Javascript最佳工程实践沉淀下来，传播出去! 😊 <br />
<a href="https://www.twitter.com/liudongtony">Twitter</a> || <a href="https://www.linkedin.com/in/dong-liu-45069b30/">LinkedIn</a>
</div>

---

###### 1. 怎么来共享一个拥有客户化配置的网页?（

场景描述：我们在开发一个报表网页，允许用户选择不同的参数来生成用户化的报表。现在，用户需要向其他人共享按照自己选择的参数生成的报表。

- A: 共享页面的URL，通过query string params来携带用户参数信息
- B: 按照RESTful原则，根据用户化页面生成unique URL来表示客户化页面资源,共享URL
- C: 将参数存储在JSON中，将URL和JSON共享
- D: 共享页面的URL，并且通过request header来携带用户参数信息

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

最主流的方案是直接共享URL，并且通过Query String参数来携带用户配置参数。这种方案实现简单，不需要在服务器端存储每次共享页面的信息（比如B方案，如果每次生成一个特定的URL,就需要服务器生成、存储、访问这些URL。在大多数场景下，不需要这么复杂的实现）。如果需要隐藏QS参数信息，可以在JS和服务器端做encoding/decoding处理。
B方案是可行的，但是在大多数场景下不推荐。缺点是实现复杂，额外占用服务器资源。好处是可以存储历史共享信息。

</p>
</details>
