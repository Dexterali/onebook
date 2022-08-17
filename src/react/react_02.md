# jsx语法规则

```jsx
	const id = "Hi";
	const data = "Hello React";

	const VDOM = (
		<div>
			<h1 className="title" id={id.toLocaleLowerCase()}>
				<span style={{color: 'red', fontsize: '90px'}}>{data}</span>
			</h1>
			<h1 className="title" id={id.toLocaleLowerCase()}>
				<span style={{color: 'red', fontsize: '90px'}}>{data}</span>
			</h1>
			<input type="text" />
		</div>
	)
```

## 总结

1. 定义虚拟DOM时，不要写引号。
2. 标签中混入JS表达式时要用{}。
3. 样式的类名指定不要用class，要用className。
4. 内联样式，要用style={{key:value}}的形式去写。
5. 只有一个根标签
6. 标签必须闭合
7. 标签首字母
    (1).若小写字母开头，则将该标签转为html中同名元素，若html中无该标签对应的同名元素，则报错。
    (2).若大写字母开头，react就去渲染对应的组件，若组件没有定义，则报错。

## jsx小练习

```jsx
	const data = ["React", "Vue", "Angular"];

	const VDOM = (
		<div>
			<h1>前端框架列表</h1>
			<ul>
				{
                    //数组的map方法接受一个回调函数，函数有两个参数
					data.map((item, index) => {
						return <li key={index}>{item}</li>
					})
				}
			</ul>

		</div>
	)
```
