<template>
  <Suspense>
    <template #default>
      <div>
        <ProductCard :id="productId" />
      </div>
    </template>
    <template #fallback>
      <Loading />
    </template>
  </Suspense>
</template>

<script setup lang="ts">
import { defineAsyncComponent, ref, onMounted } from "vue";
import Loading from "./components/Loading.vue";

const productId = ref<number>(3);

const ProductCard = defineAsyncComponent(
  () => import("./components/CardProduct.vue")
);

const updateProductId = (newId: number) => {
  productId.value = newId;
};

const getProductIdFromURL = () => {
  const urlParams = new URLSearchParams(window.location.search);
  const id = urlParams.get("productId");
  if (id) {
    const parsedId = parseInt(id, 10);
    if (!isNaN(parsedId)) {
      updateProductId(parsedId);
    }
  }
};

onMounted(getProductIdFromURL);
</script>

<style scoped>
.product {
  max-width: 400px;
  margin: 0 auto;
  text-align: center;
}

img {
  max-width: 100%;
}

button {
  margin-top: 20px;
}
</style>
