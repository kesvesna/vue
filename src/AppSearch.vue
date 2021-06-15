<template>
    <div class="card">
      <h1>{{ title }}</h1>
      <hr />
      <div class="good-item">
        <h4><input placeholder="Введите название товара"/></h4>
    </div>
      <h4><button class="btn">Найти</button></h4>
    </div>
</template>

<script>
  export default {
    data: () => ({
      title: 'Поиск',
      goods: []
    })
  }
</script>

<style>
</style>
