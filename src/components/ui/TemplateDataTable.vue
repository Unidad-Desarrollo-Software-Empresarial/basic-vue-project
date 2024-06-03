<template>
    <div>
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
        <div class="relative overflow-x-auto shadow-md sm:rounded-lg">
            <table class="w-full text-sm text-left rtl:text-right text-gray-500 dark:text-gray-400">
                <thead class="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400">
                    <tr>
                        <th v-for="(head, headIndex) in columns" :key="headIndex" scope="col"
                            :class="`${columns[headIndex].isShowing ? 'px-6 py-3' : ''}`">
                            <div v-show="head.isShowing">
                                {{ head.head }}
                            </div>
                        </th>
                        <th>
                            Acción
                        </th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(item, rowIndex) in filteredItems" :key="rowIndex"
                        class="bg-white border-b dark:bg-gray-800 dark:border-gray-700 hover:bg-gray-50 dark:hover:bg-gray-600">
                        <th v-for="(cell, cellIndex) in Object.values(item ? item : [])" :key="cellIndex" scope="row"
                            :class="[
                                ` font-medium text-gray-900 whitespace-nowrap dark:text-white`,
                                `${columns[cellIndex].isShowing ? 'px-6 py-4' : ''}`
                            ]">
                            <div v-show="columns[cellIndex].isShowing">
                                {{ cell }}
                            </div>
                        </th>
                        <!-- item.INTER_ID, se debe cambiar por el campo que se desee obtener el Index del registro de la Data en la Tabla -->
                        <th><button @click="handleRowClick(item.INTER_ID)" type="button" class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 me-2 mb-2 dark:bg-blue-600 dark:hover:bg-blue-700 focus:outline-none dark:focus:ring-blue-800">Editar</button></th>
                    </tr>
                    
                </tbody>
            </table>
        </div>
    </div>
</template>

<script setup lang="ts">
import { computed, onMounted, ref, watch } from 'vue'
import { useQuery } from '@tanstack/vue-query'
import axios from 'axios'
import type { MatrizResponseInterface } from '../interfaces/matriz.interface'

const { data } = useQuery({
    queryKey: ['matriz'],
    queryFn: async () => {
        const response = await axios.get<MatrizResponseInterface[]>(
            'https://gestiondocumental.pucesi.edu.ec/index.php/api/matriz'
        )
        return response.data
    }
})

const searchFilter = ref<string>('');

const filteredItems = computed(() => {
    const rowsToShow = data.value ? data.value : [];
    let items = rowsToShow;

    return items.filter((item, index) => {
        const withinRange = index >= (currentPage.value - 1) * rowsPerPage.value &&
            index < currentPage.value * rowsPerPage.value;

        const matchesSearch = Object.values(item).some(value => {
            return value.toString().toLowerCase().includes(searchFilter.value.toLowerCase());
        });

        return matchesSearch && withinRange;
    });
});

const search = (e) => {
    searchFilter.value = e.target.value;
};

const columns = ref<{ head: string; isShowing: boolean }[]>([])

watch(data, () => {
    if (data.value) {
        columns.value = Object.keys(data.value[0]).map((col) => {
            return { head: col, isShowing: true }
        })
    }
})

onMounted(() => {
    if (data.value) {
        columns.value = Object.keys(data.value[0]).map((col) => {
            return { head: col, isShowing: true }
        })
    }
})

const rowsPerPage = ref<number>(100)
const currentPage = ref<number>(1)
const totalPages = computed(() => {
    return Math.ceil(data.value ? data.value.length / rowsPerPage.value : 0)
})

const items = computed(() => {
    const rowsToShow = data.value ? data.value : []
    return rowsToShow.map((item, index) => {
        if (
            index >= (currentPage.value - 1) * rowsPerPage.value &&
            index < currentPage.value * rowsPerPage.value
        ) {
            return item
        }
    })
})

let selectedIndex = ref<number | null>(null);

const handleRowClick = (index: number) => {
    selectedIndex.value = index;
    console.log('Índice seleccionado:', selectedIndex.value);
};
</script>

<style scoped>
.container {
    position: relative;
    display: flex;
    justify-content: flex-end;
    padding: 0%;
}
</style>