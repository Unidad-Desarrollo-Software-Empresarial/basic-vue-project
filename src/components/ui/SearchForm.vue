<script setup lang="ts">
import { defineEmits } from 'vue';
const emit = defineEmits(['search']);

const search = (e) => {
    console.log(e.target.value);
    emit('search', e.target.value);
};

</script>

<template>
    <div class="container">
        <form class="py-2 px-2">
            <label class="sr-only">Búsqueda</label>
            <div class="relative w-full">
                <div class="absolute inset-y-0 rtl:inset-r-0 start-0 flex items-center ps-3 pointer-events-none">
                    <svg class="w-4 h-4 text-gray-500 dark:text-gray-400" aria-hidden="true"
                        xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 20 20">
                        <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                            d="m19 19-4-4m0-7A7 7 0 1 1 1 8a7 7 0 0 1 14 0Z" />
                    </svg>
                </div>
                <input type="text" @input="search" placeholder="Buscar . . ."
                    class="block pt-2 ps-10 text-sm text-gray-900 border border-gray-300 rounded-lg w-80 bg-gray-50 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500">
            </div>
        </form>
    </div>
</template>

<style>
.container {
    position: relative;
    display: flex;
    justify-content: flex-end;
    /* Alinea el contenido a la derecha */
    padding: 0%;
    /* Ajusta el espacio en los bordes para que el contenido no quede pegado al borde */
}
</style>