# 组件间的通信方式

## 方式：

1. props：
    1. children props
    2. render props
2. 消息订阅-发布：
    [pubs-sub](https://github.com/mroderick/PubSubJS/) 、event等等
    1. PubSub
        ```jsx
            //发布消息
            PubSub.publish(mas,data)
            //订阅消息
            this.tokenID = PubSub.subscribe(msg,(msg,data)=>{
                //订阅消息执行的回调
            })
            //解除订阅
            PubSub.unsubscribe(this.tokenID)
        ```

3. 集中式管理：
    [redux](http://cn.redux.js.org/)：[英文官网](https://redux.js.org/)、dva等等
4. conText:
    生产者-消费者模式

## 组件间的关系

1. 父子组件：props
2. 兄弟组件(非嵌套组件)：消息订阅-发布、集中式管理
3. 祖孙组件(跨级组件)：消息订阅-发布、集中式管理、conText(用的少)
