<template>
<h1 class="jobs">Jobs:</h1>
<RouterLink to="add">
    <button style="text-decoration: none; color: black" class="add">Add Jobs/Work</button>
</RouterLink>
<div class="categories">
    <button style="text-decoration: none; color: black" class="all">All</button>
</div>

<div class="anket">
<div>
<div @click="openModal(person)" v-for="(person, index) in profile" :key="index" class="ankets">
<div class="backicon">
    <img loading="lazy" class="icon" :src="person.icon" alt="Profile Icon" v-if="person.icon">
</div>
    <p class="nick">{{ person.nick }}</p>
    <p class="infd">{{ person.infd }}</p>
    <p class="info">{{ person.info }}</p>
<ul class="tags" v-if="person.tags">
    <li v-for="tag in person.tags" :key="tag">{{ tag }}</li>
</ul>
</div> 
</div>
</div>

<transition name="modal">
<div v-if="open && selectedProfile" class="modal" @click.self="closeModal">
    <div class="modal-content">
        <button @click="closeModal" class="close">X</button>
        <img class="icon" :src="selectedProfile.icon" alt="Profile Icon" v-if="selectedProfile.icon">
        <p style="margin-top: -50px; font-size: 19px;" class="nick">{{ selectedProfile.nick }}</p>
        <p style="color: rgb(166, 166, 166); margin-top: -20px; margin-left: 70px;">{{ selectedProfile.infd }}</p>
        <p style="margin-top: 30px;" class="infomodl">{{ selectedProfile.infomodl }}</p>
    <a :href="selectedProfile.link" target="_blank">
        <button style="text-decoration: none; color: black" class="contact">Contact</button>
    </a>
    </div>
</div>
</transition>
<p></p>
<p></p>
</template>

<script setup>
import { ref } from 'vue';
import { profile } from '../script/home.js';

const open = ref(false); // Управляет видимостью модального окна
const selectedProfile = ref(null); // Здесь будет храниться объект выбранного профиля

// Функция, которая вызывается при клике на анкету
const openModal = (person) => {
  selectedProfile.value = person; // Сохраняем выбранный профиль
  open.value = true; // Открываем модальное окно
};

// Функция для закрытия модального окна
const closeModal = () => {
  open.value = false;
  selectedProfile.value = null; // Очищаем выбранный профиль при закрытии
};
</script>