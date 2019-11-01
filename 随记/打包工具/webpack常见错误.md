## 1.CleanWebpackPlugin is not a constructor



```
// 抛错原写法
const CleanWebpackPlugin = require("clean-webpack-plugin");
 
plugins: [
    new CleanWebpackPlugin(['dist'])
    //或者写成  new CleanWebpackPlugin()
]
 
// 另一种错误写法
 
const CleanWebpackPlugin = require("clean-webpack-plugin");
 
plugins: [
    new CleanWebpackPlugin(['dist'], {
        root: path.resolve(__dirname, '../'),   //根目录
    })
]
 
 
// =============================分割线==============================
 
// 正确写法
 
const { CleanWebpackPlugin } = require("clean-webpack-plugin");
 
...
 
plugins: [
    new CleanWebpackPlugin()
]

```

