<template>
  <div>
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    <ul>
      <li v-for="(good,index) in goods" :key="good.id">
        <span>{{good.text}}</span>
        <span>{{good.price}}</span>
        <el-button type="primary" @click="addGood(index)">添加购物车</el-button>
      </li>
    </ul>

    <!-- App.vue是父组件 -->
    <!-- 购物车组件 -->
    <cart :name="name" :cart="cart"></cart>
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import Cart from "./components/Cart.vue";
export default {
  name: "app",
  components: {
    HelloWorld,
    Cart
  },
  data() {
    return {
      name: "购物车练习",
      showName: false,
      cart: [],
      goods: [
        { id: 1, text: "Java", price: 1000 },
        { id: 2, text: "Python", price: 1000 },
        { id: 3, text: "JavaScript", price: 1000 }
      ]
    };
  },

  methods: {
    addGood(index) {
      const good = this.goods[index];
      const result = this.cart.find(res => res.id === good.id);

      if (result) {
        //购物车里已有该商品
        result.count += 1;
      } else {
        this.cart.push({
          ...good,
          count: 1,
          active: true
        });
      }
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
