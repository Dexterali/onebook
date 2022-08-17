# 创建虚拟DOM的两种方式

## 1. 使用jsx创建虚拟DOM

```jsx
    const VDOM = (
        <h1 id = "title">
            <span>Hello React</span>
        </h1>
    )
```

## 2. 使用js创建虚拟DOM

```js
    const VDOM = React.createElement('h1', {id: 'title'}, React.createElement('span', {}, "Hello React"));
```
* 推荐使用jsx创建虚拟DOM
* 虚拟DOM是React的概念，虚拟DOM所携带的属性与真实DOM相比比较少
* 虚拟DOM最后会被React转化为真实DOM