<script setup lang="ts">
import { reactive, ref } from "vue";

interface Item {
    id: number;
    name: string;
}

const items = reactive<Item[]>([]);

const newItem = ref<string>("");

const editingId = ref<number | null>(null);
const editingName = ref<string>("");

const addItem = () => {
    if (newItem.value.trim() === "") return;

    items.push({
        id: Date.now(),
        name: newItem.value,
    });
    newItem.value = ""; 
    console.log(items);
    
};

const deleteItem = (id: number) => {
    const index = items.findIndex((item) => item.id === id);
    if (index !== -1) {
        items.splice(index, 1);
    }
};

const startEditing = (id: number, currentName: string) => {
    editingId.value = id;
    editingName.value = currentName;
};

const saveEdit = () => {
    if (editingId.value !== null) {
        const item = items.find((item) => item.id === editingId.value);
        if (item) {
            item.name = editingName.value.trim();
        }
    }
    cancelEdit();
};

const cancelEdit = () => {
    editingId.value = null;
    editingName.value = "";
};
</script>

<template>
    <div>
        <h2>Quản lý Danh sách</h2>

        <div>
            <input
                v-model="newItem"
                type="text"
                placeholder="Nhập tên mục mới"
            />
            <button @click="addItem">Thêm</button>
        </div>

        <ul>
            <li v-for="item in items" :key="item.id">
                <template v-if="editingId !== item.id">
                    {{ item.name }}
                    <button @click="startEditing(item.id, item.name)">
                        Sửa
                    </button>
                    <button @click="deleteItem(item.id)">Xóa</button>
                </template>

                <template v-else>
                    <input
                        v-model="editingName"
                        type="text"
                        placeholder="Chỉnh sửa mục"
                    />
                    <button @click="saveEdit">Lưu</button>
                    <button @click="cancelEdit">Hủy</button>
                </template>
            </li>
        </ul>
    </div>
</template>
