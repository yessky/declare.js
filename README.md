# declare.js

<a href="https://github.com/yessky/declare.js" target="_blank">declare.js</a>使得JavaScript具备了多继承的能力。基于 <a href="https://www.python.org/download/releases/2.3/mro/" target="_blank">C3 Method Resolution Order</a> 算法实现，支持单/多/深度继承；支持菱形继承错误提示；仅一个api简单易用，继承关系清晰易读；体积小巧minify后约3kb，gzip后约1kb大小；性能优秀，占用不到1毫秒cpu时间。<a href="https://github.com/yessky/declare.js" target="_blank">declare.js</a>带你玩转JavaScript多继承。

# 用法示例

```
var X = declare('X', null, {
  constructor: function() {
    this.name = 'X';
    console.log('inherited X::constructor');
  },
  superName: 'X',
  superFn: function() {
    console.log('inherited X::superFn');
  }
});
var F = declare('F', [X], {
  constructor: function() {
    this.name = 'F';
    console.log('inherited F::constructor');
  },
  superName: 'F',
  superFn: function() {
    this.inherited(arguments);
    console.log('inherited F::superFn');
  },
  superFn2: function() {
    console.log('inherited F::superFn2');
  }
});
console.time('e')
var E = declare('E', [X], {
  constructor: function() {
    this.name = 'E';
    console.log('inherited E::constructor');
  },
  superName: 'E'
});
console.timeEnd('e')
console.time('d')
var D = declare('D', [X], {
  constructor: function() {
    this.name = 'D';
    console.log('inherited D::constructor');
  },
  superName: 'D'
});
console.timeEnd('d')
console.time('c')
var C = declare('C', [D, F], {
  constructor: function() {
    this.name = 'C';
    console.log('C');
  },
  superName: 'C'
});
console.timeEnd('c')
console.time('b')
var B = declare('B', [E, D], {
  constructor: function() {
    this.name = 'B';
    console.log('inherited B::constructor');
  },
  superName: 'B',
  superFn: function() {
    this.inherited(arguments);
    console.log('inherited B::superFn');
  }
});
console.timeEnd('b')
console.time('a')
var A = declare('A', [B, C], {
  constructor: function() {
    this.name = 'A';
    console.log('inherited A::constructor');
  },
  superName: 'A',
  superFn2: function() {
    this.inherited(arguments);
    console.log('inherited A::superFn2');
  }
});
console.timeEnd('a');
```