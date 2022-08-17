# React中收集表单数据

## 1. 非受控组件

* 表单值在提交时才能被收集

```jsx
    class Login extends React.Component {

        handleSubmit = (event) => {
            event.preventDefault(); //阻止表单提交
            const { username, password } = this;
            alert(`username:${username.value},password:${password.value}`);
        }

        render() {
            return (
                <form onSubmit={this.handleSubmit}>
                    用户名：<input ref={c => this.username = c} type="text" name="username" />
                    密码：<input ref={c => this.password = c} type="password" name="password" />
                    <button>登录</button>
                </form>
            )

        }
    }
```

## 2. 受控组件

* 表单数据在输入时就能被收集

```jsx
    class Login extends React.Component {

        state = {
            username: "",
            password: "",
        }

        saveUsername = (event) => {
            this.setState({
                username: event.target.value
            })
        }

        savePaaword = (event) => {
            this.setState({
                password: event.target.value
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
                    用户名：<input onChange={this.saveUsername} type="text" name="username" />
                    密码：<input onChange={this.savePaaword} type="password" name="password" />
                    <button>登录</button>
                </form>
            )

        }
    }
```