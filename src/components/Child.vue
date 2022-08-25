<template>
<div>
  <h1>雷jingqi</h1>
  <button @click="childHandler">子组件触发事件</button>
</div>
</template>
<script>
// 解构
import { defineComponent,} from 'vue'
// 模块化
export default defineComponent({
name:'', 
props: ['name'],
components: {
},
setup(props, ctx){
  console.log(props,ctx);
  function childHandler(){
    ctx.emit('jj','++')
  }
return {
  childHandler
}
}
})
</script>
<style scoped>
</style>
 