# ESMint
 Minteea个人ES项目的常用代码格式规则

## 概述
这里是Minteea个人常用的代码格式规则。因为这份规则是在ESLint基础上加上个人偏好修改的，所以我将它称为ESMint。

这份规则与ESLint规则相比，更加强调简洁、易写和易读性。

## 规则
### 缩进与换行
**代码缩进使用2个空格**
```
indent: ["error", 2]
```
eslint默认缩进是4个空格，但4空格缩进显得过于“扯裆”，而且缩进较多时容易占用很多横向空间，而两空格看起来像方块一样，较为舒适。
``` javascript
// 👎 4空格缩进
function fn(a) {
    if (a > -1 && a < 1) {
        if (a > 0) {
            return true
        } else {
            return false
        }
    }
}

// 👍 2空格缩进
function fn(a) {
  if (a > -1 && a < 1) {
    if (a > 0) {
      return true
    } else {
      return false
    }
  }
}
```

**换行符使用LF模式**
```
"linebreak-style": ["error", "unix"]
```
Unix系统里，每行行尾用`\n`换行(即LF)；而Windows系统里，每行行尾用`\r\n`换行(即CRLF)，为了保证不同平台代码格式的统一和换行的简洁，换行符统一设置为Unix(LF)模式。


### 符号

**行尾不添加分号**
```
semi: ["error", "never"]
```
分号一般表示一条语句的结束，分隔不同的两条语句。由于js具有自动插入分号机制(ASI)，一些语句的分号可以省略。因此有许多人在写代码时不在语句末尾添加分号。

然而，ASI机制也会遇到有歧义的情况，例如
``` javascript
let foo = bar
(1 || 2).baz()
// 以上语句会被解析为一条语句，而不是两条语句
let foo = bar(1 || 2).baz()
```
不过这样的情况并不常见

我认为每写一条语句就在结尾添加分号太麻烦了，而且代码里到处是分号显得不简洁，所以我，至于一些可能有ASI歧义的情况，在开头添加分号分隔就可以了。
``` javascript
// 👎 在语句结尾添加分号，这并不简洁
const pi = 3.14;
function getCircleArea(a) {
  let s = a ** 2 * pi;
  return s;
}

// 👍 省略分号是好文明
const pi = 3.14
function getCircleArea(a) {
  let s = a ** 2 * pi
  return s
}

// 👍 遇到以 ([{ 等开头的情况，可以在开头添加一个分号
let foo = bar
;(1 || 2).baz()
```

**非模板字符串使用双引号表示**
```
quotes: ["error", "double"]
```
双引号 `" "` 比单引号 `' '` 显眼且不刺眼，更适合用作字符串表示。
``` javascript
// 👎 单引号字符串
const str = '这是单引号字符串'

// 👍 双引号字符串
const str = "这是双引号字符串"
const str = "这是\"带双引号的\"双引号字符串"
```
### 运算符

