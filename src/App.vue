<script setup>
import { ref, computed } from "vue";
const products = ref([
  {
id:1,
name: 'tesla',
date: '20.11.24',
count: 10,
price: 4000,
  },
  {
id:2,
name: 'acer',
date: '10.11.24',
count: 150,
price: 2200,
  },
  {
id:3,
name: 'hp',
date: '22.9.24',
count: 15,
price: 1500,
  },
  {
id:4,
name: 'lenovo',
date: '14.5.24',
count: 94,
price: 1900,
  }
]);

const name= ref('');
const date= ref('');
const count= ref('1');
const price= ref('');

const addProduct = () => {
  if (name.value && date.value && count.value && price.value) {
    products.value.push({
      id:Date.now(),
      name: name.value,
      date: date.value,
      count: count.value,
      price: price.value,
    })
  }}

const removeProduct = (id) => {
    products.value = products.value.filter((product) => product.id != id);
    }
  
  const totalSum = computed(() => {
    return products.value.reduce((sum, product) => sum + (product.price*product.count),0); 
  });

</script>

<template>
<div class="container">
    <div class="row">
      <div class="col">
        <h1 class="text-center my-3">Учет товаров</h1>
        <div class="mb-3">
          <label for="exampleFormControlInput1" class="form-label">Название</label>
          <input type="email" v-model="name" class="form-control" id="exampleFormControlInput1" placeholder="name@example.com">
        </div>
        <div class="mb-3">
          <label for="date" class="form-label">Дата добавления</label>
          <input type="date" v-model="date" class="form-control" id="date">
        </div>
        <div class="mb-3">
          <label for="count" class="form-label">Количество</label>
          <input type="number" v-model="count" class="form-control" id="date">
        </div>
        <div class="mb-3">
          <label for="price" class="form-label">Цена</label>
          <input type="number" v-model="price" class="form-control" id="date">
        </div>
        <div>
          <button @click="addProduct" type="button" class="btn btn-outline-success">Добавить</button>
        </div>
      </div>
    </div>
    <div class="row row-cols-1 row-cols-md-2 mt-4">
  <div class="col" v-for="product in products" :key="product.id">
    <div class="card h-100">
      <div class="card-body">
        <h5 class="card-title">{{ product.name }}</h5>
        <p class="card-text">{{ product.price }}</p>
        <p class="card-text">{{ product.count }}</p>
        <p class="card-text">{{ product.date }}</p>
      </div>
      <div class="card-footer">
        <button @click="removeProduct(product.id)" class="btn btn-outline-danger">Удалить</button>
      </div>
    </div>
  </div>
</div>
<div class="row my-4">
  <div class="col">
    <h3 class="text-end">Общая сумма товаров: ${{ totalSum }}</h3>
  </div>
</div>
  </div>
</template>

