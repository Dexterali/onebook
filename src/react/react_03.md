# React组件

## 1. 函数式组件

```jsx
    //创建函数式组件
    function Hello(){
        console.log(this); //此处的this是undefined，因为React默认开启了严格模式
        return <h2>函数式组件</h2>
    }
```

## 2. 类式组件

```jsx
    //创建类式组件
    class Hello extends React.Component {
        //类式组件必须重写render函数，
        //React在将虚拟DOM转化为真实DOM时会new出一个类式组件对象，
        //该对象自动调用render函数来渲染组件
        render() {
            console.log('render中的this:',this);
            return (
                <h2>类式组件</h2>
            )
        }
    }
```