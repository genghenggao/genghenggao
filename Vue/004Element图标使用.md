组件中注册：

```
//组件script
import { Fold } from '@element-plus/icons'
import { Edit } from '@element-plus/icons'

export default {
    components: {
        Fold,
        Edit
    }
}
```

全局注册：

```
//main.js
import { Expand } from '@element-plus/icons'

const app=createApp(App)
app.component('expand',Expand)
app.mount('#app')
```

使用：

```
<!-- 组件template -->
<!-- 来自文档中代码段，可用 -->
<el-icon :size='20'><edit /></el-icon>
<expand />
```



- [ref](https://blog.csdn.net/Alloom/article/details/119415984)





