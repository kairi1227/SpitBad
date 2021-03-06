# ES6 学习
##1.export default
[What is “export default” in javascript?](http://stackoverflow.com/questions/21117160/what-is-export-default-in-javascript)

###方式一：
如果用，这种形式导出 `不export default`:
```javascript
module "foo" {
    export let x = 42;
}
```
就需要用这种形式引入:
```javascript
import { y } from "foo";
```
###方式二：
如果用，这种形式导出 `export default`:
```javascript
module "foo" {
    export default function() { console.log("hello!") }
}
```
就需要用这种形式引入:
```javascript
import foo from "foo";
foo(); // hello!
```
###相当于在import一个文件的时候，如果没有写特定的类像`import {abc} from ./abc`，可以直接导入 `./abc` 中default的类，否则就需要加上{}，但是导出时可以有default，也可以没有(react模块要求必须有)，代码可以像这样:
```javascript
//export, file name : abc.js
export default class ABC
export class DEF

//import abc.js
//这就引入了ABC这个default类以及DEF这个具体的类
import A, {D} from ./abc.js
```

* [React中导出模块为何必须要有export default](http://stackoverflow.com/questions/31852933/why-es6-react-component-works-only-with-export-default)

[harmony:modules](http://wiki.ecmascript.org/doku.php?id=harmony:modules)

##2.exports 和 module.exports 的区别
* 参考[exports 和 module.exports 的区别](https://cnodejs.org/topic/5231a630101e574521e45ef8)
* exports 是指向的 module.exports 的引用
* module.exports 初始值为一个空对象 {}，所以 exports 初始值也是 {}
* `require()`也就是`import` 返回的是 module.exports 而不是 exports

```javascript
  var name = 'nswbmw';
  exports.name = name;
  exports.sayName = function() {
    console.log(name);
  }
  //相当于
  var name = 'nswbmw';
  module.exports.name = name;
  module.exports.sayName = function() {
    console.log(name);
  }
```

基于此，在这里需要回答一个问题[用Babel6编译文件后，为何export default XXX之后，import它的时候，调用它需要 XXX.default](http://stackoverflow.com/questions/34736771/webpack-umd-library-return-object-default/34778391#34778391)

[中文答案](https://segmentfault.com/a/1190000004301150)
大致是说，因为缺少了，`modules.export = XXX` 所以，Babel6只支持import的写法，不再支持require()，并且不再支持`解构`([请戳我了解什么是ES6解构Destructuring](http://www.infoq.com/cn/articles/es6-in-depth-destructuring/))
区别代码如下：

`Babel6`在编译JS文件时，会将:
```javascript
export default XXX
//编译为
export.default = XXX
``` 
而在 `Babel5`的时候，会将:
```javascript
export default XXX
//编译为
/**注释的内容是上一行的另一种写法，更易懂*/
exports['default'] = XXX
// exports.default = XXX
module.exports = exports['default'];
//module.exports = exports.default;

//上面两行内容 也就是等于
exports.default = XXX
module.exports = XXX
```

`Babel6`在编译的时候，少了最后一行 `module.exports = XXX`
* 如果有这一行，说明继续支持require()的写法，也就是可以解构……
