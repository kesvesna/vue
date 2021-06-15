<template>
  <div class="container pt-1">
    <div class="card">
      <h1>{{ title }}</h1>
      <hr />
      <div class="good-item" v-for="good in goods" :key="good.product_id">
        <h4>{{ good.product_name }} - Цена {{ good.price }}<span> </span></h4>
        <button class="btn" @click="addToCart" :data-id="good.product_id" :data-product-name="good.product_name" :data-price="good.price">Купить</button>
      </div>
  </div>
    <app-search></app-search>
    <app-basket :cart-goods="cartGoods"></app-basket>
  </div>
</template>

<script>
  import AppSearch from './AppSearch.vue'
  import AppBasket from './AppBasket.vue'
export default {
  data: () => ({
    title: 'Товары',
    goods: [{ product_id: 1, product_name: 'Mouse', price: 2000, value: 1 },
      { product_id: 2, product_name: 'Notebook', price: 4000, value: 1 }],
    cartGoods: []
  }),
  provide () {
    return {
      cartGoods: this.cartGoods
    }
  },
  components: {
    'app-search': AppSearch,
    'app-basket': AppBasket
  },
  methods: {
      addToCart (e) {
        let thisGoodIsNotExist = false
        if (this.cartGoods.length > 0) {
            for (let i = 0; i < this.cartGoods.length; i++) {
              if (this.cartGoods[i].product_id === e.target.getAttribute('data-id')) {
                this.cartGoods[i].value += 1
                i = this.cartGoods.length + 1
                thisGoodIsNotExist = true
              }
            }
        }
        if (!thisGoodIsNotExist) {
          const choosenItem = {
            product_id: e.target.getAttribute('data-id'),
            product_name: e.target.getAttribute('data-product-name'),
            price: e.target.getAttribute('data-price'),
            value: 1
          }
          this.cartGoods.push(choosenItem)
        }
      }
  }
}
</script>

<style>
</style>
