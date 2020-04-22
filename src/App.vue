<template>
  <div id="app">
    <h1>{{title.name}}</h1>
    <div>{{user}}</div>
    <button @click="updateUser">修改名称</button>
    <div>当前count：{{computedCount}}</div>
    <button @click="increment">count + 1</button>
  </div>
  <div>
    <span>不再局限于模板中的单个根节点</span>
  </div>
</template>

<script>
import { reactive,ref,readonly,watchEffect,onMounted,computed } from 'vue'
export default {
  name: 'App',
  setup(){
    // 变量
    const title = reactive({
      name:'welcome to vue 3 beta!'
    })

    const original = reactive({
      conut: 0
    })

    // 只读
    const copy = readonly(original)

    // watch
    watchEffect(() => {
      console.log(`readonly: ${copy.conut}`)
    })

    const user = ref('ref黑铁');

    const updateUser = () => {
      user.value = 'ref青铜'
    }

    // 钩子函数
    onMounted(() => {
      console.log('俺是mounted钩子！')
    })

    // 初始化count值
    const count = ref(0);

    // 事件处理
    const increment = () => {
      count.value++
    }

    // 调用计算属性函数Hook
    const computedCount = computed(() => count.value*100)

    return { title , user, updateUser, count, increment, computedCount }
  }
}
</script>

<style>
#app {
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
