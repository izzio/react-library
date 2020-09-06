# React 项目实践 -- 搭建一个温度控制App

> 原文链接：https://www.freecodecamp.org/news/react-beginner-project-tutorial-temperature-control-app/
> 

## 项目需求

- 点击 "+" 按钮的时候，温度上升
- 温度不能超过 30℃
- 点击 "-" 按钮的时候，温度降低
- 温度不能低于 0℃
- 当温度高于 15℃ 的时候，背景色变成红色
- 当温度低于 15℃ 的时候，背景色变成蓝色

## 代码构建

> 默认已经安装好 React 环境

首先先创建项目：

```bash
npx create-react-app temperature-control
```

我们需要更改 `index.css` 文件的内容

```css
body {
	font-family: sans-serif;
	text-align: center;
	display: flex;
	flex-direction: column;
	justify-content: center;
	align-items: center;
	min-height: 100vh;
}

.app-container {
	height: 400px;
	width: 300px;
	background: #2b5870;
	border-radius: 20px;
	box-shadow: 10px 10px 38px 0px rgba(0, 0, 0, 0.75);
}

.temperature-display-container {
	display: flex;
	justify-content: center;
	align-items: center;
	height: 70%;
}

.temperature-display {
	display: flex;
	border-radius: 50%;
	color: #ffffff;
	height: 220px;
	width: 220px;
	text-align: center;
	justify-content: center;
	align-items: center;
	font-size: 48px;
	border: 3px #ffffff solid;
	transition: background 0.5s;
}

button {
	border-radius: 100px;
	height: 80px;
	width: 80px;
	font-size: 32px;
	color: #ffffff;
	background: rgb(105, 104, 104);
	border: 2px #ffffff solid;
}

button:hover {
	background: rgb(184, 184, 184);
	cursor: pointer;
}

button:focus {
	outline: 0;
}

.button-container {
	display: flex;
	justify-content: space-evenly;
	align-items: center;
}

.neutral {
	background: rgb(184, 184, 184);
}

.cold {
	background: #035aa6;
}

.hot {
	background: #ff5200;
}

```

更改 `App.js` 的内容：

```jsx
import React from 'react';

const App = () => {
    return (
        <div className='app-container'>
            <div className='temperature-display-container'>
                <div className='temperature-display'>10°C</div>
            </div>
            <div className='button-container'>
                <button>+</button>
                <button>-</button>
            </div>
        </div>
    );
};

export default App;
```

打开终端运行此项目：

```shell script
npm start
```

没有问题将会显示：

![kQ3Inh](https://cdn.jsdelivr.net/gh/izzio/picbed@master/uPic/kQ3Inh.png)

## 动态显示温度值

首先我们让温度值动态显示，将温度值存储在 state 中，便于我们稍后读取数据，并用于逻辑呈现。

***建议将能引起 UI 改变的东西 都放在 state 中。***

在 `App.js` 文件开头导入 `useState hook`:

```jsx
import React, { useState } from 'react';
```

在 `App function` 函数内添加：

```jsx
const [temperatureValue, setTemperatureValue] = useState(10);
```

我们通过 `useState` 进行组件状态管理。 `useState` hook 包含两个参数：

- 一个表示状态初始值的变量
- 一个更新状态值的函数

我们调用了状态变量 `temperatureValue` 和函数 `setTemperatureValue`， 将 10 这个值传递给 userSate hook，作为 temperatureValue 的初始值

> 从 `useState` 获取的值的用法和其他的 JavaScript 变量和函数的用法一样

将 JSX 里的固定温度值改为状态变量

```jsx
// 原来的值
<div className='temperature-display'>10°C</div>

// 更改后的值
<div className='temperature-display'>{temperatureValue}°C</div>
```

## 按钮改变状态

`useState` hook 有一个  `setTemperatureValue`  函数，可以修改温度值，所以我们可以在按钮的  `onClick` 事件中用到它。

首先把“+”按钮的代码修改成：

```jsx
 <button onClick={() => setTemperatureValue(temperatureValue + 1)}>+</button>
```

注意它是怎么调用  `setTemperatureValue`  函数的。获得当前温度值，加上 1，然后将其作为参数传递。

因为温度初始值是 10，加上 1 的话状态值就变成 11。再按一次按钮，状态值变成 12......

将“-”按钮的代码修改成：

```jsx
 <button onClick={() => setTemperatureValue(temperatureValue - 1)}>-</button>
```

和对“+”按钮的操作类似，不过这次是降低温度值。

现在我们的代码是这样的：

```jsx
import React, { useState } from 'react';

const App = () => {
    const [temperatureValue, setTemperatureValue] = useState(10);

    return (
        <div className='app-container'>
            <div className='temperature-display-container'>
                <div className='temperature-display'>{temperatureValue}°C</div>
            </div>
            <div className='button-container'>
                <button onClick={() => setTemperatureValue(temperatureValue + 1)}>+</button>
                <button onClick={() => setTemperatureValue(temperatureValue - 1)}>-</button>
            </div>
        </div>
    );
};

export default App;
```

试着在浏览器运行代码，点击按钮，温度值会升高或降低。

## 基于状态修改颜色



> 参考：
>
>freeCodeCamp - [React 项目实践——搭建一个温度控制 App](https://mp.weixin.qq.com/s/2ec8jNgHZiscekIOg4rQRA)
