<template>
    <div class="card">
      <h1>{{ title }}</h1>
      <hr />
        <div class="good-item" v-for="good in cartGoods" :key="good.product_id">
          <h4>{{ good.product_name }} : {{ good.price }} руб. &nbsp; &nbsp; <span style="color:red; font-weight:bold;" @click="minusCartGood(good.product_id)">&#8722;</span> {{ good.value }} <span style="color:green;  font-weight:bold;" @click="plusCartGood(good.product_id)">&#43;</span></h4>
          <button class="danger btn" @click="removeFromCart(good.product_id)">Удалить</button>
        </div>
      <h2 v-if="cartGoods.length < 1">Корзина пустая</h2>
    </div>
</template>

<script>
  export default {
    data: () => ({
      title: 'Корзина'
    }),
    inject: ['cartGoods'],
    methods: {
      removeFromCart: function (key) {
        for (let i = 0; i < this.cartGoods.length; i++) {
          if (this.cartGoods[i].product_id === key) {
            this.cartGoods.splice(i, 1)
          }
        }
        return this.cartGoods
      },
      minusCartGood: function (key) {
        for (let i = 0; i < this.cartGoods.length; i++) {
          if (this.cartGoods[i].product_id === key) {
            if (this.cartGoods[i].value > 1) {
              this.cartGoods[i].value -= 1
            }
          }
        }
      },
      plusCartGood: function (key) {
        for (let i = 0; i < this.cartGoods.length; i++) {
          if (this.cartGoods[i].product_id === key) {
              this.cartGoods[i].value += 1
          }
        }
      }
    }
  }
</script>

<style>
</style>
