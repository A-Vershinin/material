# Описание правил для style lint

Style lint имеет более 100 правил для настройки линтера. Сам файл .stylelintrc содержить обычный js объект в котором хранятся все эти правила. Здесь описаны большинство правил по типу.

` Название правила : Возможные варианты ` - описание

### Правила для цвета

* `color-hex-case : "lower" || "upper"` - Указание HEX цвета в определенном регистре.
```scss
  color: #FFF; // -> 'upper'
  background: #fff; // -> 'lower'
```

* `color-hex-length : "short" || "long"` - Указание длины цвета.
```scss
  color: #FFF; // -> 'short'
  background: #ffffff; // -> 'long'
```
> При этом в short должны быть цвета, которые нельзя указать коротко. Например: #a4a4a4

* `color-named : "always-where-possible"  || "never"` - Указание цвета в словах
 ```scss
  color: black; // -> '"always-where-possible'
  background: #fff; // -> 'never'
  ```

* `color-no-hex : true` - Запрещает использовать HEX цвета, это из правил, которые нужно указывать если они нужны, а если нет, то указывать не нужно.
 ```scss
  color: black; // -> '"always-where-possible'
  background: #fff; // -> 'never'
  ```

* `color-no-invalid-hex : true` - Показывает ошибку при невалидном HEX цвете.
 ```scss
  color: black; // -> '"always-where-possible'
  background: #fff; // -> 'never'
  ```
  ---

### Объявление font-family

* `font-family-name-quotes : "always-where-required" || "always-where-recommended" || "always-unless-keyword"` - Указание ковычек при объявления шрифта
```scss
font-family: "Times New Roman", "Times", serif; // -> 'always-unless-keyword'
font-family: "Hawaii 5-0", Times New Roman, Times, serif; // -> 'always-where-required'
font-family: 'Times New Roman', Times, serif; // -> 'always-where-recommended'
```
---

### Объявление font-weight

* `font-weight-notation : "numeric" || "named-where-possible"` - Указание толщины шрифта
```scss
a { font-weight: 700; } // -> 'numeric'
a { font-weight: bold; } // -> 'named-where-possible'
```
---

### Объявление Function

* `function-blacklist : array|string: '["scale", "rgba", "linear-gradient"]' || "scale"` - Указание фукнций которые не должны быть использованы в css
```scss
a { transform: scale(1); } // -> Error
a { background: -moz-linear-gradient(45deg, blue, red); } // -> Error
a { background: red; } -> Success
```
---

* `function-calc-no-unspaced-operator : "true"` - Указание пробелов при использовании функции calc
```scss
a { top: calc(calc(1em * 2) / 3); }
margin-top: calc(var(--some-variable) + var(--some-other-variable));
```
---

* `function-comma-newline-after : "always" || "always-multi-line" || "never-multi-line"` - Переход на новую строку **после** запятой при использовании функций с несколькими аргументами, если селектор описывается в одну или несколько строк

  ```scss
  a {
    transform: translate(1
      1)
  } // -> always

  a { transform: translate(1,1) } // -> always-multi-line
  a {
    transform: translate(1,
      1)
  } // -> always-multi-line

  a { transform: translate(1, 1) } // -> never-multi-line
  ```
---

* `function-comma-newline-after : "always" || "always-multi-line" || "never-multi-line"` - Переход на новую строку **до** запятой при использовании функций с несколькими аргументами, если селектор описывается в одну или несколько строк

  ```scss
  a {
    transform: translate(1
      ,1)
  } // -> always

  a { transform: translate(1,1) } // -> always-multi-line
  a {
    transform: translate(1
      ,1)
  } // -> always-multi-line

  a {
    transform: translate(1,
      1)
  } // -> never-multi-line
  ```
---

* `function-comma-space-after : "always" || "never" || "always-single-line" || "never-single-line"` - Указание пробела **после** запятой при использовании функции с несколькими аргументами
```scss
a { transform: translate(1, 1) } -> always
a { transform: translate(1,1) } -> never
a { transform: translate(1, 1) } -> always-single-line
a { transform: translate(1,1) } -> never-single-line
```
---

* `function-comma-space-before : "always" || "never" || "always-single-line" || "never-single-line"` - Указание пробела **до** запятой при использовании функции с несколькими аргументами
```scss
a { transform: translate(1 ,1) } -> always
a { transform: translate(1,1) } -> never
a { transform: translate(1 ,1) } -> always-single-line
a { transform: translate(1,1) } -> never-single-line
```
---

* `function-linear-gradient-no-nonstandard-direction : "true"` - указание линейного градиента по стандартной нотации
```scss
.foo { background: linear-gradient(to top, #fff, #000); } // Ключевый словом является to
.foo { background: linear-gradient(left, #fff, #000); } -> Error
```
---

* `function-max-empty-lines : int : 0` - указание максимального количества пустых строк между аргументами функции
```scss
a {
  transform:
    translate(
      1,
      1
    );
} -> 0
```
---

* `function-name-case : "lower" || "upper"` - Регистр имен функций
```scss
a { width: calc(5% - 10em); } -> lower
a { width: CALC(5% - 10em); } -> upper
```
---

* `function-parentheses-newline-inside : "always" || "always-multi-line" || "never-multi-line"` - Отступ на новую линию после открывающей и перед закрывающей скобками функции
```scss
a {
  transform: translate(
    1, 1
  );
} -> always
a {
  transform: translate(
    1, 1
  );
} -> always-multi-line
a { transform: translate(1, 1) } -> never-multi-line
```
---

* `function-parentheses-space-inside : "always" || "never" || "always-single-line" || "never-single-line"` - Пробел после открывающей и перед закрывающей скобками функции
```scss
a { transform: translate( 1, 1 ); } -> always
a { transform: translate(1, 1); } -> never
a { transform: translate( 1, 1 ) } -> always-single-line
a { transform: translate(1, 1) } -> never-single-line
```
---

* `function-url-data-uris : "always" || "never"` - Использование base64 формата для URL
```scss
a {
  background-image: url('data:image/gif;base64,R0lGODlhAQABAIAAAAUEBAAAACwAAAAAAQABAAACAkQBADs=')
} -> always
a {
  background-image: url(image.gif)
} -> never
```
---

* `function-url-no-scheme-relative : "true"` - Запрещает указание URL начинающегося с **//**
```scss
a {
  background: url("../file.jpg");
} -> true
a {
  background: url("//www.google.com/file.jpg");
} -> Error
```
---

* `function-url-quotes : "always" || "never"` - Указание ковычек при указании URL
```scss
a { background: url('x.jpg'); } -> always
a { background: url(x.jpg); } -> never
```
---

* `function-whitelist : array|string: ["scale", "rgba", "linear-gradient"]` - Белый лист функций (все функции не входящие в этот список запрещаются к использованию)
```scss
a { transform: scale(1); } -> true
a { transform: rotate(1); } -> Error
```
---

* `function-whitespace-after : "always" || "never"` - Использование пробела между несколькими функциями в одном свойстве
```scss
a { transform: translate(1, 1) scale(3); } -> always
a { transform: translate(1, 1)scale(3); } -> never
```
---

### Правила для Number

* `number-leading-zero : "always" || "never"` - Указание нуля в десятичных цифрах
```scss
a { line-height: 0.5; } -> always
a { line-height: .5; } -> never
```
---

* `number-max-precision : int : 1` - Кол-во цифр после точки
```scss
.foo { top: 3.24px; } -> 2
```
---

* `number-no-trailing-zeros : "true"` - Запрещает использование ненужных нулей
```scss
a { top: 1.0px } -> Error
a { top: 1px } -> true
```
---

### Правила для string

* `string-no-newline : "true"` - Запрещает использование перехода на новую строку
```scss
a {
  content: "first
    second";     
} -> Error
a { content: "first\Asecond" } -> true
```
---

* `string-quotes : "single" || "double"` - Правило задает указание ковычек при использовании строк
```scss
a { content: 'x'; } -> single
a { content: "x"; } -> double
```
---

### Правила для length

* `length-zero-no-unit : "true"` - Запрещает использование единиц измерения при указании 0
```scss
a { top: 0px } -> Error
a { top: 0 } -> true
```
---

### Правила для Time

* `time-no-imperceptible : "true"` - Запрещает использование времени меньше 100ms
```scss
.foo { animation: 80ms; } -> Error
.foo { animation: 8s; } -> True
```
---

### Правила для единиц измерения

* `unit-blacklist : ["array", "of", "units"] || "unit"` - запрещает использовать единицы измерения
```scss
/*
unit-blacklist : "em"
*/

.foo { font-size: 1.5em } -> Error
```

* `ignoreProperties: { unit: ["property", "/regex/"] }` - Дополняет `unit-blacklist` и разрешает использовать единицы для некоторых свойств
```scss
/*
ignoreProperties: {
  "px": [ "font-size", "/^border/" ],
  "vmin": [ "width" ]  
}
*/

a { font-size: 13px; } -> True
a { line-height: 12px; } -> Error
```

* `unit-case : "lower" || "upper"` - регистр единиц измерения
```scss
a { width: 10px } -> lower
a { width: 10PX } -> upper
```

* `unit-no-unknown : true` - запрещает использовать единицы измерения не описаные в специкации css
```scss
a { width: 100pixels } -> Error
```

* `ignoreUnits : ["/regex/", "string"]` - Дополняется свойство `unit-no-unknown` разрешая использовать перечисленные свойства
```scss
/*
ignoreUnits: ['custom']
*/

a { width: 10custom } -> True
```

* `unit-whitelist : ["array", "of", "units"] || "string"` - разрешает использовать указанные свойства
```scss
/*
unit-whitelist : ["px", "em", "deg"]
*/

a { width: 100%; } -> Error
a { height: 100px; } -> True
```

### Правила для значений свойств

* `value-keyword-case : "lower"|"upper"` - регистр значений
```scss
a { display: Block } -> Error
a { display: block } -> lower
a { display: BLOCK } -> upper
```

* `value-no-vendor-prefix : true` - Запрещает использовать вендорные префиксы для значений
```scss
a { display: -webkit-flex; } -> Error
```

### Правила для множественных свойств

* `value-list-comma-newline-after : "always" || "always-multi-line" || "never-multi-line"` - использование перехода на новую строку после запятой
```scss
a { background-size: 0,
      0; } -> always

a { background-size: 0, 0; } -> never-multi-line

// always-multi-line - разрешает использовать синтаксис и из always и из never-multi-line
```

* `value-list-comma-newline-before : "always" || "always-multi-line" || "never-multi-line"` - использование перехода на новую строку перед запятой
```scss
a { background-size: 0
      , 0; } -> always

a { background-size: 0,0; } -> never-multi-line
// always-multi-line - разрешает использовать синтаксис и из always и из never-multi-line
```

* `value-list-comma-space-after : "always" || "never" || "always-single-line" || "never-single-line"` - использование пробела после запятой
```scss
a { background-size: 0, 0; } -> always || always-single-line

a { background-size: 0
      , 0; } -> always || always-single-line || never-single-line

a { background-size: 0,0; } -> never || never-single-line

a { background-size: 0
      ,0; } -> never || always-single-line || never-single-line

```

* `value-list-comma-space-after : "always" || "never" || "always-single-line" || "never-single-line"` - использование пробела перед запятой
```scss
a { background-size: 0 ,0; } -> always || always-single-line

a { background-size: 0 ,
      0; } -> always || always-single-line || never-single-line

a { background-size: 0,0; } -> never || never-single-line

a { background-size: 0
      , 0; } -> never || always-single-line || never-single-line
```

* `value-list-max-empty-lines : int` - возможное кол-во пустых строк
```scss
/*
value-list-max-empty-lines : 0
*/

a {
  padding: 10px

    10px
    10px
    10px
} -> Error

a {
  padding: 10px
    10px
    10px
    10px
} -> True

a { padding: 10px 10px 10px 10px } -> True
```

### Правила для кастомных свойств

* `custom-property-empty-line-before : "always" || "never"` - использование пустой строки перед кастомным свойством
```scss
a {
  top: 10px;
  --foo: pink;
  --bar: red;
} -> never

a {
  top: 10px;

  --foo: pink;

  --bar: red;
} -> always
```

* `custom-property-no-outside-root : true` - запрещает использовать кастомные свойства без `:root`
```scss
:root { --foo: 1px; } -> true
:root, a { --foo: 1px; } -> error
a { --foo: 1px; } -> Error
```

* `custom-property-pattern : regex|string` - паттерн для имени кастомного свойства
```scss
/*
custom-property-pattern: "foo-.+"
*/

:root { --boo-bar: 0; } -> Error
:root { --foo-bar: 0; } -> True
```

### Правила для короткого описания свойст
* `shorthand-property-no-redundant-values : true` - запрещает использовать излишние символы в свойствах:
`margin`
`padding`
`border-color`
`border-radius`
`border-style`
`border-width`

```scss
a { margin: 1px 1px; } -> Error
a { margin: 1px; } -> True
```

### Привила для свойтс

* `property-blacklist : ["array", "of", "unprefixed", "properties" or "regex"] || "property" || "/regex/"` - запрещает использовать данные свойства

```scss
/*
property-blacklist : [ "text-rendering", "animation", "/^background/" ]
*/

a { text-rendering: optimizeLegibility; } -> Error
```

* `property-case : "lower" || "upper"` - регистр названий свойств
```scss
a { width: 1px } -> lower
a { WIDTH: 1px } -> upper
```

* `property-no-unknown : true` - запрещает использовать свойства которые не указаны в спецификации CSS, но игнорируется переменные ($sass, @less, --custom-property)
```scss
a { colr: blue } -> Error
a { color: blue } -> True
```

* `property-no-vendor-prefix : true` - запрещает использовать вендорные префиксы в именах свойств
```scss
a { -webkit-transform: scale(1); } -> Error
a { transform: scale(1); } -> True
```

* `property-whitelist : ["array", "of", "unprefixed", "properties" or "regex"] || "property" || "/regex/"` - разрешает использовать указанные свойства
```scss
/*
property-whitelist: ["display", "animation", "/^background/"]
*/

a { color: pink; } -> Error
a { display: block; } -> True
a { -webkit-animation: my-animation 2s; } -> True
```

### Правила для keyframe правила

* `keyframe-declaration-no-important : true` - Запрещает использовать `!important` в keyframe
```scss
@keyframes important1 {
  from {
    margin-top: 50px;
  }
  to {
    margin-top: 100px !important;
  }
} -> Error

@keyframes important1 {
  from {
    margin-top: 50px;
  }
  to {
    margin-top: 100px;
  }
} -> True
```

### Правила для разных деклараций свойств

* `declaration-bang-space-after : "always" || "never"` - Пробел перед знаком ! в декларации `!important`
```scss
a { color: pink ! important; } -> always
a { color: pink !important; } -> never
```

* `declaration-bang-space-before : "always" || "never" ` - Пробел после знаком ! в декларации `!important`
```scss
a { color: pink !important; } -> always
a { color: pink!important; } -> never
```

* `declaration-colon-newline-after : "always" || "always-multi-line" ` - переход на новую строку в свойствах где значений может быть несколько
```scss
a {
  color:
    pink;
} -> always

a {
  box-shadow:
    0 0 0 1px #5b9dd9,
    0 0 2px 1px rgba(30, 140, 190, 0.8);
} -> always-multi-line

a {
  color: pink;
} -> always-multi-line
```

* `declaration-colon-space-after : "always" || "never" || "always-single-line"` - пробел после символа ':' в объявлении свойства
```scss
a { color: pink } -> always
a { color:pink } -> never
a {
  box-shadow:
    0 0 0 1px #5b9dd9,
    0 0 2px 1px rgba(30, 140, 190, 0.8);
} -> always-single-line
```

* `declaration-colon-space-before : "always" || "never"` - пробел до символа ':' в объявлении свойства
```scss
a { color :pink } -> always
a { color:pink } -> never
```

* `declaration-empty-line-before : "always" || "never"` - использование пустой строки перед объявлением свойств
```scss
a {
  --foo: pink;

  top: 5px;
} -> always

a {
  --foo: pink;
  bottom: 15px;
} -> never
```

* `declaration-no-important : true` - Запрещает использовать `!important`
```scss
a { color: pink !important; } -> Error
```

* `declaration-property-unit-blacklist : { "unprefixed-property-name": ["array", "of", "units"] }` - Запрещает использовать указанные ед. измерения для указанных свойств
```scss
/*
declaration-property-unit-blacklist: {
  "font-size": ["em", "px"],
  "/^animation/": ["s"]
}
*/

a { font-size: 1em; } -> Error
a { font-size: 1.2rem; } -> True
```

* `declaration-property-unit-whitelist : { "unprefixed-property-name": ["array", "of", "units"] }` - Разрешает использовать указанные ед. измерения для указанных свойств
```scss
/*
declaration-property-unit-whitelist: {
  "font-size": ["em", "px"],
  "/^animation/": ["s"]
}
*/

a { font-size: 1em; } -> True
a { font-size: 1.2rem; } -> Error
```

* `declaration-property-value-blacklist : { "unprefixed-property-name": ["array", "of", "values"], "unprefixed-property-name": ["/regex/", "non-regex"] }` - Запрещает использовать определенные значения для свойств
```scss
/*
declaration-property-value-blacklist: {
  "transform": ["/scale3d/", "/rotate3d/", "/translate3d/"],
  "position": ["fixed"],
  "color": ["/^green/"]
  "/^animation/": ["/ease/"]
}
*/

a { position: fixed; } -> Error
a { position: relative; } -> True
a { transform: scale3d(1, 2, 3); } -> Error
```

* `declaration-property-value-whitelist : { "unprefixed-property-name": ["array", "of", "values"], "unprefixed-property-name": ["/regex/", "non-regex"] }` - Запрещает использовать определенные значения для свойств
```scss
/*
declaration-property-value-whitelist: {
  "transform": ["/scale3d/", "/rotate3d/", "/translate3d/"],
  "position": ["fixed"],
  "color": ["/^green/"]
  "/^animation/": ["/ease/"]
}
*/

a { position: fixed; } -> True
a { position: relative; } -> Error
a { transform: scale3d(1, 2, 3); } -> True
```

### Правила для блоков объявлений

* `declaration-block-no-duplicate-properties : true` - запрещает использовать одинаковые свойства несколько раз в блоке
```scss
a { color: pink; color: orange; } -> Error
a { color: pink; } -> True
```

* `declaration-block-no-ignored-properties : true` - запрещает использовать противоречащие друг другу свойства. Их список:
display: inline использовать с width, height, margin, margin-top, margin-bottom, overflow (and all variants).
display: list-item использовать с vertical-align.
display: block использовать с vertical-align.
display: flex использовать с vertical-align.
display: table использовать с vertical-align.
display: table-* использовать с margin (and all variants).
display: table-* (except table-cell) использовать с vertical-align.
display: table-(row|row-group) использовать с width, min-width or max-width.
display: table-(column|column-group) использовать с height, min-height or max-height.
float: left and float: right использовать с vertical-align.
position: static использовать с top, right, bottom, or left.
position: absolute использовать с float, clear or vertical-align.
position: fixed использовать с float, clear or vertical-align.
```scss
a { display: inline: margin-left: 10px; } -> True
a { float: left; vertical-align: baseline; } -> Error
```

* `declaration-block-no-redundant-longhand-properties : true` -  Запрещает расписывать свойства, которые можно сократить. Их список:
padding
margin
background
font
border
border-top
border-bottom
border-left
border-right
border-width
border-style
border-color
border-radius
transition
```scss
a {
  margin-top: 1px;
  margin-right: 2px;
  margin-bottom: 3px;
  margin-left: 4px;
} -> Error

a {
  margin: 1px 2px 3px 4px;
} -> True
```

* `declaration-block-no-shorthand-property-overrides : true` - Разрешает создавать перекрывающие свойства
```scss
a {
  padding-left: 10px;
  padding: 20px;
} -> Error
a { padding: 10px; padding-left: 20px; } -> True
```

* `declaration-block-properties-order : "alphabetical" || ["array", "of", "unprefixed", "property", "names", "or", "group", "objects"]` - устанавливает порядок свойств
```scss
a {
  color: pink;
  top: 0;
} -> alphabetical

/*
declaration-block-properties-order: ["transform", "top", "color"]
*/

a {
  color: pink;
  top: 0;
} -> Error
a {
  top: 0;
  color: pink;
} -> True
```

* `declaration-block-semicolon-newline-after : "always" || "always-multi-line" || "never-multi-line"` - переход на новую строку после символа ';' в объявлении свойства
```scss
a {
  color: pink;
  top: 0;
} -> always

a { color: pink; top: 0; } -> always-multi-line
a {
  color: pink;
  top: 0;
} -> always-multi-line

a {
  color: pink
  ; top: 0;
} -> never-multi-line
```

* `declaration-block-semicolon-newline-before : "always" || "always-multi-line" || "never-multi-line"` - переход на новую строку перед символом ';' в объявлении свойства
```scss
a { color: pink
; } -> always

a { color: pink; } -> always-multi-line
a {
  color: pink
  ; top: 0;
} -> always-multi-line

a {
  color: pink;
  top: 0;
} -> never-multi-line
```

* `declaration-block-semicolon-space-after : "always" || "never" || "always-single-line" || "never-single-line"` - символ пробела после ";"
```scss
a { color: pink; top: 0; } -> always || always-single-line
a { color: pink; } -> never || never-single-line

```

* `declaration-block-semicolon-space-before : "always" || "never" || "always-single-line" || "never-single-line"` - символ пробела до ";"
```scss
a { color: pink ; } -> always || always-single-line
a { color: pink;top: 0; } -> never || never-single-line

```

* `declaration-block-single-line-max-declarations : int` - максимальное кол-во свойств в одноблочном объявлении
```scss
/*
declaration-block-single-line-max-declarations: 1
*/

a { color: pink; top: 3px; } -> Error
a { color: pink; } -> True
```

* `declaration-block-trailing-semicolon : "always" || "never"` - Последний закрывающий символ в блоке свойств
```scss
a { background: orange; color: pink; } -> always
a { color: pink } -> never
```

### Правила для блоков свойств

* `block-closing-brace-empty-line-before : "always-multi-line" || "never"` - использовать пустую линию перед закрывающим символом `}`
```scss
a {
  color: pink;

} -> always-multi-line

a { color: pink; } -> always-multi-line

a {
  color: pink;
} -> never
```

* `block-closing-brace-newline-after : "always" || "always-single-line" || "never-single-line" || "always-multi-line" || "never-multi-line"` - Переход на новую строку после закрывающего символа `}`
```scss
a { color: pink; }
b { color: red; } -> always

a { color: pink;
} b { color: red; } -> always-single-line

a { color: pink; }b { color: red; } -> never-single-line

a { color: pink;
}
b { color: red; } -> always-multi-line

a { color: pink;
}b { color: red; } -> never-multi-line
```

* `block-closing-brace-newline-before : "always" || "always-multi-line" || "never-multi-line"` - Переход на новую строку перед закрывающим символом `}`
```scss
a { color: pink;
} -> always || always-multi-line

a { color: pink; } -> always || never-multi-line

a {
color: pink;} -> never-multi-line
```

* `block-closing-brace-space-after : "always" || "never" || "always-single-line" || "never-single-line" || "always-multi-line" || "never-multi-line"` - Пробел после закрывающего символа `}`

* `block-closing-brace-space-before : "always" || "never" || "always-single-line" || "never-single-line" || "always-multi-line" || "never-multi-line"` - Пробел перед закрывающим символом `}`

* `block-no-empty : true` - запрещает использовать пустые блоки
```scss
a {} -> Error
a { color: pink; } -> True
```

* `block-no-single-line : true` - Запрещает использовать однострочные блоки
```scss
a { color: pink; top: 1px; } -> Error

a {
  color: pink;
  top: 1px;
} -> True
```

* `block-opening-brace-newline-after : "always" || "always-multi-line" || "never-multi-line` - переход на новую линию после открывающего символа `{`

* `block-opening-brace-newline-before : "always" || "always-single-line" || "never-single-line" || "always-multi-line" || "never-multi-line"` - переход на новую линию перед открывающим символом `{`

* `block-opening-brace-space-after : "always" || "never" || "always-single-line" || "never-single-line" || "always-multi-line" || "never-multi-line"` - Пробел после откпосле открывающего символа `{`

* `block-opening-brace-space-before : "always" || "never" || "always-single-line" || "never-single-line" || "always-multi-line" || "never-multi-line"` - Пробел перед открывающим символом `{`

### Правила для селекторов

* `selector-attribute-brackets-space-inside : "always" || "never"` - отступы в селекторе атрибутов
```scss
[ target ] {} -> always
[target] {} -> never
```

* `selector-attribute-operator-blacklist : ["array", "of", "operators"] || "operator"` - Черный список операторов в атрибутах селекторов
```scss
/* selector-attribute-operator-blacklist: [ "*=" ] */

[class*="test"] {} -> Error
[target="_blank"] {} -> True
```

* `selector-attribute-operator-space-after : "always" || "never"` - Пробел после оператора в атрибуте селектора
```scss
[target= _blank] {} -> always
[target=_blank] {} -> never
```

* `selector-attribute-operator-space-before : "always" || "never"` - Пробел перед оператором в атрибуте селектора

* `selector-attribute-operator-whitelist : ["array", "of", "operators"]|"operator"` - Белый список операторов в атрибутах селекторов

* `selector-attribute-quotes : "always" || "never"` - Использование ковычек в атрибутах селекторов
```scss
[target="_blank"] {} -> always
[title=flower] {} -> never
```

* `selector-class-pattern : regex || string` - Паттерн для классовой нотации
```scss
/*
  selector-class-pattern: "foo-[a-z]+"
*/

.foo-bar {} -> True
.foo-BAR {} -> Error
```

*  `selector-combinator-space-after : "always" || "never"` - Пробел после символа комбинатора(+ > ~)
```scss
a> b { color: pink; } -> always
a>b { color: pink; } -> never
```

* `selector-combinator-space-before : "always" || "never"` - Пробел перед символом комбинатора(+ > ~)

* `selector-descendant-combinator-no-non-space : true` - Запрещает использовать ненуженое пространоство между классами
```scss
.foo .bar {} -> True
.foo  .bar {} -> Error
```

* `selector-id-pattern : regex || string` - Паттерн для селектора id

* `selector-max-compound-selectors : int` -  Максимальное кол-во селекторов в запросе
```scss
/* selector-max-compound-selectors: 3 */

.foo .bar .baz .lorem {} -> Error
.foo .baz {
  & > .bar .lorem {}
} -> Error

#foo #bar > #baz {} -> True
```

* `selector-max-specificity : string` - Кол-во максимальных элементов селектора по типу 'id,class,type' указанная в цифрах
```scss
/* selector-max-specificity: '0,2,0' */

.foo div {} -> True
.foo div {
  & div a {}
} -> True

.foo .baz .bar {} -> Error
```

* `selector-nested-pattern : regex || string` - Паттерн для наследуемых свойств
```scss
/* selector-nested-pattern: "^&:\(\?:hover\|focus\)$" */

a {
  .bar {}
} -> Error

a {
  &:hover {}
} -> True
```

* `selector-no-attribute : true` - Запрещает использовать атрибуты в селекторе
```scss
[rel="external"] {} -> Error
a {} -> True
```

* `selector-no-combinator : true` - Запрещает использовать комбинаторы в селекторе
```scss
a b { color: pink; } -> Error, символ пробела так же является комбинатором

a, b { color: pink; } -> True
a { color: pink; } -> True
```

* `selector-no-empty : true` -Запрещает использовать пустые селекторы
```scss
a, , b {} -> Error
{} -> Error
```

* `selector-no-id : true` - Запрещает использовать id в селекторе

* `selector-no-qualifying-type : true` - Запрещает использовать смешанный селектор
```scss
a.foo {
  margin: 0
} -> Error

input[type='button'] {
  margin: 0
} -> Error

.foo {
  margin: 0
} -> True
```
