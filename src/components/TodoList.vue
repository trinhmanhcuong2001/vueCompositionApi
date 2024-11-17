<script setup lang="ts">
import { defineProps, ref } from "vue";
interface Todo {
    id: number;
    name: string;
}
const props = defineProps<{
    todo_list: Todo[];
}>();

const deleteTodo = (id: number) => {
    const index = props.todo_list.findIndex((todo) => todo.id === id);
    if (index !== -1) {
        props.todo_list.splice(index, 1);
    }
};

const editForm = ref<boolean>(false);
const editName = ref<string>("");
const editId = ref<number | null>();
const input = ref<HTMLInputElement | null>(null);

const startEdit = (id: number, name: string) => {
    try {
        editId.value = id;
        editForm.value = true;
        editName.value = name;
    } catch (error) {
        console.log("Error in startEdit:", error);
    }
};

const updateTodo = () => {
    const index = props.todo_list.findIndex((todo) => todo.id === editId.value);
    if (index !== -1) {
        props.todo_list[index].name = editName.value.trim();
        cancelEdit();
    }
};

const cancelEdit = () => {
    editId.value = null;
    editForm.value = false;
    editName.value = "";
};
</script>

<template>
    <div>
        <h3>Danh sách công việc</h3>
        <template v-if="props.todo_list.length">
            <ul>
                <li v-for="todo in props.todo_list" :key="todo.id">
                    <template v-if="editForm && editId === todo.id">
                        <input type="text" v-model="editName" />
                        <button @click="updateTodo()">Lưu</button>
                        <button @click="cancelEdit">Hủy</button>
                    </template>
                    <template v-else>
                        {{ todo.name }}
                        <button @click="startEdit(todo.id, todo.name)">
                            Sửa
                        </button>
                        <button @click="deleteTodo(todo.id)">Xóa</button>
                    </template>
                </li>
            </ul>
        </template>
        <template v-else>
            <b class="colorRed">Chưa có công việc nào</b>
        </template>
    </div>
</template>

<style scoped>
.colorRed {
    color: red;
}
</style>
