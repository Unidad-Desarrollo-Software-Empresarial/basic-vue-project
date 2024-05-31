<script setup lang="ts">
import { defineEmits } from 'vue';
const emit = defineEmits(['filter']);

const filter = (e) => {
    console.log(e.target.value);
    emit('filter', e.target.value);
};

</script>

<template>
    <div>
        <label class="flex mr-4 items-center flex-nowrap">
            <input type="radio" name="show" value="all" checked @change="filter">
            <span class="whitespace-nowrap ml-1">Mostrar Todo</span>
        </label>
        <label class="flex mr-4 items-center flex-nowrap">
            <input type="radio" name="show" value="today" @change="filter">
            <span class="whitespace-nowrap ml-1">Para hoy</span>
        </label>
        <label class="flex mr-4 items-center flex-nowrap">
            <input type="radio" name="show" value="past"  @change="filter">
            <span class="whitespace-nowrap ml-1">Vencido</span>
        </label>
    </div>
</template>

<style scoped>

</style>