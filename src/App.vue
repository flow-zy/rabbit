<template>
  <div>APP组件</div>
  <ul>
    <li v-for="item in boys" :key="item.id">{{ item.name }}</li>
  </ul>
  <!-- 使用模块A的username -->
  <p>A的username --- {{ a.username }}</p>
  <p>A的changeName --- {{ changeName }}</p>
  <hr />
  <p>B的username --- {{ b.username }}</p>
  <p>B的changeName --- {{ bChangeName }}</p>
  <button @click="updates">修改username</button>
  <button @click="updatesS">异步修改username</button>
</template>

<script>
import { computed } from 'vue'
import { useStore } from 'vuex'

export default {
  setup() {
    const store = useStore()
    const boys = store.getters.boys
    const a = store.state.a
    const b = store.state.b
    const changeName = store.getters.username
    const bChangeName = computed(() => {
      return store.getters['b/changeName']
    })
    const updates = () => {
      store.commit('b/update')
    }
    const updatesS = () => {
      store.dispatch('b/update')
    }
    return {
      boys,
      a,
      b,
      changeName,
      bChangeName,
      updates,
      updatesS
    }
  }
}
</script>

<style lang="scss" scoped></style>
