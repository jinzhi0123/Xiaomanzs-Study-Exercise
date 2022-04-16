<template>
  <div>
    <input v-model="firstName" type="text">
    <input v-model="lastName" type="text">
    <div>{{ name }}</div>
    <hr>
    <table style="width:800px" border>
      <thead>
        <tr>
          <th>名称</th>
          <th>数量</th>
          <th>价格</th>
          <th>操作</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in data">
          <td align="center">{{ item.name }}</td>
          <td align="center">
            <button @click="AddAnbSub(item, false)">-</button>{{ item.num }}<button
              @click="AddAnbSub(item, true)">+</button>
          </td>
          <td align="center">{{ item.price }}</td>
          <td align="center"> <button @click="del(index)">删除</button>
          </td>
        </tr>
      </tbody>
      <tfoot>
        <tr>
          <td></td>
          <td></td>
          <td></td>
          <td align="center">总价:{{ $total }}</td>
        </tr>
      </tfoot>

    </table>

  </div>
</template>

<script setup lang="ts">
// 学习Vue3 第九章（认识computed计算属性）
import { ref, computed, reactive } from 'vue'
//  2 对象形式
const firstName = ref('')
const lastName = ref('')

let name = computed({
  get: () => {
    return firstName.value + lastName.value
  },
  set: (value) => {
    firstName.value + lastName.value
  }
})
type Shop = {
  name: string,
  num: number,
  price: number
}
const data = reactive<Shop[]>(
  [{
    name: '特菈学姐的咖啡',
    num: 1,
    price: 100
  }, {
    name: '残影的Reflect',
    num: 1,
    price: 100
  }, {
    name: '小池的服务器',
    num: 1,
    price: 1
  }
  ]
)

const AddAnbSub = (item: Shop, type: boolean = false) => {
  if (item.num > 1 && !type) {
    item.num--
  }
  if (item.num <= 99 && type) {
    item.num++
  }

}

const del = (index: number) => {
  data.splice(index, 1)

}

const $total = computed<number>(() => {
  return data.reduce((prev, next) => {
    return prev + (next.num * next.price)
  }, 0)

})

</script>

<style scoped>
</style>