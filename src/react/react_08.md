# 组件的生命周期

## 1. 旧版本生命周期
![img](./images/react生命周期旧.png)

1. 初始化阶段: 由ReactDOM.render()触发---初次渲染
    1.	constructor()
    2.	componentWillMount()
    3.	render()
    4.	componentDidMount() =====> 常用
            一般在这个钩子中做一些初始化的事，例如：开启定时器、发送网络请求、订阅消息
2. 更新阶段: 由组件内部this.setSate()或父组件render触发
    1.	shouldComponentUpdate()
    2.	componentWillUpdate()
    3.	render() =====> 必须使用的一个
    4.	componentDidUpdate()
3. 卸载组件: 由ReactDOM.unmountComponentAtNode()触发
    1.	componentWillUnmount()  =====> 常用
            一般在这个钩子中做一些收尾的事，例如：关闭定时器、取消订阅消息

```jsx
    class Count extends React.Component {

        //构造器
        constructor(props) {
            console.log('Count---constructor');
            super(props)
            //初始化状态
            this.state = { count: 0 }
        }

        //加1按钮的回调
        add = () => {
            //获取原状态
            const { count } = this.state
            //更新状态
            this.setState({ count: count + 1 })
        }

        //卸载组件按钮的回调
        death = () => {
            // ReactDOM.unmountComponentAtNode(document.getElementById('root'))
            
            //旧的卸载组件的方法现在出现了一点问题，改用这种方式
            this.props.root.unmount();
        }

        //强制更新按钮的回调
        force = () => {
            //forceUpdate是组件原型上的一个方法
            this.forceUpdate()
        }

        //组件将要挂载的钩子
        componentWillMount() {
            console.log('Count---componentWillMount');
        }

        //组件挂载完毕的钩子
        componentDidMount() {
            console.log('Count---componentDidMount');
        }

        //组件将要卸载的钩子
        componentWillUnmount() {
            console.log('Count---componentWillUnmount');
        }

        //控制组件更新的“阀门”
        shouldComponentUpdate() {
            console.log('Count---shouldComponentUpdate');
            return true
        }

        //组件将要更新的钩子
        componentWillUpdate() {
            console.log('Count---componentWillUpdate');
        }

        //组件更新完毕的钩子
        componentDidUpdate() {
            console.log('Count---componentDidUpdate');
        }

        render() {
            console.log('Count---render');
            const { count } = this.state
            return (
                <div>
                    <h2>当前求和为：{count}</h2>
                    <button onClick={this.add}>点我+1</button>
                    <button onClick={this.death}>卸载组件</button>
                    <button onClick={this.force}>不更改任何状态中的数据，强制更新一下</button>
                </div>
            )
        }
    }

    //父组件A
    class A extends React.Component {
        //初始化状态
        state = { carName: '奔驰' }

        changeCar = () => {
            this.setState({ carName: '奥拓' })
        }

        render() {
            return (
                <div>
                    <div>我是A组件</div>
                    <button onClick={this.changeCar}>换车</button>
                    <B carName={this.state.carName} />
                </div>
            )
        }
    }

    //子组件B
    class B extends React.Component {
        //组件将要接收新的props的钩子
        componentWillReceiveProps(props) {
            console.log('B---componentWillReceiveProps', props);
        }

        //控制组件更新的“阀门”
        shouldComponentUpdate() {
            console.log('B---shouldComponentUpdate');
            return true
        }
        //组件将要更新的钩子
        componentWillUpdate() {
            console.log('B---componentWillUpdate');
        }

        //组件更新完毕的钩子
        componentDidUpdate() {
            console.log('B---componentDidUpdate');
        }

        render() {
            console.log('B---render');
            return (
                <div>我是B组件，接收到的车是:{this.props.carName}</div>
            )
        }
    }
```

### 弃用的生命周期钩子

1. componentWillReceiveProps => UNSAFE_componentWillReceiveProps
2. componentWillUpdate => UNSAFE_componentWillUpdate
3. componentWillMount => UNSAFE_componentWillMount

* 如果使用可暂时选择在前面加上 UNSAFE

## 2. 新生命周期

![img](./images/react生命周期新.png)

1. 初始化阶段: 由ReactDOM.render()触发---初次渲染
    1.	constructor()
    2.	getDerivedStateFromProps 
    3.	render()
    4.	componentDidMount() =====> 常用
            一般在这个钩子中做一些初始化的事，例如：开启定时器、发送网络请求、订阅消息
2. 更新阶段: 由组件内部this.setSate()或父组件重新render触发
    1.	getDerivedStateFromProps
    2.	shouldComponentUpdate()
    3.	render()
    4.	getSnapshotBeforeUpdate
    5.	componentDidUpdate()
3. 卸载组件: 由ReactDOM.unmountComponentAtNode()触发
    1.	componentWillUnmount()  =====> 常用
            一般在这个钩子中做一些收尾的事，例如：关闭定时器、取消订阅消息

```jsx
    class Count extends React.Component {
        //构造器
        constructor(props) {
            console.log('Count---constructor');
            super(props)
            //初始化状态
            this.state = { count: 0 }
        }

        //加1按钮的回调
        add = () => {
            //获取原状态
            const { count } = this.state
            //更新状态
            this.setState({ count: count + 1 })
        }

        //卸载组件按钮的回调
        death = () => {
            ReactDOM.unmountComponentAtNode(document.getElementById('root'))
        }

        //强制更新按钮的回调
        force = () => {
            this.forceUpdate()
        }

        //若state的值在任何时候都取决于props，那么可以使用getDerivedStateFromProps
        static getDerivedStateFromProps(props, state) {
            console.log('getDerivedStateFromProps', props, state);
            return null
        }

        //在更新之前获取快照
        getSnapshotBeforeUpdate() {
            console.log('getSnapshotBeforeUpdate');
            return 'hello'
        }

        //组件挂载完毕的钩子
        componentDidMount() {
            console.log('Count---componentDidMount');
        }

        //组件将要卸载的钩子
        componentWillUnmount() {
            console.log('Count---componentWillUnmount');
        }

        //控制组件更新的“阀门”
        shouldComponentUpdate() {
            console.log('Count---shouldComponentUpdate');
            return true
        }

        //组件更新完毕的钩子, snapshotValue 是 getSnapshotBeforeUpdate 的返回值
        componentDidUpdate(preProps, preState, snapshotValue) {
            console.log('Count---componentDidUpdate', preProps, preState, snapshotValue);
        }

        render() {
            console.log('Count---render');
            const { count } = this.state
            return (
                <div>
                    <h2>当前求和为：{count}</h2>
                    <button onClick={this.add}>点我+1</button>
                    <button onClick={this.death}>卸载组件</button>
                    <button onClick={this.force}>不更改任何状态中的数据，强制更新一下</button>
                </div>
            )
        }
    }
```