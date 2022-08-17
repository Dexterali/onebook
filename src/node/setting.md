# yarn与npm设置软件源

一、npm

1. 查看
```
    npm get registry 
```
2. 设置淘宝
```
npm config set registry http://registry.npm.taobao.org/
```
3. 切换默认
```
npm config set registry https://registry.npmjs.org/
```

二 、yarn

1. 查看：
```
yarn config get registry
```
2. 修改
```
yarn config set registry http://registry.npm.taobao.org/
```
3. 设置默认
```
yarn config set registry https://registry.yarnpkg.com
```
4. 查看yarn全局缓存目录
```
yarn cache dir
```
5. 清除缓存
```
yarn cache clean
```
6. 设置缓存目录
```
yarn config set cache-folder <path>
// example
yarn config set cache-folder 
```