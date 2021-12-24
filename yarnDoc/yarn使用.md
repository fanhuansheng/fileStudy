### 安装

```bash
npm i -g yarn
```

### 使用

#### 常用命令

```
yarn add package // 安装依赖
yarn global add package // 全局安装依赖
yarn add package -D // 安装开发依赖
yarn remove package // 移除依赖
```

#### 设置yarn国内源

```
yarn config set registry https://registry.npm.taobao.org/
```

#### 设置yarn中node-sass的地址

```
yarn config set sass_binary_site http://cdn.npm.taobao.org/dist/node-sass -g
```