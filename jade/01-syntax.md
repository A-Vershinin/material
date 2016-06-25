# Основы синтаксиса в JADE
* [Декларация](#Декларация)
* [Теги](#Оформление-тегов)
* [Атрибуты](#Атрибуты)
* [Вложенность](#Вложенность)
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
вроде '&lt;img/&gt;' то оформлять их нужно следующим образом
```Jade
foo/
// html -> <foo/>
```

> Такие теги как img, meta, link
> закрывать вручную не нужно компилятор это сделает сам, если нужно

### Атрибуты
Все атрибуты можно оформлять в () скобках
```Jade
// Пример одиночного закрывающегося тега
foo(bar='baz')/
// html -> <foo bar="baz">

// Не стоит забывать, что jade - это движок шаблонов
// и он умеет исполнять операторы из js
- var authenticated = true
body(class=authenticated ? 'authed' : 'anon')
// html -> <body class="authed"></body>


// Если атрибутов много их можно переносить на новые строки
input(
  type='checkbox'
  name='agreement'
  checked
)
// html -> <input type="checkbox" name="agreement" checked="checked"/>
```

#### Атрибут class
Атрибут класс как и все может быть записал в () скобках,
но такую нотацию лучше использовать при динамических классах
```Jade
- var classes = ['foo', 'bar', 'baz']
a(class=classes)
// html -> <a class="foo bar baz"></a>
```
> Заметьте "-" в начале ключевого слова var является обязательным
> так компилятор определяет, что это инструкция для выполнения,
> без нее будет ошибка

А в остальных случаях проще использовать литералы класса
```Jade
a.foo.bar.baz
// html -> <a class="foo bar baz"></a>

// кроме класса литеральная нотация так же есть и у атрибута id
a#jadeLang.foo.bar.baz
// html -> <a id="jadeLang" class="foo bar baz"></a>
```

#### Атрибут style
Атрибут класс так же может быть записан в () как строка,
но атрибут так же принимает объект
```Jade
- var obj = {color: 'red', background: 'green'}
a(style=obj)
// html -> <a style="color:red;background:green"></a>

// или 

a(style={color: 'red', background: 'green'})
// html -> <a style="color:red;background:green"></a>
```

#### Миксин &attributes
Принимает объект из пар, где ключ - это название атрибута, а свойство - это его значение.
```Jade
- var attributes = {'data-foo': 'bar'};
div#foo(data-bar="foo")&attributes(attributes)
// html -> <div id="foo" data-bar="foo" data-foo="bar"></div>
```

### Вложенность
Иерархия в jade строится путем добавления отступов к тегу
```Jade
ul
	li Первый
	li Второй
	li Третий
// html ->
//<ul>
//  <li>Первый</li>
//  <li>Второй</li>
//  <li>Третий</li>
//</ul>	
```
Если нам в строчный элемент нужно положить еще один строчный мы можем использовать следующюю нотацию
```Jade
a(href="link"): img(src="linkForImage")
// html -> <a href="link"><img src="linkForImage"></a>
```

### Текстовый контент
У блочных элементов текстовый контент может быть оформлен несколькими способами
```Jade
// Первый способ
h1="<strong>Важный текст</strong>, а тут не очень важный"
// html -> <h1>&lt;strong&gt;Важный текст&lt;/strong&gt;, а тут не очень важный</h1>
// В таком случае <> - скобки оформляются как символы, а не как код

// Второй способ
h1!="<strong>Важный текст</strong>, а тут не очень важный"
// html -> <h1><strong>Важный текст</strong>, а тут не очень важный</h1>
// <> скобки будут обработаны парсером html и внутри у нас будут теги

// Третий способ
h1 <strong>Важный текст</strong>, а тут не очень важный
// html -> <h1><strong>Важный текст</strong>, а тут не очень важный</h1>
// Идентичен второму
```
Если первые два работают для многострочного текста сразу, то третий способ нужно немного изменить
```Jade
p.
	This way is shortest if you need big
	blocks of text spanning multiple
	lines.
// html -> 
//<p>
//  This way is shortest if you need big
//  blocks of text spanning multiple
//	lines.
//</p>
```