<template>
  <div>
    <MyHeader title="购物车案例" background="orange"></MyHeader>
    <div class="main">
      <MyGoods v-for="obj in list" :key="obj.id" :gObj="obj"></MyGoods>
    </div>
    <MyFooter @changeAll="allFn" :arr="list"></MyFooter>
  </div>
</template>

<script>
import MyHeader from './components/MyHeader.vue'
import MyGoods from './components/MyGoods.vue'
import MyFooter from './components/MyFooter.vue'
export default {
  data() {
    return {
      list: [],
    }
  },
  components: {
    MyHeader,
    MyGoods,
    MyFooter,
  },
  created() {
    this.$axios({
      method: 'get',
      url: '/api/cart',
    }).then((res) => {
      console.log(res)
      this.list = res.data.list
    })
  },
  methods: {
    allFn(bool) {
      this.list.forEach((obj) => {
        obj.goods_state = bool
      })
    },
  },
}
</script>
7

<style scoped>
.main {
  padding-top: 45px;
  padding-bottom: 50px;
}
</style>
