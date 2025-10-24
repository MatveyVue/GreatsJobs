<template>
<div class="backdrop">
<RouterLink style="text-decoration: none; color: white" to="/">
  <h1 class="jobs">Add:</h1>
</RouterLink>
<div class="input-group">
  <textarea class="text" id="messageInput" type="text"  v-model="userMessage" placeholder=" Your Information"></textarea>
</div>
<p class="example">
Example:<br>
1)Connection: @username<br>
2)Your: Worker/Employer<br>
3)Brief Information:<br>
4)Description:<br>
5)Tags:
</p>
<div class="scroll">
<p style="color: rgb(24, 24, 24);">.</p>
<p style="color: rgb(24, 24, 24);">.</p>
<p style="color: rgb(24, 24, 24);">.</p>
</div>

<div class="link-display">
<center>
<a :href="generatedLink">
    <button class="pay" style="text-decoration: none; color: black;" type="button" target="_blank" rel="noopener noreferrer">Pay 1 Ton</button>
</a>
</center>
</div>
</div>
</template>

<style scoped>
.container {
  max-width: 600px;
  margin: 50px auto;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 8px;
  font-family: Arial, sans-serif;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  text-align: center;
}

.input-group {
  margin-bottom: 20px;
  text-align: left;
  color: white;
}

label {
  display: block;
  margin-bottom: 8px;
  font-weight: bold;
  color: #555;
}

input[type="text"] {
  width: calc(100% - 20px);
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 4px;
  font-size: 16px;
  box-sizing: border-box; /* Учитывает padding и border в ширине */
}

.link-display {
  margin-top: 25px;
  margin-bottom: 25px;
  word-break: break-all; /* Разрывает длинные слова для переноса строк */
}

.link-display a:hover {
  text-decoration: underline;
}

.text {
  background-color: rgb(27, 27, 27);
  width: 90%;
  height: 200px;
  margin-left: 15px;
  border-radius: 15px;
  border: none;
  resize: none;
}

textarea {
  color: white; 
  font-size: 16px;
  resize: none;
}

.pay {
  background-color: #97f492;
  font-family: Geologica;
  font-size: 16px;
  height: 45px;
  border: none;
  border-radius: 15px;
  position: fixed;
  width: 90%;
  top:95%;
  left:50%;
  transform:translate(-50%, -50%);
  font-family: Geologica
}

.example {
  color: white;
  font-family: Geologica;
  margin-left: 20px
}
</style>

<script setup>
import { ref, computed } from 'vue';

// --- КОНФИГУРАЦИЯ ---
// Эти параметры можно сделать реактивными, если вы хотите, чтобы пользователь их тоже менял.
// Для примера оставим их константами.
const recipientWallet = 'matveymatvey.ton';
// Сумма в нано-TON. 1 TON = 1,000,000,000 нано-TON.
// Здесь 1000000000 = 1 TON.
const transferAmount = 1000000000; 

// --- Реактивные данные ---
// ref() делает переменную реактивной. Когда ее значение меняется,
// Vue автоматически обновляет связанные части интерфейса.
const userMessage = ref(''); // Здесь будет храниться текст, введенный пользователем
const copied = ref(false); // Для индикации, что ссылка скопирована

// --- Вычисляемое свойство (Computed Property) ---
// computed() используется для создания зависимых реактивных значений.
// generatedLink будет автоматически пересчитываться при изменении userMessage.
const generatedLink = computed(() => {
  const baseUrl = "https://app.tonkeeper.com/transfer/";

  // Важно: Кодируем пользовательский текст для безопасного использования в URL.
  // encodeURIComponent() заменяет специальные символы (пробелы, знаки препинания)
  // на их URL-совместимые эквиваленты (например, пробел на %20).
  const encodedText = encodeURIComponent(userMessage.value);

  // Формируем полную ссылку
  return `${baseUrl}${recipientWallet}?amount=${transferAmount}&text=${encodedText}`;
});

// --- Метод для копирования ссылки ---
const copyLink = async () => {
  try {
    await navigator.clipboard.writeText(generatedLink.value);
    copied.value = true;
    setTimeout(() => {
      copied.value = false;
    }, 2000); // Сбрасываем индикатор "скопировано" через 2 секунды
  } catch (err) {
    console.error('Не удалось скопировать текст: ', err);
    alert('Не удалось скопировать текст. Возможно, ваш браузер не поддерживает эту функцию или не дал разрешение.');
  }
};
</script>
