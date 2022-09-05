# 8个console.log的解决方案

console.log 很棒，它可能是我们日常开发中最常用的方法之一。但实际上，控制台对象中也有一些很棒的方法，它们可以帮助我们在控制台中打印出更清晰漂亮的消息。

![图片](https://mmbiz.qpic.cn/mmbiz_png/eXCSRjyNYcYsBCKtX8fnUFgcEon2jD0w3059uz4jZmLK2OeTQ785XHDYw9HMma5b42srxcvB6V4597auecKJVw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

在今天的文章中，我就来分享一些有关控制台的高级技巧，我们现在开发吧。

**日志记录级别：调试、信息、警告、错误**

不同的事件根据其重要性具有不同的日志记录级别，通常有四个日志级别：调试→信息→警告→错误，他们在控制台对象中有对应的方法：

![图片](https://mmbiz.qpic.cn/mmbiz_png/eXCSRjyNYcYsBCKtX8fnUFgcEon2jD0w2wUzlsUWHyKibmKcz5hFia08qsTS6RBKZkhcKTNc5XajLGfxicibJEZqOg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

用法：

- 
- 
- 
- 

```
console.debug('Debug message');console.info('Useful information');console.warn('This is a warning');console.error('Something went wrong!');
```

输出：

![图片](https://mmbiz.qpic.cn/mmbiz_png/eXCSRjyNYcYsBCKtX8fnUFgcEon2jD0wkYpJTA5FAicmZ1397nAGAtK2HwZRnZ0McBjXAHXY3ib0FfQ6o8224oAQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

- 默认情况下，console.debug 打印的消息不会出现在控制台上。
- console.info 等于 console.log 。
- console.warn 将打印黄色警告样式消息。
- console.error 将打印一条红色错误样式消息。

当我们需要打印特殊消息时，可以使用这些方法代替 console.log ，它将使消息清晰。

此外，如果我们使用不同的日志记录级别，我们可以过滤消息：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/eXCSRjyNYcYsBCKtX8fnUFgcEon2jD0wJbWSkicLoDp1ghTn4SwIu2byHw5aDiciaCceQlOQBIq3Ld0vcxlQN0KrA/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

在这种情况下，Verbose等于debug。

**以精美的样式输出消息**

如果要在打印的消息中添加 CSS 样式，只需在字符串前添加 %c 并将 CSS 样式作为另一个参数传递：

- 
- 

```
console.log('%c Hi everyone!', 'color: red; font-size: 18px');console.log('%c hello world', 'color: #1c03fc; font-size: 18px');
```

![图片](https://mmbiz.qpic.cn/mmbiz_png/eXCSRjyNYcYsBCKtX8fnUFgcEon2jD0wuwg9qnUFImhGLqotMg88XqibcG11Y3M8Tk7Ywvz3yhxymSflOG596iaQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**在控制台输出图像**

另一个有趣的事情是，我们可以在控制台中输出图像，我们只需要设置 background-img 属性。

例子：

- 
- 
- 
- 
- 
- 

```
console.log(        "%c  ",        `background: url(https://cdn-images-1.medium.com/fit/c/64/64/1*XYGoKrb1w5zdWZLOIEevZg.png) no-repeat;         font-size:130px;         line-height: 64px`      )
```

结果：

![图片](https://mmbiz.qpic.cn/mmbiz_png/eXCSRjyNYcYsBCKtX8fnUFgcEon2jD0wKib9uicSJoHNF2leek11ny8vH2qqLTJSeEEdldQlElNNWr37dxw383SQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

- 由于控制台不支持 <img> 标签，我们使用背景图片代替。
- 另外，控制台不支持宽高，所以我们用空格和字体大小来代替；

**console.table()**

假设我们要打印一些对象，如果像这样直接使用console.log：

- 
- 
- 
- 
- 

```
let user1 = { name: 'bytefish', tech: 'JavaScript', age: 99 }let user2 = { name: 'Jon', tech: 'CSS', age: 55}let user3 = { name: 'Bob', tech: 'HTML', age: 22 }
console.log(user1, user2, user3)
```

它有效，但不清楚：

![图片](https://mmbiz.qpic.cn/mmbiz_png/eXCSRjyNYcYsBCKtX8fnUFgcEon2jD0wuibSdJqgJvIkY07RMhl0y0UaBAhyY2XB6uVicDPeXWzoePPs5JqjGkcQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

更好的选择是使用 console.table 在表格中打印它们：

![图片](https://mmbiz.qpic.cn/mmbiz_png/eXCSRjyNYcYsBCKtX8fnUFgcEon2jD0wMR3rKkBzmV9eGr3kGIL1DjfWicw9yGknAGohjCDhkpTU9k4kMBWgD6A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**console.****trace()**

在调试深度嵌套的函数时，我们可能还想输出代码的堆栈跟踪。console.trace() 方法将帮助我们输出堆栈跟踪。

![图片](https://mmbiz.qpic.cn/mmbiz_png/eXCSRjyNYcYsBCKtX8fnUFgcEon2jD0wLh0tesudjACOCS784mHuXZ4ggFq6ocvPwHgxV80qJ6iabYRuWj3QUzw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如果我们仍然使用 console.log ，我们将无法再观察程序调用堆栈：

![图片](https://mmbiz.qpic.cn/mmbiz_png/eXCSRjyNYcYsBCKtX8fnUFgcEon2jD0wx8MhZzbElPyibBLr8uG0qVr90whpxYhOwOcXh9MYca37uJd1KQZ6j3A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**console.time()**

当我们需要跟踪一个操作需要多长时间时，我们可以使用 console.time() ，它会启动一个计时器。

我们为每个计时器指定一个唯一的名称，并且在给定页面上最多可以运行 10,000 个计时器。

当我们使用相同的名称调用 console.timeEnd() 时，浏览器将输出自计时器启动以来经过的时间（以毫秒为单位）。

![图片](https://mmbiz.qpic.cn/mmbiz_png/eXCSRjyNYcYsBCKtX8fnUFgcEon2jD0w3QZzwiawBZtPo7hS5QQXW3wwryKIYVoWaiadcLOMH7jmDB4Iv69QDuCw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**console.count()**

当我们需要计算一段代码执行了多少次时，我们可以使用 console.count 。console.count() 方法记录了这个对 count() 的特定调用被调用的次数。

例如，如果我们想计算一个斐波那契函数被调用了多少次，那么我们可以编写如下代码：

- 
- 
- 
- 
- 
- 

```
function fibonacci(num) {  console.count('fibonacci function has been executed')  if (num <= 1) return 1;  return fibonacci(num - 1) + fibonacci(num - 2);}fibonacci(10)
```

![图片](https://mmbiz.qpic.cn/mmbiz_png/eXCSRjyNYcYsBCKtX8fnUFgcEon2jD0w8Av6WJibKhLAvUnTr3T6Z4XMpKicXBzWjKYDYeqeW9ibwgcAsgBjxzq5A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

当我们需要计算组件在 React 或 Vue 中渲染或更新的次数时，我们也可以使用 console.count，所以你不需要自己实现一个计数器。

**console.assert()**

使用 console.assert()，我们可以决定只在条件为假时记录一些内容，并通过避免不必要的消息打印来节省一些控制台空间：

**console.group()**

我们可以使用嵌套组通过视觉关联相关消息来帮助组织您的输出。要创建新的嵌套块，请调用 console.group()。

console.groupCollapsed() 方法类似，但是新块是折叠的，需要点击一个公开按钮才能阅读。

- 
- 
- 
- 
- 
- 
- 
- 
- 
- 

```
console.log("This is the outer level");console.group();    console.log("Level 2");    console.group();        console.log("Level 3");        console.warn("More of level 3");    console.groupEnd();console.log("Back to level 2");console.groupEnd();console.log("Back to the outer level");
```

![图片](https://mmbiz.qpic.cn/mmbiz_png/eXCSRjyNYcYsBCKtX8fnUFgcEon2jD0wlL2PKg8sAe6S96el32LaO781uMXZFLtGYJ5khibZ82ekc22ia0ibPegNA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)