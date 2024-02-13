<template>
  <div class="product" v-if="product">
    <VueMagnifier :src="product.image" />
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, watch } from "vue";
import VueMagnifier from "@websitebeaver/vue-magnifier";
import "@websitebeaver/vue-magnifier/styles.css";
import { fetchProduct } from "../service/Product";
import { Product } from "../types/Product";


const props = defineProps<{
  id: number;
}>()

const product = ref<Product | null>(null);

const updateProduct = async (id: number) => {
  try {
    const data = await fetchProduct(id);
    if (data) {
      product.value = data;
    }
  } catch (error) {
    console.error("Error fetching product:", error);
  }
};

onMounted(() => {
  updateProduct(props.id);
});

watch(() => props.id, (newId) => {
  updateProduct(newId);
});
</script>

<style scoped>
.product {
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
