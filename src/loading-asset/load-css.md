## Loading CSS

```js
pnpm add style-loader css-loader -D
```

loader 执行顺序从右到左，最后一个 loader 应该返回 js 代码

style-loader: 将 css 代码插入到 head 标签中的 style 标签里

css-loader: 读取 css 中的内容并解析然后输出为一个 js 模块

### minimize css for production

```js
const MiniCssExtractPlugin = require("mini-css-extract-plugin")
const CssMinimizerPlugin = require("css-minimizer-webpack-plugin")

module.exports = {
  plugins: [
    new MiniCssExtractPlugin({
      filename: "[name].css",
      chunkFilename: "[id].css",
    }),
  ],
  module: {
    rules: [
      {
        test: /\.css$/,
        use: [MiniCssExtractPlugin.loader, "css-loader"],
      },
    ],
  },
  optimization: {
    minimizer: [
      // For webpack@5 you can use the `...` syntax to extend existing minimizers (i.e. `terser-webpack-plugin`), uncomment the next line
      // `...`,
      new CssMinimizerPlugin(),
    ],
  },
}
```
