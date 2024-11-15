<script setup lang="ts">
import { computed, ref } from "vue";

const count = ref<number>(0);

const incrementCount = () => {
    count.value++;
};

const decrementCount = () => {
    count.value--;
};

const doubleCount = computed(() => count.value * 2)
</script>

<template>
    <div>
        <h3>
            Số đếm: <b>{{ count }}</b>
        </h3>
        <h3>Số nhân đôi: {{ doubleCount }}</h3>
        <button @click="incrementCount">Cộng</button>
        <button @click="decrementCount">Trừ</button>
    </div>
</template>
