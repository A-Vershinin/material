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
