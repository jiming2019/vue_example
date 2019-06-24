<template>
  <div>
    <p>{{name}}</p>
    <table border="1" cellspacing="0" cellpadding="1">
      <tr>
        <th>#</th>
        <th>课程名</th>
        <th>单价</th>
        <th>数量</th>
        <th>价格</th>
      </tr>
      <!-- c.active的值如果为true，activeColor的样式会添加到这个class元素中 -->
      <tr v-for="(c,index) in cart" :key="c.id" :class="{activeColor:c.active}">
        <td>
          <input type="checkbox" v-model="c.active">
        </td>
        <td>{{c.text}}</td>
        <td>￥{{c.price}}</td>
        <td>
          <button @click="minus(index)">-</button>
          {{c.count}}
          <button @click="add(index)">+</button>
        </td>
        <td>￥{{c.price*c.count}}</td>
      </tr>

      <tr>
        <td></td>
        <td colspan="2">{{activeCount}}/{{count}}</td>
        <td colspan="2">￥{{total}}</td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  props: ["name", "cart"],
  methods: {
    minus(index) {
      const count = this.cart[index].count;
      if (count > 1) {
        this.cart[index].count -= 1;
      } else {
        this.remove(index);
      }
    },
    add(index) {
      this.cart[index].count += 1;
    },
    remove(index) {
      this.$confirm("是否删除?", "提示", {
        confirmButtonText: "确定",
        cancelButtonText: "取消",
        type: "warning"
      })
        .then(() => {
          this.cart.splice(index, 1);
          this.$message({
            type: "success",
            message: "删除成功!"
          });
        })
        .catch(() => {
          this.$message({
            type: "info",
            message: "已取消删除"
          });
        });
    }
  },
  computed: {
    activeCount() {
      //过滤出激活项的数量
      return this.cart.filter(result => result.active).length;
    },
    count() {
      //购物车项总数
      return this.cart.length;
    },
    total() {
      //计算激活项的总价
      let num = 0;
      this.cart.forEach(element => {
        if (element.active) {
          num += element.price * element.count;
        }
      });
      return num;
    }
  }
};
</script>

<style lang="scss" scoped>
.activeColor {
  background-color: lightblue;
}
</style>