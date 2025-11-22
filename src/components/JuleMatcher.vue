<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup
import { ref } from "vue";

const code = ref("");
const visible = ref(false);
const julee = ref("");
const error = ref("");

const julees = ref(
  new Map([
    ["nbos4m", "SGVuZHJpaw=="],
    ["rsopb0", "SmVzc2ljYQ=="],
    ["luwgj8", "V2VybmVy"],
    ["v0c0f3", "SnV0dGE="],
    ["txujtm", "QnJpdHRh"],
    ["6vp1yx", "QmrDtnJu"],
    ["skheml", "QW5uYWJlbGxl"],
    ["ounbgv", "QmVu"],
    ["f6ap67", "SW5kaXJh"],
  ]),
);

const base64ToBytes = (base64) => {
  const binString = atob(base64);
  return Uint8Array.from(binString, (m) => m.codePointAt(0));
};

const showJulee = (code) => {
  visible.value = true;
  const val = julees.value.get(code);
  if (!!val) {
    const validUTF16StringDecoded = new TextDecoder().decode(
      base64ToBytes(julees.value.get(code)),
    );
    julee.value = validUTF16StringDecoded;
  } else {
    error.value = "Ungültiger Zugangscode!";
  }
};

const hide = () => {
  visible.value = false;
  julee.value = "";
  error.value = "";
};
</script>

<template>
  <div class="grid gap-6 mb-2">
    <div class="grid gap-4 grid-cols-2">
      <label
        for="access_code"
        class="flex text-l items-center justify-end font-medium text-white dark:text-gray-300"
        >Dein Zugangscode:</label
      >
      <div class="flex justify-left">
        <input
          type="text"
          maxlength="6"
          id="access_code"
          class="bg-[#f3f7f0] border border-[#8c5e58] text-black text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-24 p-2.5"
          placeholder="abc001"
          required
          v-model="code"
          @input="hide"
          v-on:keyup.enter="showJulee(code)"
        />
      </div>
    </div>
    <div>
      <button
        class="bg-[var(--c-red)] hover:bg-[#e32d36] text-white font-bold py-2 px-4 rounded-2xl"
        @click="showJulee(code)"
      >
        Anzeigen
      </button>
    </div>
  </div>

  <div class="mt-6 h-24">
    <div v-if="visible && !error">
      <div class="text-white">Du beschenkst:</div>
      <div class="text-4xl mt-2">{{ julee }}</div>
    </div>
    <p v-if="error" class="mt-2">
      {{ error }}
    </p>
  </div>
</template>
