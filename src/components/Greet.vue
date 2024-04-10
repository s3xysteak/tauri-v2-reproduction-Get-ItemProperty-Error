<script setup lang="ts">
import { ref } from "vue";
import { Command } from '@tauri-apps/plugin-shell';

const greetMsg = ref("");
const name = ref("");

async function run() {
  const res = await Command
    .create('powershell', 'Get-ItemProperty -Path HKLM:\\SOFTWARE\\WOW6432Node\\Valve\\Steam -Name "InstallPath"')
    .execute()
    
  greetMsg.value = res.stdout
}
</script>

<template>
  <form class="row" @submit.prevent="run">
    <input id="greet-input" v-model="name" placeholder="Enter a name..." />
    <button type="submit">Greet</button>
  </form>

  <p>{{ greetMsg }}</p>
</template>
