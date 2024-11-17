<script setup lang="ts">
import { reactive, ref } from "vue";
import TodoForm from "./components/TodoForm.vue";
import TodoList from "./components/TodoList.vue";

interface Todo {
    id: Number;
    name: String;
}

const todo_list = ref<Todo[]>([]);

const addTodo = (title: string) => {
    todo_list.value.push({
        id: Date.now(),
        name: title,
    });
};


</script>

<template>
    <div>
        <todo-form :onAdd="addTodo" />
        <todo-list :todo_list="todo_list" />
    </div>
</template>

<style>
body {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    display: block; /* Hoặc display: flex nếu cần */
}

#app {
    width: 100%;
    height: 100%;
}
</style>
