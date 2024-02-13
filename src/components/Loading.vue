<template>
    <div class="loading-container">
        <div v-for="index in numberOfSquares" :key="index" class="loading-square"
            :style="{ animationDelay: `${index * 0.1}s` }"></div>
    </div>
</template>
  
<script setup lang="ts">
import { ref } from "vue";

const numberOfSquares = ref(5); // Número de quadrados no loading
</script>
  
<style scoped>
.loading-container {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100px;
    /* Altura desejada do loading */
}

.loading-square {
    width: 15px;
    /* Largura de cada quadrado */
    height: 15px;
    /* Altura de cada quadrado */
    margin: 0 5px;
    /* Espaçamento entre os quadrados */
    background-color: #000;
    /* Cor do quadrado */
    animation: loading-animation 1s infinite alternate;
    /* Animação do loading */
}

@keyframes loading-animation {
    from {
        transform: translateY(0);
    }

    to {
        transform: translateY(-20px);
        /* Desloca cada quadrado para cima */
    }
}
</style>
  