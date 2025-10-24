<template>
<div id="preloader">
  <div style="margin-top: -20px;" class="loader">loading</div>
</div>
<h1 class="jobs">Jobs:</h1>
<RouterLink to="add">
    <button style="text-decoration: none; color: black" class="add">Add Jobs/Work</button>
</RouterLink>
<div class="categories">
    <button style="text-decoration: none; color: black" class="all">All</button>
</div>

<div class="anket" style="overflow-y: scroll;">
<div>
<div @click="openModal(person)" v-for="(person, index) in profile" :key="index" class="ankets">
    <link rel="preload">
    <img class="icon" :src="person.icon" alt="Profile Icon" v-if="person.icon">
    </link>
    <p class="nick">{{ person.nick }}</p>
    <p class="infd">{{ person.infd }}</p>
    <p class="info">{{ person.info }}</p>
<ul class="tags" v-if="person.tags">
    <li v-for="tag in person.tags" :key="tag">{{ tag }}</li>
</ul>
</div> 
</div>
</div>
<p style="color: rgb(24, 24, 24);">.</p>

<transition name="modal-bg">
    <div v-if="open && selectedProfile" class="modal-background"></div>
</transition>


<transition name="modal">
<div v-if="open && selectedProfile" class="modal" @click.self="closeModal">
    <div class="modal-content">
    <div @click="closeModal" class="close">
    <div>
        <div class="leftright"></div>
        <div class="rightleft"></div>
    </div>
    </div>
    <div style="margin-top: 10px;">
        <img class="icon" :src="selectedProfile.icon" alt="Profile Icon" v-if="selectedProfile.icon">
        <p style="margin-top: -50px; font-size: 19px;" class="nick">{{ selectedProfile.nick }}</p>
        <p style="color: rgb(166, 166, 166); margin-top: -20px; margin-left: 70px;">{{ selectedProfile.infd }}</p>
        <h3 style="color: white; margin-left: 14px; margin-top: 30px;">Description</h3>
        <p style="margin-top: -5px;" class="infomodl">{{ selectedProfile.description }}</p>
        <h3 style="color: white; margin-left: 14px; margin-top: 30px;">Skills</h3>
        <ul class="tags">
            <li v-for="(tag, index) in selectedProfile.tags" :key="index">{{ tag }}</li>
        </ul>
    <a :href="selectedProfile.link" target="_blank">
        <button style="text-decoration: none; color: black" class="contact">Contact</button>
    </a>
    </div>
</div>
</div>
</transition>
<p></p>
<p></p>
</div>
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
  document.body.classList.add('modal-active-background');
};

// Функция для закрытия модального окна
const closeModal = () => {
  open.value = false;
  selectedProfile.value = null; // Очищаем выбранный профиль при закрытии
  document.body.classList.remove('modal-active-background');
};

window.addEventListener('load', function() {
    // Убираем стандартное поведение при загрузке, т.к. будем использовать setTimeout
});

setTimeout(function() {
    const preloader = document.getElementById('preloader');
    if (preloader) { // Проверяем, существует ли элемент
        preloader.classList.add('hidden'); // Добавляем класс для скрытия
    }
}, 3000);
</script>
