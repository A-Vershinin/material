# Основы синтаксиса в JADE
* [Декларация](http://github.com/)
* [Теги]()
* [Атрибуты]()
* [Вложенность]()
* [Контент]()

```Jade
```

### Декларация 
```Jade
// html5 doctype
doctype html

// svg doctype
doctype svg PUBLIC "-//W3C//DTD SVG 1.1//EN" "http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd"
```
> Объявление других деклараций отличных от
> html5 повлияет на рендер элементов

```javascript
var jade = require('./');

// Compile a function
var fn = jade.compile('img(src="foo.png")', {doctype: 'xml'});

// Render the function
var html = fn({});
// => '<img src="foo.png"></img>'

// Compile a function
var fn = jade.compile('img(src="foo.png")', {doctype: 'html'});

// Render the function
var html = fn({});
// => '<img src="foo.png">'

``` 

### Оформление тегов
Теги оформляются без скобок и без закрывающего тега

```Jade
img 
// html -> <img>
```

Если у вас одиночный тег который нужно закрыть 
вроде <img/> то оформялть их нужно следующим образом

```Jade
foo/
// htlm -> <foo/>
```

> Такие теги как img, meta, link
> закрывать вручную не нужно компилятор это сделает сам, если нужно