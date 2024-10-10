<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup
import { ref } from "vue";

const code = ref("");
const visible = ref(false);
const julee = ref("");
const error = ref("");

// random ids created using https://www.random.org/strings/
const julees = ref(
  new Map([
    ["vwnk79".toLowerCase(), "QnJpdHRh"], // Britta
    ["f4d0wt".toLowerCase(), "SmVzc2ljYQ=="], // Jessica
    ["t6u4dl".toLowerCase(), "Qmr2cm4="], // Björn
    ["sqssii".toLowerCase(), "QW5uYWJlbGxl"], // Annabelle
    ["fak0nl".toLowerCase(), "QmVu"], // Ben
    ["l1e91q".toLowerCase(), "SnV0dGE="], // Jutta
    ["r3jluj".toLowerCase(), "V2VybmVy"], // Werner
    //["kAM4Ml".toLowerCase(), "QmluZQ=="], // Bine
    //["mWVDHC".toLowerCase(), "U3RlZmZhbg=="], // Steffan
    ["8a7hse".toLowerCase(), "SGVuZHJpaw=="], // Hendrik
    //["Ok5NJg".toLowerCase(), "TWFyZWs="], // Marek
    //["R1HgMn".toLowerCase(), "QW5uZQ=="], // Anne
  ])
);

const showJulee = (code) => {
  visible.value = true;
  const val = julees.value.get(code);
  if (!!val) {
    julee.value = atob(julees.value.get(code));
  } else {
    error.value = "Ungültiger Zugangscode!";
  }
};

const hide = () => {
  visible.value = false;
  julee.value = "";
  error.value = "";
};

const createJulklappPairs = () => {
  const teilnehmerCode = Array.from(julees.value).map(e => e[0])
  let lostopf = Array.from(julees.value).map(e => e[0])
  const paarungen = new Map()
  
  teilnehmerCode.forEach(t => {
    console.log(t + " zieht aus...")
    const lostopfOhneTeilnehmer = lostopf.filter(id => {
      return t !== id
    })
    console.log(JSON.stringify(lostopfOhneTeilnehmer))
    const gezogen = lostopfOhneTeilnehmer[Math.floor(Math.random()*lostopfOhneTeilnehmer.length)];
    console.log(gezogen)
    paarungen.set(t, gezogen)
    lostopf = lostopf.filter(l => l !== gezogen)
  })

  console.log(paarungen)
}

// createJulklappPairs()
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
      placeholder="abc001"
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
    <div v-if="visible && !error">
      <p>Du beschenkst:</p>
      <div class="text-2xl text-indigo-800">
        {{ julee }}
      </div>
    </div>
    <p v-if="error" class="text-red-600">
      {{ error }}
    </p>
  </div>
</template>
