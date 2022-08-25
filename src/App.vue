<template>
  <div>{{a}}</div>
  <h1>{{user.name}}</h1>
  <h1>{{user.age}}</h1>
  <h2>userVaue{{userVaue.age}}</h2>
  <h2>userVaue{{userVaue.list}}</h2>
  <button @click="upDataA">更新数据</button>
  <Child  name='name' @jj='jj'/>
</template>

<script lang="ts">
import { defineComponent, reactive, ref } from 'vue';
import Child from './components/Child.vue';

export default defineComponent({
  name: 'App',
  components:{Child},
  setup(props) { 
    function jj(name:string){
      user.name+=name
    }
    let  a = ref(0)  //ref函数返回的是一个ref对象需要。value操作  模板中不需要 架子自动取去。value了
    let obj = {
      name:'zhao',
      age:14,
      list:['11','22']
    }
    let user = reactive({
      name:'雷',
      age:18,
      car:['奥托']
    })
    let userVaue = reactive(obj)
    function upDataA(){
          a.value+=1, 
          user.age++,
          userVaue.age+=1
          userVaue.list[4]='999'
    }
    return {
      a,
      upDataA,
      user,
      userVaue,
      jj
    }
  }
});
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
