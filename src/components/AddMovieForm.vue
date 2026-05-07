<script setup>
import { ref } from 'vue';

const emit = defineEmits(['add-movie']);

const title = ref('');
const rating = ref('');

const handleAdd = () => {
    if (title.value === '') {
        alert('영화 제목을 입력해주세요.');
        return;
    }
    else if (rating.value === '') {
        alert('평점을 입력해주세요.');
        return;
    }
    else if (rating.value < 1 || rating.value > 10) {
        alert('평점은 1~10 사이로 입력해주세요.');
        return;
    }
    else if (!/^\d+(\.\d)?$/.test(String(rating.value))) {
        alert('평점은 소수점 한 자리까지만 입력해주세요.');
        return;
    }
    emit('add-movie', { title: title.value, rating: rating.value });

    title.value = '';
    rating.value = '';
};
</script>

<template>
  <div class="add-form">
    <h3>새 영화 등록하기</h3>
    <div class="add-area">
        <input type="text" placeholder="영화 제목" maxlength="30" v-model="title">
        <input type="number" placeholder="평점 (1~10)" min="1" max="10" step="0.1" v-model="rating">
        <button class="add-btn" @click="handleAdd">등록하기</button>
    </div>
  </div>
</template>

<style scoped>
    .add-form {
    padding: 20px 40px;
    background: #fff;
    border: 1px solid #e0e0e0;
    border-radius: 12px;
    box-shadow: 0 4px 6px rgba(0,0,0,0.05);
    min-width: 160px;
    }

    h3 {
        margin: 0 0 10px 0;
        color: #2c3e50;
        font-size: 1.4rem;
    }

    .add-area {
        display: flex;
        gap: 10px;
        flex-wrap: wrap;
    }

    input {
        padding: 10px 14px;
        border: 1px solid #ccc;
        border-radius: 6px;
        font-size: 0.9rem;
        outline: none;
    }
    input:focus {
        border-color: #3498db;
    }
    input[type="text"] {
        flex: 1;
        min-width: 100px;
        box-sizing: border-box;
    }
    input[type="number"] {
        flex: 1;
        min-width: 100px;
        box-sizing: border-box;
    }

    .add-btn {
        padding: 10px 15px;
        cursor: pointer;
        border: none;
        border-radius: 6px;
        font-weight: bold;
        font-size: 0.9rem;
        transition: opacity 0.2s;
        flex-shrink: 0;
    }
    .add-btn:hover {
        opacity: 0.8;
    }
</style>