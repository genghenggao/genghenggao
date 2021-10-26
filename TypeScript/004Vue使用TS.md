# VUE3.0+TS用ref获取元素



```vue
<div ref="eleRef" @click="handleClick">div元素</div>

//在setup中无法使用this
setup(){
	//新建一个ref对象,对象命名必须与ref命名相同
	//在setup的中还不是一个DOM节点类型,在DOM挂载后才会是ELEMENT类型,所以要设置泛型
	const eleRef = ref<null | HTMLElement>(null)

	const handleClick = () => {
		if(eleRef.value){
			console.log(eleRef.value)
		}
	}
	//return回去
	return {
		eleRef,
		handleClick
	}
}

```

