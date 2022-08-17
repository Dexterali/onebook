# React事件处理

```jsx
    class Demo extends React.Component {

        //React.createRef调用后可以返回一个容器，该容器可以存储被ref所标识的节点
        input1 = React.createRef();
        
        showData = () => {
            //需要加current
            alert(this.input1.current.value)
        }

        //React中的事件处理函数会接收到一个event参数
        showData2 = (event) => {
            alert(event.target.value);
        }

        render() {
            return (
                <div>
                    <input ref={this.input1} type="text" placeholder="点击按钮提示数据" />&nbsp;
                    <button onClick={this.showData}>点我提示左侧的数据</button>&nbsp;
                    <input onBlur={this.showData2} type="text" placeholder="失去焦点提示数据"/>&nbsp;
                </div>
            )
        }
    }
```

* 有了事件处理函数的event参数，有些时候我们就不需要打ref了！！！
