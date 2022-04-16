<template>
  <div>

  </div>
</template>

<script setup lang="ts">
// 学习Vue3 第七章（认识Reactive全家桶）
import {reactive,readonly } from 'vue'

// let person = reactive('sad')
// 绑定普通的数据类型 我们可以 使用昨天讲到ref
// 你如果用ref去绑定对象 或者 数组 等复杂的数据类型 我们看源码里面其实也是 去调用reactive
// 使用reactive 去修改值无须.value
// reactive 基础用法
let person = reactive({
  name:'瑾知'
})
person.name = "特菈学姐"
// 数组异步赋值问题
// 这样赋值页面是不会变化的因为会脱离响应式
let arr = reactive<number[]>([])
setTimeout(() => {
  arr = [1,2,3]
  console.log(arr)
}, 1000);

// 方案2

// 包裹一层对象



// 拷贝一份proxy对象将其设置为只读
const copy = readonly(person)


// shallowReactive 只能对浅层的数据 如果是深层的数据只会改变值 不会改变视图
</script>

<style scoped>

</style>