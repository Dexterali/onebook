# js高阶函数与函数柯里化

```jsx
    class Login extends React.Component {

        state = {
            username: "",
            password: "",
        }

        saveFormData = (dataType) => {
            //返回一个回调函数
            return (event) => {
                this.setState({
                    [dataType]: event.target.value
                })
            }
        }

        handleSubmit = (event) => {
            event.preventDefault(); //阻止表单提交
            const { username, password } = this.state;
            alert(`username:${username},password:${password}`);
        }

        render() {
            return (
                <form onSubmit={this.handleSubmit}>
                    用户名：<input onChange={this.saveFormData('username')} type="text" name="username" />
                    密码：<input onChange={this.saveFormData('password')} type="password" name="password" />
                    <button>登录</button>
                </form>
            )

        }
    }
```

* 高阶函数：如果一个函数符合下面2个规范中的任何一个，那该函数就是高阶函数。
    1. 若A函数，接收的参数是一个函数，那么A就可以称之为高阶函数。
    2. 若A函数，调用的返回值依然是一个函数，那么A就可以称之为高阶函数。
    常见的高阶函数有：Promise、setTimeout、arr.map()等等

* 函数的柯里化：通过函数调用继续返回函数的方式，实现多次接收参数最后统一处理的函数编码形式。 
    function sum(a){
        return(b)=>{
            return (c)=>{
                return a+b+c
            }
        }
    }


## 不适用高阶函数的实现方法

```jsx
    class Login extends React.Component {

        state = {
            username: "",
            password: "",
        }

        saveFormData = (event, dataType) => {
            this.setState({
                [dataType]: event.target.value
            })
        }

        handleSubmit = (event) => {
            event.preventDefault(); //阻止表单提交
            const { username, password } = this.state;
            alert(`username:${username},password:${password}`);
        }

        render() {
            return (
                <form onSubmit={this.handleSubmit}>
                    {/* 注意这里 */}
                    用户名：<input onChange={event => this.saveFormData(event, 'username')} type="text" name="username" />
                    密码：<input onChange={event => this.saveFormData(event, 'password')} type="password" name="password" />
                    <button>登录</button>
                </form>
            )

        }
    }
```