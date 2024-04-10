<script setup lang="ts">
import { ref } from "vue";
import { Command } from '@tauri-apps/plugin-shell';

const greetMsg = ref("");
const name = ref("");

const loading = ref(false)

async function run() {
  loading.value = true
  const res = await Command
    .create('powershell', 'Get-ItemProperty -Path HKLM:\\SOFTWARE\\WOW6432Node\\Valve\\Steam -Name "InstallPath"')
    .execute()
  loading.value = false
    
  greetMsg.value = res.stdout
}
</script>

<template>
  <form class="row" @submit.prevent="run">
    <input id="greet-input" v-model="name" placeholder="Enter a name..." />
    <button type="submit">{{loading ? 'Loading...' :'Greet'}}</button>
  </form>

  <p>{{ greetMsg }}</p>
</template>
