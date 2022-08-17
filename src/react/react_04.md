# class组件的三大的属性

## 1. state

```jsx
    class Hello extends React.Component {

        //初始化state的原始写法需要写constructor函数，函数固定接收props参数
        constructor(props) {
            //因为Hello组件继承了React.Component所以必须写super
            //props参数必须传给super
            super(props);
            //初始化state
            this.state = {isHi: false};
            //解决changeData函数中的this指向问题
            this.changeData = this.changeData.bind(this);
        }

        changeData() {
            //这个函数中的this指向有问题！解决方式有两种
            //解构赋值
            const { isHi } = this.state;
            //状态必须通过setState进行更新,且更新是一种合并，不是替换。
            this.setState({
                isHi: !isHi
            });
        }

        //render函数会被调用1到n次，这里的n是指界面更新了n次
        render () {
            const { isHi } = this.state;
            return (
                <h1 onClick={this.changeData}>Hello还是Hi：{isHi ? "Hello" : "Hi" }！</h1>
            )
        }
    }
```

* 注意
  * this指向问题
  ![img](./images/this%E6%8C%87%E5%90%91%E9%97%AE%E9%A2%98.png)

### state简写方式

```jsx
    class Hello extends React.Component {
        //初始化状态
        state = {isHi: false};

        //赋值语句的形式+箭头函数可以解决this指向问题
        changeData = () => {
            const { isHi } = this.state;
            this.setState({
                isHi: !isHi
            });
        }

        render () {
            const { isHi } = this.state;
            return (
                <h1 onClick={this.changeData}>Hello还是Hi：{isHi ? "Hello" : "Hi" }！</h1>
            )
        }
    }
```

## 2. props

* props是只读的

### props的基础使用

```jsx
    class Person extends React.Component {
        render() {
            const { name, age } = this.props;
            return (
                <ul>
                    <li>name : {name}</li>
                    <li>age : {age}</li>
                </ul>
            )
        }
    }

    function App() {

        const p = { name: "li", age: 19 };
        return (
            <div>
                {/* //传递props */}
                <Person name="rust" age={19} />
                {/* //对象的展开操作 */}
                <Person {...p}/>
            </div>
        );
    }
```

### 对props进行限制

```jsx
    import PropTypes from "prop-types";

    class Person extends React.Component {

        //对标签属性进行类型、必要性的限制
        static propTypes = {
            name:PropTypes.string.isRequired, //限制name必传，且为字符串
            age:PropTypes.number,//限制age为数值
        }

        //指定默认标签属性值
        static defaultProps = {
            age:18 //age默认值为18
        }

        render() {
            const { name, age } = this.props;
            return (
                <ul>
                    <li>name : {name}</li>
                    <li>age : {age}</li>
                </ul>
            )
        }
    }
    
    //---------------
    //上面是propTypes的简写形式，下面是复杂形式

    //对标签属性进行类型、必要性的限制
    Person.propTypes = {
        name:PropTypes.string.isRequired, //限制name必传，且为字符串
        sex:PropTypes.string,//限制sex为字符串
        age:PropTypes.number,//限制age为数值
        speak:PropTypes.func,//限制speak为函数
    }
    //指定默认标签属性值
    Person.defaultProps = {
        sex:'男',//sex默认值为男
        age:18 //age默认值为18
    }
```

### 函数式组件使用props

```jsx
    function Person(props) {
        const { name, age } = props;
        return (
            <ul>
                <li>name : {name}</li>
                <li>age : {age}</li>
            </ul>
        )
    }

    function App() {

        const p = { name: "li", age: 19 };
        return (
            <div>
                <Person name="rust" age={19} />
                {/* //对象的展开操作 */}
                <Person {...p} />
            </div>
        );
    }
```

## 3. Ref

### 字符串形式的ref

* 字符串形式的ref即将弃用，这里只是展示一下如何使用！

```jsx
    class Demo extends React.Component {

        showData = () => {
            // console.log(this.refs)
            // const input1 = this.refs.input1;
            const { input1 } = this.refs;
            alert(input1.value)
        }

        render() {
            return (
                <div>
                    <input ref="input1" type="text" placeholder="点击按钮提示数据" />&nbsp;
                    <button onClick={this.showData}>点我提示左侧的数据</button>&nbsp;
                </div>
            )
        }
    }
```

### 回调形式的ref

* 可以使用！
  
```jsx
    class Demo extends React.Component {

        showData = () => {
            alert(this.input1.value)
            alert(this.input2.value)
        }

        //或者这样写回调形式的ref
        getNode = (currentNode) => {
            this.input2 = currentNode;
        }

        render() {
            return (
                <div>
                    <input ref={(currentNode) => { this.input1 = currentNode } } type="text" placeholder="点击按钮提示数据" />&nbsp;

                    <input ref={this.getNode} type="text" placeholder="点击按钮提示数据" />&nbsp;

                    <button onClick={this.showData}>点我提示左侧的数据</button>&nbsp;
                </div>
            )
        }
    }
```

### creatRef

* 提倡使用！！！

```jsx
class Demo extends React.Component {

	//React.createRef调用后可以返回一个容器，该容器可以存储被ref所标识的节点
	input1 = React.createRef();
	
	showData = () => {
		//需要加current
		alert(this.input1.current.value)
	}

	render() {
		console.log(this)
		return (
			<div>
				<input ref={this.input1} type="text" placeholder="点击按钮提示数据" />&nbsp;
				<button onClick={this.showData}>点我提示左侧的数据</button>&nbsp;
			</div>
		)
	}
}
```