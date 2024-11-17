<script setup lang="ts">
import { ref, defineProps } from 'vue';

const newTodoName = ref<string>('')
    const props = defineProps({
        onAdd: {
            type: Function,
            required: true
        }
    })

    const addTodo = () => {
        props.onAdd(newTodoName.value)
        newTodoName.value = ''
    }

</script>

<template>
    <div>
        <h1>Thêm công việc mới</h1>
        <input type="text" v-model="newTodoName"/>
        <button @click="addTodo">Add</button>
    </div>
</template>
