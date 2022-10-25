<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup
import { ref } from "vue";

const code = ref("abc123");
const visible = ref(false);
const julee = ref("");
const error = ref("")

const julees = ref(
  new Map([
    ["abc123", "QnJpdHRh"],
    ["abc124", "SmVzc2ljYQ=="],
    ["abc124", "Qmr2cm4="],
    ["abc125", "QW5uYWJlbGxl"],
    ["abc126", "QmVu"],
    ["abc127", "SnV0dGE="],
    ["abc128", "V2VybmVy"],
    ["abc129", "QmluZQ=="],
    ["abc130", "U3RlZmZhbg=="],
    ["abc131", "SGVuZHJpaw=="],
    ["abc132", "TWFyZWs="],
    ["abc132", "QW5uZQ=="],
  ])
);

function showJulee(code) {
  visible.value = true;
  const val = julees.value.get(code);
  if (!!val) {
    julee.value = atob(julees.value.get(code));
  } else {
    error.value = "Ungültiger Zugangscode!"
  }
}

function hide() {
  visible.value = false;
  julee.value = ""
  error.value = ""
}
</script>

<template>
  <div class="flex flex-col justify-center items-center">
    <label
      for="first_name"
      class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-300"
      >Dein Zugangscode:</label
    >
    <input
      type="text"
      maxlength="6"
      id="first_name"
      class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-24 p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
      placeholder="Dein Zugangscode"
      required
      v-model="code"
      @input="hide"
      v-on:keyup.enter="showJulee(code)"
    />
  </div>
  <button
    @click="showJulee(code)"
    class="h-10 px-5 m-2 text-indigo-100 transition-colors duration-150 bg-indigo-700 rounded-lg focus:shadow-outline hover:bg-indigo-800"
  >
    Anzeigen
  </button>
  <div class="mt-12 h-24">
    <p v-if="visible && !error">
      <p >Du beschenkst:</p>
      <div class="text-2xl text-indigo-800">
      {{ julee }}
    </div>
    </p>
    <p v-if="error" class="text-red-600">
      {{ error }}
    </p>
  </div>
</template>
