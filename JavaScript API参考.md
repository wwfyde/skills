# JavaScript API参考

# JavaScript

## document.querySelector() - [N](https://developer.mozilla.org/zh-CN/docs/Web/API/Document/querySelector)

档对象模型[`Document`](https://developer.mozilla.org/zh-CN/docs/Web/API/Document)引用的`querySelector()`方法返回文档中与指定选择器或选择器组匹配的第一个 html元素[`Element`](https://developer.mozilla.org/zh-CN/docs/Web/API/Element)。 如果找不到匹配项，则返回`null`。

**提示**: 匹配是使用深度优先先序遍历，从文档标记中的第一个元素开始，并按子节点的顺序依次遍历。

```js
var element = document.querySelector(selectors);


var el = document.querySelector(".myclass");
```

### 参数

- `selectors`

  包含一个或多个要匹配的选择器的 DOM字符串[`DOMString`](https://developer.mozilla.org/zh-CN/docs/Web/API/DOMString)。 该字符串必须是有效的CSS选择器字符串；如果不是，则引发`SYNTAX_ERR`异常。请参阅[使用选择器定位DOM元素](https://developer.mozilla.org/zh-CN/docs/Web/API/Document_Object_Model/Locating_DOM_elements_using_selectors)以获取有关选择器以及如何管理它们的更多信息。

**提示:**必须使用反斜杠字符转义不属于标准CSS语法的字符。 由于JavaScript也使用退格转义，因此在使用这些字符编写字符串文字时必须特别小心。 有关详细信息，请参阅[Escaping special characters](https://developer.mozilla.org/zh-CN/docs/Web/API/Document/querySelector#Escaping_special_characters)。

### 返回值



表示文档中与指定的一组CSS选择器匹配的第一个元素的 html元素[`Element`](https://developer.mozilla.org/zh-CN/docs/Web/API/Element)对象。

如果您需要与指定选择器匹配的所有元素的列表，则应该使用[`querySelectorAll()`](https://developer.mozilla.org/zh-CN/docs/Web/API/Document/querySelectorAll) 。

## Document.querySelectorAll()- [N](https://developer.mozilla.org/zh-CN/docs/Web/API/Document/querySelectorAll)

返回与指定的选择器组匹配的文档中的元素列表 (使用深度优先的先序遍历文档的节点)。返回的对象是 [`NodeList`](https://developer.mozilla.org/zh-CN/docs/Web/API/NodeList) 。

### Syntax - 语法

```
elementList = parentNode.querySelectorAll(selectors);
```

### 参数



- `selectors`

  一个 [`DOMString`](https://developer.mozilla.org/zh-CN/docs/Web/API/DOMString) 包含一个或多个匹配的选择器。这个字符串必须是一个合法的 [CSS selector](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors) 如果不是，会抛出一个 `SyntaxError` 错误。有关使用选择器标识元素的更多信息，请参阅 [Locating DOM elements using selectors](https://developer.mozilla.org/en-US/docs/Web/API/Document_object_model/Locating_DOM_elements_using_selectors) 可以通过使用逗号分隔多个选择器来指定它们。

**注意：** 必须使用反斜杠字符转义不属于标准CSS语法的字符。 由于JavaScript也使用反斜杠转义，因此在使用这些字符编写字符串文字时必须特别小心。 有关详细信息，请参阅 [Escaping special characters](https://developer.mozilla.org/zh-CN/docs/Web/API/Document/querySelectorAll#Escaping_special_characters)

### 返回值



一个静态 [`NodeList`](https://developer.mozilla.org/zh-CN/docs/Web/API/NodeList)，包含一个与至少一个指定选择器匹配的元素的[`Element`](https://developer.mozilla.org/zh-CN/docs/Web/API/Element)对象，或者在没有匹配的情况下为空[`NodeList`](https://developer.mozilla.org/zh-CN/docs/Web/API/NodeList)

**注意：** 如果`selectors`参数中包含 [CSS伪元素](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-elements)，则返回的列表始终为空。



## document.getElementByID()

```js
var element = document.getElementById(id);
var element = document.getElementById("app")
```

## document.getElementsByClassName()

## document.getElementsByTagName()

## document.getElementsByName()



# Web API

## Window

### setInterval - [重复调用](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/setInterval)



```js
var intervalID = scope.setInterval(func, delay, [arg1, arg2, ...]);  //推荐
var intervalID = scope.setInterval(code, delay);  // 存在安全风险
// args 传递给函数的附加参数

```

```
func
```

要重复调用的函数。A [`function`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/function) to be executed every `delay` milliseconds. The function is not passed any arguments, and no return value is expected.

code

这个语法是可选的，你可以传递一个字符串来代替一个函数对象，你传递的字符串会被编译然后每个delay毫秒时间内执行一次。这个语法因为存在安全风险所以不被推荐使用。

```
delay
```

是每次延迟的毫秒数 (一秒等于1000毫秒)，函数的每次调用会在该延迟之后发生。和[setTimeout](https://developer.mozilla.org/en-US/docs/DOM/window.setTimeout#Minimum_delay_and_timeout_nesting)一样，实际的延迟时间可能会稍长一点。这个时间计算单位是毫秒（千分之一秒），这个定时器会使指定方法或者代码段执行的时候进行时间延迟。如果这个参数值小于10，则默认使用值为10。请注意，真正延迟时间或许更长； 请参考示例： [Reasons for delays longer than specified](https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/setTimeout#Reasons_for_delays_longer_than_specified) in [WindowOrWorkerGlobalScope.setTimeout()](https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/setTimeout) 

`arg1, ..., argN` 可选

当定时器过期的时候，将被传递给func指定函数的附加参数。

# Jquery

## Selector.toggleClass('main')