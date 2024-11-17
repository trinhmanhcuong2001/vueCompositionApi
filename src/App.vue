<script setup lang="ts">
import { ref, reactive } from 'vue';

interface FormState {
    name: string;
    email: string;
    password: string;
}

const form = reactive<FormState>({
    name: '',
    email: '',
    password: ''
});

const submittedData = reactive<FormState>({
    name: '',
    email: '',
    password: ''
});

const isSubmitting = ref<boolean>(false);

const submitForm = (): void => {
    isSubmitting.value = true;

    setTimeout(() => {
        submittedData.name = form.name;
        submittedData.email = form.email;
        submittedData.password = form.password;
        isSubmitting.value = false;
    }, 1000);
};
</script>

<template>   
    <div>
        <div>
            <h4>Thông tin đã gửi</h4>
            <p>Name: <b>{{ submittedData.name }}</b></p>
            <p>Email: <b>{{ submittedData.email }}</b></p>
            <p>Password: <b>{{ submittedData.password }}</b></p>
        </div>
        <h2>Đăng ký</h2>
        
        <label for="name">Tên:</label>
        <input 
            id="name"
            v-model="form.name"
            type="text"
            placeholder="Nhập tên"
        />
        
        <label for="email">Email:</label>
        <input 
            id="email"
            v-model="form.email"
            type="email"
            placeholder="Nhập email"
        />
        
        <label for="password">Mật khẩu:</label>
        <input 
            id="password"
            v-model="form.password"
            type="password"
            placeholder="Nhập mật khẩu"
        />
        
        <!-- Nút gửi form -->
        <button @click="submitForm" :disabled="isSubmitting">Gửi</button>
        
        <!-- Hiển thị trạng thái gửi form -->
        <p v-if="isSubmitting">Đang gửi...</p>
    </div>
</template>

<style scoped>
input {
    margin: 5px 0;
    padding: 8px;
    font-size: 16px;
}

button {
    margin-top: 10px;
    padding: 10px;
    font-size: 16px;
    cursor: pointer;
}

button:disabled {
    background-color: #ccc;
    cursor: not-allowed;
}
</style>