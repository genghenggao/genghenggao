# 关闭eslint检测



- vue.config.js

```js
module.exports = {


    // 关闭eslint检测
    lintOnSave: false,

    devServer: {

        overlay: {

            warning: false,

            errors: false

        }

    },
}
```

