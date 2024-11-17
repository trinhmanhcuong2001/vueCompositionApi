<script setup lang="ts">
import {
    onMounted,
    onUnmounted,
    onBeforeMount,
    onBeforeUpdate,
    onUpdated,
    ref,
    onRenderTracked,
} from "vue";

const data = ref<string | null>(null);
const isLoading = ref<boolean>(false);
let intervalId: number | null = null;
const input = ref<string | null>(null);

const fetchData = async () => {
    isLoading.value = true;

    await new Promise((resolve) => setTimeout(resolve, 2000));

    data.value = "Dữ liệu đã được tải!";
    isLoading.value = false;
};

onBeforeMount(() => {
    console.log("Component sắp được mount");
});

onMounted(() => {
    console.log("Component đã được mount");
    fetchData();

    intervalId = setInterval(() => {
        console.log("Cập nhật mỗi giây...");
    }, 1000);
});

onBeforeUpdate(() => {
    console.log("Component sắp đc update");
});

onUpdated(() => {
    console.log("component đã đc update");
});

onUnmounted(() => {
    console.log("Component đã được unmount");

    if (intervalId) {
        clearInterval(intervalId);
        intervalId = null;
    }
});

onRenderTracked((e) => {
    console.log('Render tracked:', e);
});
</script>

<template>
    <div>
        <h1>Sử dụng Lifecycle Hooks</h1>
        <p v-if="isLoading">Đang tải dữ liệu...</p>
        <p v-else>{{ data }}</p>
        <p>{{ input }}</p>
        <input type="text" v-model="input" />
    </div>
</template>
