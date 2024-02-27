<template>
  <ProductItem
    v-for="product in products"
    :key="product.id"
    :name="product.name"
    :price="product.price"
    :img="product.img"
    :to="`welcome/product/${product.id}`"
  ></ProductItem>
</template>

<script setup lang="ts">
import ProductItem from "../../Product/ProductItem/ProductItem.vue";
import Products from "@/http/axios/products/Products.js";
import { ref } from "vue";

const products = ref(await getProducts());
async function getProducts() {
  const data = await Products.getAll();
  return data.data;
}
</script>
