<script setup lang="ts">
import { ref } from "vue";

const passwordLength = ref(16);
const includeUppercase = ref(true);
const includeLowercase = ref(true);
const includeNumbers = ref(false);
const includeSymbols = ref(false);
const numOfCreatePassword = ref(5);
const generatedPasswords = ref([]);

const generatePassword = () => {
  const uppercaseChars = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
  const lowercaseChars = "abcdefghijklmnopqrstuvwxyz";
  const numberChars = "0123456789";
  const symbolChars = "!@#$%^&*()_+-=[]{}|;:,.<>?";

  let chars = "";
  if (includeUppercase.value) chars += uppercaseChars;
  if (includeLowercase.value) chars += lowercaseChars;
  if (includeNumbers.value) chars += numberChars;
  if (includeSymbols.value) chars += symbolChars;
  if (numOfCreatePassword.value === 0) {
    alert("パスワードを作成する個数を入力してください");
    return;
  }

  // all checkboxes are unchecked
  if (chars === "") {
    alert("少なくとも1つのオプションを選択してください");
    return;
  }

  let passwords = [];
  for (let i = 0; i < numOfCreatePassword.value; i++) {
    let password = "";
    for (let j = 0; j < passwordLength.value; j++) {
      password += chars.charAt(Math.floor(Math.random() * chars.length));
    }
    passwords.push(password);
  }
  console.log(passwords);

  generatedPasswords.value = passwords;
};
</script>

<template>
  <div class="container my-4 mx-auto">
    <h1 class="text-3xl">パスワードジェネレーター</h1>
    <form class="mt-4" action="">
      <div class="flex flex-col mb-4">
        <label for="length" class="mb-2"
          >Password Length / パスワードの長さ</label
        >
        <input
          type="number"
          id="length"
          class="px-2 py-1 border border-gray-300 rounded"
          v-model="passwordLength"
        />
      </div>
      <div class="flex flex-col mb-4">
        <label for="includeUppercase" class="mb-2">大文字を含む</label>
        <input
          type="checkbox"
          id="includeUppercase"
          class="mr-2"
          v-model="includeUppercase"
        />
      </div>
      <div class="flex flex-col mb-4">
        <label for="includeLowercase" class="mb-2">小文字を含む</label>
        <input
          type="checkbox"
          id="includeLowercase"
          class="mr-2"
          v-model="includeLowercase"
        />
      </div>
      <div class="flex flex-col mb-4">
        <label for="includeNumbers" class="mb-2">数字を含む</label>
        <input
          type="checkbox"
          id="includeNumbers"
          class="mr-2"
          v-model="includeNumbers"
        />
      </div>
      <div class="flex flex-col mb-4">
        <label for="includeSymbols" class="mb-2">記号を含む</label>
        <input
          type="checkbox"
          id="includeSymbols"
          class="mr-2"
          v-model="includeSymbols"
        />
      </div>
      <div class="flex flex-col mb-4">
        <label for="numOfCreatePassword" class="mb-2"
          >パスワードを作成する個数</label
        >
        <input
          type="number"
          id="numOfCreatePassword"
          class="px-2 py-1 border border-gray-300 rounded"
          v-model="numOfCreatePassword"
        />
      </div>
      <button
        class="px-4 py-2 bg-blue-500 text-white rounded hover:bg-blue-600"
        type="button"
        @click="generatePassword"
      >
        パスワード生成
      </button>
    </form>
    <div class="generatedPassword">
      <p class="mt-4">生成されたパスワード</p>
      <ul v-if="generatedPasswords">
        <li v-for="password in generatedPasswords" :key="password">
          {{ password }}
        </li>
      </ul>
    </div>
  </div>
</template>

<style scoped></style>
