# axios

## 具体请参考官网

* [axios](https://www.axios-http.cn/):https://www.axios-http.cn/
    ```jsx
        axios.get(url).then(
            response => {
                //请求成功的回调...
            },
            error => {
                //请求失败的回调...
            }
        )
    ```
* [fetch](https://github.github.io/fetch/):https://github.github.io/fetch/
    ```jsx
		//发送网络请求---使用fetch发送（未优化）
		fetch(url).then(
			response => {
				console.log('联系服务器成功了');
				return response.json()
			},
			error => {
				console.log('联系服务器失败了',error);
				return new Promise(()=>{})
			}
		).then(
			response => {console.log('获取数据成功了',response);},
			error => {console.log('获取数据失败了',error);}
		) 

		//发送网络请求---使用fetch发送（优化）
		try {
			const response= await fetch(url)
			const data = await response.json()
			console.log(data);
		} catch (error) {
			console.log('请求出错',error);
		}
    ```

