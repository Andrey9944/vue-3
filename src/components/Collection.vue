<template>
  <div class="main-page">
    <h1>Список товаров</h1>
    <div v-if="loading" class="loading-state">
      Загрузка...
    </div>
    <div v-else class="product-list">
      <div v-for="product in products" :key="product.id" class="product-card">
        <img :src="product.image" alt="Изображение товара" />
        <h2>{{ product.title }}</h2>
        <p>Цена: {{ product.price }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, onMounted } from 'vue';
import { fetchProducts } from '../services/products';

export default {
  name: 'collectionProducts',
  setup() {
    const loading = ref(true);
    const products = ref([]);

    onMounted(async () => {
      loading.value = true;
      products.value = await fetchProducts();
      loading.value = false;
    });

    return {
      loading,
      products
    };
  }
};
</script>

<style>
.main-page {
  padding: 20px;
}

.loading-state {
  font-size: 20px;
  text-align: center;
}

.product-list {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 20px;
}

.product-card {
  height: 490px;
  padding: 20px;
  border: 1px solid #ccc;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.product-card h2 {
  font-size: 18px;
  margin-bottom: 10px;
}

.product-card p {
  font-size: 14px;
}

/* Добавьте стили для линий выделяющих карточку */
.product-card {
  border: 1px solid #ccc;
  border-radius: 5px;
  box-shadow: 0 0 5px rgba(0, 0, 0, 0.1);
}

h1 {
  font-size: 24px;
  margin-bottom: 20px;
}

h2 {
  font-size: 18px;
  margin-bottom: 10px;
}

p {
  margin-bottom: 10px;
}

img {
  width: 200px;
  height: auto;
  margin-left: 35px;
}
</style>