# Build & Upload React Component to Kissflow LowCode

> **Note:** ไฟล์นี้จะเน้นเฉพาะ **ขั้นตอนหลังจากพัฒนา Component ด้วย React เสร็จแล้ว** และเตรียมสำหรับ **อัปโหลดขึ้นใช้งานบน Kissflow LowCode** ในรูปแบบ Custom Component  
> *(ข้ามขั้นตอนการพัฒนา Component)*  
>  
> ไฟล์แนบ: **Resource & Result**

---

## 📦 ขั้นตอนการ Build โปรเจกต์

เริ่มต้นจาก **Root Folder ของโปรเจกต์**

---

### ✅ 1. ติดตั้ง Webpack

```bash
npm install --save-dev webpack webpack-cli
```

---

### ✅ 2. สร้างไฟล์ `webpack.config.js` ที่ Root Folder

```js
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
  entry: './src/index.js',

  output: {
    filename: 'bundle.js',
    path: path.resolve(__dirname, 'dist'),
  },

  devServer: {
    static: './dist',
  },

  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: /node_modules/,
        use: {
          loader: 'babel-loader',
          options: {
            presets: ['@babel/preset-env', '@babel/preset-react'],
          },
        },
      },
      {
        test: /\.css$/,
        use: ['style-loader', 'css-loader'],
      },
      {
        test: /\.(png|svg|jpg|jpeg|gif)$/i,
        type: 'asset/resource',
      },
    ],
  },

  plugins: [
    new HtmlWebpackPlugin({
      template: 'src/index.html',
    }),
  ],

  resolve: {
    extensions: ['.js', '.jsx', '.json'],
  },
};
```

---

### ✅ 3. ติดตั้ง Loaders & Plugins เพิ่มเติม

```bash
npm install --save-dev babel-loader @babel/core @babel/preset-env @babel/preset-react
npm install --save-dev style-loader css-loader
npm install --save-dev html-webpack-plugin
```

---

### ✅ 4. สร้างไฟล์ `babel.config.json` ใน Root Folder

```json
{
  "presets": ["@babel/preset-env", "@babel/preset-react"]
}
```

---

### ✅ 5. สร้างไฟล์ `index.html` ไปไว้ในโฟลเดอร์ `src/`

> เพื่อใช้เป็น Template ให้กับ HtmlWebpackPlugin
> 
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>React Application</title>
</head>
<body>
    <div id="root"></div> <!-- React will attach to this div -->
</body>
</html>

---

### ✅ 6. แก้ไขไฟล์ `App.js` ในโฟลเดอร์ `src/`

> import React, { Fragment, useState, useEffect } from 'react';

### ✅ 7. แก้ไข `package.json` ในส่วนของ `scripts`

```json
"scripts": {
  "start": "webpack serve --mode development --open",
  "build": "webpack --mode production"
}
```

---

### ✅ 8. สั่ง Build Project

```bash
npm run build
```

หาก Build สำเร็จ จะได้โฟลเดอร์ `dist/` ซึ่งประกอบด้วย:

- `index.html`
- `bundle.js`

---

## 🚀 Upload to Kissflow LowCode

1. **Zip ไฟล์ทั้งหมดภายในโฟลเดอร์ `dist/`**  
   (ไม่รวมตัวโฟลเดอร์ `dist` เอง)

2. อัปโหลดไฟล์ Zip นี้ขึ้น **Kissflow LowCode**  
   ผ่านเมนู **Custom Component**
