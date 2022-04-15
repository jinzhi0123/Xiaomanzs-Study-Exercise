<template>
  <div>
    <button @click="changeMsg">change</button>
    <div>{{ message3.name }}</div>
    <div>{{ message4.name }}</div>
     <button @click="changeMyref">changeMyref</button>
     <div>{{message5}}</div>
  </div>
</template>

<script setup lang="ts">
import { ref, isRef, shallowRef, Ref, triggerRef, customRef } from 'vue'

// isRef
// 判断是不是一个ref对象
const message = ref("lalala");
const message2 = '特菈学姐超可爱';
console.log(isRef(message))
console.log(isRef(message2))


// shallowRef
// 创建一个跟踪自身 .value 变化的 ref，但不会使其值也变成响应式的
// 例子
// 修改其属性是非响应式的这样是不会改变的
type user = {
  name: string
}
const message3: Ref<user> = ref({
  name: '特菈学姐'
})
const message4: Ref<user> = shallowRef({
  name: '特菈学姐'
})
const changeMsg = () => {
  // message3.value.name = '瑾知'
  message4.value.name = '瑾知'
  console.log(message3.value, message4.value);
  // triggerRef 
  // 强制更新页面DOM
  // 这样也是可以改变值的
  triggerRef(message4)
  // 如果同时有ref更新，shallowRef也会被响应
}

// customRef
// 自定义ref 
// customRef 是个工厂函数要求我们返回一个对象 并且实现 get 和 set

function Myref<T>(value: T) {
  return customRef((track, trigger) => {
    return {
      get() {
        track()
        return value;
      },
      set(newVal: T) {
        console.log('set');
        value = newVal
        trigger();
      }
    }
  })
}

let message5 = Myref('嗷呜')
const changeMyref=()=>{
  message5.value='嗷呜~~~~~'
}


</script>

<style scoped>
</style>