---
title: 记一次react与cordova兼容
date: 2022-06-02 00:17:56
tags: react
---

# react 打包文件给cordova使用
> 谁让咱还不会react native
## Step 1: Update your Package.json
```json
// ...
"private": true,
"homepage": "./",
"dependencies": {
// ...
```

## Step 2: Update your Package.json
   - copy  
   ./cordova/www/js/index.js  =>  ./public
   - update
```html
    <noscript>You need to enable JavaScript to run this app.</noscript>
    <div id="root"></div>
    <!-- this is your cordova script index.js file: -->
    <script src="index.js"></script>
```
src/index.jsx
```javascript

import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import reportWebVitals from './reportWebVitals';
import { Social } from './components/Social'

let startApp = () => {
  ReactDOM.render(
    <react.strictmode>
      <app>
      <social>
    </social></app></react.strictmode>,
    document.getElementById('root')
  );
}

if(!window.cordova) {
  startApp()
} else {
  document.addEventListener('deviceready', startApp, false)
}

reportWebVitals();


```
update package.json file
```json
"scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build && cp -r build/* ./cordova/www",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
},
```
接下来就是添加cordova平台编译签名即可

1. 创建证书命令:
keytool -genkey -alias android.keystore -keyalg RSA -validity 36500 -keystore android.keystore
2. cordova 打包命令:
```shell
cordova run android --release -- --keystore=./android.keystore --storePassword=123456 --alias=android.keystore --password=123456 --packageType=apk
```


   