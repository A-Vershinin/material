# Вступление в reactjs
> В этом гайде мы будем использовать синтаксис ES6+
> по этому вам уже нужно уметь настроить Webpack + babel

Самая основная идея react'a это Virtual DOM.
**Virtual DOM** — это дерево React элементов на JavaScript или проще это HTML элементы переведенные в JS объекты.
![Virtual DOM](images/virtual_dom.png)
###### Что делает react
React отрисовывает Virtual DOM в браузере, чтоб сделать интерфейс видимым. React следит за изменениями в Virtual DOM и автоматически изменяет DOM в браузере так, чтоб он соответствовал виртуальному. Самые затратные операции на клиенте это DOM операции и реакт пытается свести их к минимуму, проводя все просчеты в js. 
###### Самые основные понятия в мире react 
С первым мы познакомились это virtual dom.

- **Компоненты** — это элементы React, написаные разработчиком. Обычно это части пользовательского интерфейса, которые содержат свою структуру и функциональность. Например, такие как NavBar, LikeButton, или ImageUploader.
- **JSX** — это мини-шаблонизатор элементов и компонентов React, он трансформируется в JavaScript перед запуском в браузере или рендере на сервере.
- **Элементы** — это объекты JavaScript, которые представляют HTML-элементы. Их не существуют в браузере. они описывают DOM-элементы, такие как h1, div, или section.(на картинке это один кружок)
- **Рендеринг** - это перенос наших элементов в реальный DOM.

___

### Компоненты
**Компоненты** — это главный элемент библиотеки, обычно компонент обладает своими свойствами и функциональностью. Ниже пример компонента.

```javascript
// Импортируем нужные нам методы и библиотеки
import React, {Component} from 'react';
import ReactDOM from 'react-dom';

// создаем собственный компонент
class HelloMessage extends Component {
	render() {
		return <div>Hello, {this.props.name}</div>;
	}
}

// Вывод элемента в реальный DOM
ReactDOM.render(<HelloMessage name="Merrick" />, document.body);

```

Как вы заметили, компоненты это экземпляры класса, которые наследуют функционал из `React.Component`(благодаря hеструктуризующему присваиванию, мы можем писать просто `Component`). Каждый компонент должен реализовывать метод `render`, который будет выполняться во время рендера.
`ReactDOM.render(element, domNode);`, где

- element - это наш компонент,
- domNode - это тот элемент html в который его нужно вставить наш компонент.

___

### JSX
Если присмотреться, то можно увидеть html в том, что возвращает метод render и это не ошибка, это тот самый JSX. Рассмотрим по подробней во что конвертируется JSX.
```javascript
// Возьмем только функцию render()
render() {
	return <div className='text'>Hello</div>;
}
```
Вот во что это переконвертируется
```javascript
// Здесь только функция render()
function render() {
	return React.createElement(
		"div",
		{ className: 'text'},
		'Hello'
	);
}	
```

Выше мы видим, что наш JSX код переконвертировался в обычную функцию `React.createElement();`. Да так и будет происходить всегда и да для этого мы и импортировали `React` класс из библиотеки 'react'.  Функция `React.createElement();` очень интересная она принимает несколько параметров `React.createElement(type, props, children);`, где 
- **type** - это название нашего HTML элемента, 
- **props** - это объект свойств, которые мы указали у компонента,
- **children** - То, что находится внутри нашего элемента. (В данном случае это текст, но может быть и другой React элемент, который сконвертируется в новую функцию `React.createElement();`)

___

### Свойства
В фигурных скобках указываются аргументы которые мы передаем компоненту и они называются свойства. Если посмотреть в вызов `ReactDOM.render()`. Мы добавили туда атрибут *"name"*, который передается при рендере нашего компонента в объект `props` и мы можем к нему обратиться. 
> в JSX нельзя использовать атрибуты for и class, вместо них нужно использовать именя для атрибутов className и htmlFor

```javascript
// Импортируем нужные нам методы и библиотеки
import React, {Component} from 'react';
import ReactDOM from 'react-dom';

// создаем собственный компонент
class HelloMessage extends Component {
	render() {
		return <div className={this.props.classes}>Hello {this.props.name}</div>;
	}
}

// Вывод элемента в реальный DOM
ReactDOM.render(<HelloMessage classes="box light" name="Merrick" />, document.body);

```
Важно сказать, что свойства должны быть неизменяемыми для компонента.

___

### Состояние
**Состояние** - это объект внутри компонента, который отвечает за динамические свойства этого компонента. Его стоит использовать если у вас есть свойства, которые должны меняться по ходу выполнения кода. Чаще всего нужно задать какое то начальное состояние для компонента и это делается с помощью создания объекта `state`, следующим образом.

```javascript
// Импортируем нужные нам методы и библиотеки
import React, {Component} from 'react';
import ReactDOM from 'react-dom';

class GreatButton extends Component {
	deleteName = () => {
		this.setState({ name: !this.state.name });
	}

	state = {
		name: true
	}

	render() {
		var headerText = this.state.name ? 'Merrick' : '';

		return(
			<div>
				<h1>Привет {headerText}</h1>
				<button onClick={this.deleteName}>Скрыть</button>
			</div>
		);
	}
}

ReactDOM.render(<GreatButton/>, document.body);
```
Здесь `state` является инициализируемым свойством, которое наследует наш компонент, babel поддерживает на данный момент это в режиме stage-1. Что бы изменить текущее состояние состояния, как бы это глупо не звучало, в собственных функциях, нужно использовать метод `setState`, текущего компонента, тк обычные функции создают собственную область видимости, а нам нужна область видимости компонента, то мы будем использовать arrow-функции из es6. Данный пример убирает имя при нажатии на кнопку.
Так же `state` можно переписать на более ранную версию Ecmascript так:
```javascript
// Импортируем нужные нам методы и библиотеки
import React, {Component} from 'react';
import ReactDOM from 'react-dom';

class GreatButton extends Component {

	constructor(props) {
		super(props)
		this.state = {
			name: true
		}
	}

	deleteName = () => {
		this.setState({ name: !this.state.name });
	}

	render() {
		var headerText = this.state.name ? 'Merrick' : '';
		return(
			<div>
				<h1>Привет {headerText}</h1>
				<button onClick={this.deleteName}>Скрыть</button>
			</div>
		);
	}
}

ReactDOM.render(<GreatButton/>, document.body);
```
И это будет работать абсолютно так же.

___

### Композиция
**Композиция** - это последнее, что мы пройдем и означает это комбинирование большого компонента из маленьких.
Сразу напишем несложный пример: 
```javascript
// Импортируем нужные нам методы и библиотеки
import React, {Component} from 'react';
import ReactDOM from 'react-dom';

class Photo extends Component {

	state = {
		visible: 'visible'
	}

	deleteFromSpread = (e) => {
		this.setState({
			visible: 'not-visible'
		});
	}

	render() {
		return (
			<a href="#link" onClick={this.deleteFromSpread} className={this.state.visible}><img src={this.props.src} alt="Test" /></a>
		);
	}
}

class PhotoGallary extends Component {

	getDataFromServer = (e) => {
		return [
			'http://photoholic24.com/wp-content/uploads/2012/01/u234280.jpg',
			'http://megafun.name/images/articles/sereznye-koshki-6-foto_1.jpg',
			'http://www.fingus.ru/pict/pict1003/kartinki_987787543333333.jpg'
			]
	}

	render() {

		var data = this.getDataFromServer();
		
		var photos = data.map( (photoUrl) => {
			return <Photo src={photoUrl} />
		});	

		return (
			<div> {photos} </div>
		);
	}
}

ReactDOM.render(<PhotoGallary />, document.body);
```

