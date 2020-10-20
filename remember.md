#### 1.css3自动补全前缀
>
cnpm install --save-dev autoprefixer postcss-loader
```
   var autoprefixer = require('autoprefixer');
    module.exports={
    //其他配置这里就不写了

    module:{
        loaders:[
        {
        test:/\.css$/,
        //在原有基础上加上一个postcss的loader就可以了
        loaders:['style-loader','css-loader','postcss-loader']
        }
        ]
    },
    postcss:[autoprefixer({browsers:['last 2 versions']})]

    }
```
>

#### 2.copy-webpack-plugin拷贝资源插件
>
cnpm install --save-dev copy-webpack-plugin
```
    new CopyWebpackPlugin([{
        from: __dirname + '/src/public'
    }]),
```
作用：把public 里面的内容全部拷贝到编译目录
>
#### 3.区分开发环境与生产环境
>
```
if (process.env.NODE_ENV === 'production') {
  module.exports.devtool = '#source-map'
  // http://vue-loader.vuejs.org/en/workflow/production.html
  module.exports.plugins = (module.exports.plugins || []).concat([
    new webpack.DefinePlugin({
      'process.env': {
        NODE_ENV: '"production"'
      }
    }),
    new webpack.optimize.UglifyJsPlugin({
      compress: {
        warnings: false
      }
    }),
    new webpack.optimize.OccurrenceOrderPlugin()
    // 根据模块调用次数，给模块分配ids，常被调用的ids分配更短的id，使得ids可预测，降低文件大小，该模块推荐使用
  ])
}
```
> 
#### 4. 路由懒加载
>
```
    chunkFilename: 'js/[name][chunkhash].js',
```
>
#### 5.打包公共文件
>
```
    new webpack.optimize.CommonsChunkPlugin({
                name: 'vendor',
                minChunks: function (module) {
                   // 该配置假定你引入的 vendor 存在于 node_modules 目录中
                   return module.context && module.context.indexOf('node_modules') !== -1;
                }
            })
```  
>
#### 6.webpack命令行工具:webpack-dashboard
>
  webpack中文网： https://doc.webpack-china.org/concepts/
>      
#### ios10 下白屏
```js
   new UglifyJsPlugin({
      uglifyOptions: {
        compress: {
          warnings: false
        },
        mangle: {
          safari10: true
        }
      },
      sourceMap: config.build.productionSourceMap,
      parallel: true
}),
```
#### poly-fill
这是由于IE对promise的支持不好，我们需要安装：babel-polyfill和es6-promise:
```js
    yarn add babel-polyfill es6-promise
    然后在main.js文件中引用:

    import 'babel-polyfill'
    import Vue from 'vue'
    import Es6Promise from 'es6-promise'
    Es6Promise.polyfill()
    最后 build/webpack.base.conf.js 文件中配置如下：

    module.exports = {
        entry: {
        app: ["babel-polyfill", "./src/main.js"]
        }
    };
```

####  Cannot read property 'compilation' of undefined

#### post-css 
yarn add postcss-loader autoprefixer postcss-pxtorem postcss-cssnext -D
####  [object Object] is not a PostCSS plugin
https://github.com/postcss/autoprefixer/issues/1359