<template>
  <!-- <p>App.vue</p> -->
  <CustomDataTableUi />
</template>

<script setup lang="ts">
import { onMounted } from 'vue';
import CustomDataTableUi from './components/ui/CustomDataTableUi.vue'
import { initFlowbite } from 'flowbite';
onMounted(() => {
  initFlowbite()
})
</script>
