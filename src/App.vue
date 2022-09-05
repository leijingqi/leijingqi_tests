<template>
  <div>{{a}}</div>
  <h1>{{user.name}}</h1>
  <h1>{{user.age}}</h1>
  <h2>userVaue{{userVaue.age}}</h2>
  <h2>userVaue{{userVaue.list}}</h2>
  <button @click="upDataA">更新数据</button>
  <Child  name='name' @jj='jj'/>
  <input type="text" v-model="user1.firstName">
  <input type="text" v-model="user1.lastName">
  <input type="text" v-model="totleName">
  <input type="text" v-model="totleName1">
  <input type="text" v-model="a.totleName2">
  <h2>x:{{x}} Y:{{y}}</h2>
</template>

<script lang="ts">
import { defineComponent, reactive, ref ,computed ,watchEffect, onMounted, onBeforeUnmount } from 'vue';
import Child from './components/Child.vue';

export default defineComponent({
  name: 'App',
  components:{Child},
  setup(props) { 
    function jj(name:string){
      user.name+=name
    }
        let obj = {
      name:'zhao',
      age:14,
      list:['11','22'],
      totleName2:''
    }
    let  a = ref(obj)  //ref函数返回的是一个ref对象需要。value操作  模板中不需要 架子自动取去。value了

    let user = reactive({
      name:'雷',
      age:18,
      car:['奥托']
    })
    let userVaue = reactive(obj)
    function upDataA(){
      console.log(a);
      
          a.value.age+=1, 
          user.age++,
          userVaue.age+=1
          userVaue.list[4]='999'
    }
    const  user0 = {
      firstName:'东方',
      lastName:'不败'
    }
   const user1 =  reactive(user0)
   const totleName = computed(()=>{
        return user1.firstName+'_'+user1.lastName
    })
      const x = ref(-1)
      const y = ref(-1)
      //  const totleName1 = computed({
      //   get(){
      //     return user1.firstName+'_'+user1.lastName

      //   },
      //   set(val:string){
      //     let result = val.split('_')
      //      user1.firstName = result[0]
      //      user1.lastName = result[1]
      //   } 
      //  })
      //  const totleName2 = ''
      const handlerPage=(event:MouseEvent)=>{
        console.log(event);      
        x.value = event.pageX
        y.value = event.pageY
      }
      onMounted(()=>{
        window.addEventListener('click',handlerPage)
      })
      onBeforeUnmount(()=>{
        window.removeEventListener('click',handlerPage)
      })
    watchEffect(()=>{
          a.value.totleName2 = user1.firstName+'_'+user1.lastName
       })
    return {
      a,
      upDataA,
      user,
      userVaue,
      jj,
      user1,
      totleName,x,y
      // totleName1,
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
