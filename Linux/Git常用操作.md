# 目录

[TOC]

## 一、命令

```bash
# 清空git缓存
git rm -r --cached .
```



## 一、忽略规则文件语法

### a.忽略指定文件/目录

```gitignore
# 忽略指定文件
HelloWrold.class

# 忽略指定文件夹
bin/
bin/gen/
```

### b.通配符忽略规则

通配符规则如下：

```kotlin
# 忽略.class的所有文件
*.class

# 忽略名称中末尾为ignore的文件夹
*ignore/

# 忽略名称中间包含ignore的文件夹
*ignore*/
```





