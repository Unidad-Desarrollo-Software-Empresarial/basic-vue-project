<template>
    <!-- <div>
        <div class="p-4 bg-white dark:bg-gray-900">
            <label for="table-search" class="sr-only">Search</label>
            <div class="relative mt-1">
                <div class="absolute inset-y-0 rtl:inset-r-0 start-0 flex items-center ps-3 pointer-events-none">
                    <svg class="w-4 h-4 text-gray-500 dark:text-gray-400" aria-hidden="true"
                        xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 20 20">
                        <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                            d="m19 19-4-4m0-7A7 7 0 1 1 1 8a7 7 0 0 1 14 0Z" />
                    </svg>
                </div>
                <input type="text" id="table-search"
                    class="block pt-2 ps-10 text-sm text-gray-900 border border-gray-300 rounded-lg w-80 bg-gray-50 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                    placeholder="Buscar..." />
            </div>
        </div>
    </div> -->


    <div>

        <!-- Dropdown button -->
        <button id="dropdownHoverButton" data-dropdown-toggle="dropdownHover" data-dropdown-trigger="hover"
            data-dropdown-delay="500"
            class="bg-white-700 shadow-lg hover:bg-white-800 focus:ring-4 focus:outline-none focus:ring-white-300 font-medium rounded-lg text-sm mx-4 my-2 px-5 py-2.5 text-center inline-flex items-center dark:bg-white-600 dark:hover:bg-white-700 dark:focus:ring-white-800 "
            type="button">Columnas
            <svg class="w-2.5 h-2.5 ms-3" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none"
                viewBox="0 0 10 6">
                <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                    d="m1 1 4 4 4-4" />
            </svg>
        </button>
        <!-- Dropdown menu -->
        <div id="dropdownHover"
            class="z-10 hidden  bg-white divide-y divide-gray-100 rounded-lg shadow-lg w-44 dark:bg-gray-700 mx-4 max-h-[400px] min-w-[400px] overflow-auto">
            <ul class="py-2 text-sm text-gray-700 dark:text-gray-200" aria-labelledby="dropdownHoverButton">
                <li v-for="(header, index) in columns" :key="index"
                    class="flex justify-between hover:bg-gray-100 hover:cursor-pointer dark:hover:bg-gray-600 dark:hover:text-white"
                    @click="onChangeVisibilityColumn(index)">
                    <span class="block px-4 py-2 ">{{
                        header.head }}</span>
                    <span :class="[
                        `${header.isShowing ? 'text-green-500' : 'text-red-500'}`,
                        `block px-4 py-2`,
                        `hover:bg-gray-100 dark:hover:bg-gray-600 dark:hover:text-white`
                    ]">{{ header.isShowing ? 'Visible' : 'Oculto' }}</span>
                </li>
            </ul>
        </div>

    </div>
    <div>


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
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(row, rowIndex) in rows" :key="rowIndex"
                        class="bg-white border-b dark:bg-gray-800 dark:border-gray-700 hover:bg-gray-50 dark:hover:bg-gray-600">

                        <th v-for="(cell, cellIndex) in Object.values(row ? row : [])" :key="cellIndex" scope="row"
                            :class="[
                                ` font-medium text-gray-900 whitespace-nowrap dark:text-white`,
                                `${columns[cellIndex].isShowing ? 'px-6 py-4' : ''}`
                            ]">
                            <div v-show="columns[cellIndex].isShowing">
                                {{ cell }}
                            </div>
                        </th>

                    </tr>
                </tbody>
            </table>
        </div>

    </div>
    <div>
        <nav class="flex items-center flex-column flex-wrap md:flex-row justify-between p-4"
            aria-label="Table navigation">
            <span
                class="text-sm font-normal text-gray-500 dark:text-gray-400 mb-4 md:mb-0 block w-full md:inline md:w-auto">Mostrando
                <span class="font-semibold text-gray-900 dark:text-white">1-10</span> de
                <span class="font-semibold text-gray-900 dark:text-white">1000</span></span>
            <ul class="inline-flex -space-x-px rtl:space-x-reverse text-sm h-8">
                <li>
                    <a href="#"
                        class="flex items-center justify-center px-3 h-8 ms-0 leading-tight text-gray-500 bg-white border border-gray-300 rounded-s-lg hover:bg-gray-100 hover:text-gray-700 dark:bg-gray-800 dark:border-gray-700 dark:text-gray-400 dark:hover:bg-gray-700 dark:hover:text-white">Anterior</a>
                </li>
                <li>
                    <a href="#"
                        class="flex items-center justify-center px-3 h-8 leading-tight text-gray-500 bg-white border border-gray-300 hover:bg-gray-100 hover:text-gray-700 dark:bg-gray-800 dark:border-gray-700 dark:text-gray-400 dark:hover:bg-gray-700 dark:hover:text-white">1</a>
                </li>
                <li>
                    <a href="#"
                        class="flex items-center justify-center px-3 h-8 leading-tight text-gray-500 bg-white border border-gray-300 hover:bg-gray-100 hover:text-gray-700 dark:bg-gray-800 dark:border-gray-700 dark:text-gray-400 dark:hover:bg-gray-700 dark:hover:text-white">2</a>
                </li>
                <li>
                    <a href="#"
                        class="flex items-center justify-center px-3 h-8 text-blue-600 border border-gray-300 bg-blue-50 hover:bg-blue-100 hover:text-blue-700 dark:border-gray-700 dark:bg-gray-700 dark:text-white">3</a>
                </li>
                <li>
                    <a href="#"
                        class="flex items-center justify-center px-3 h-8 leading-tight text-gray-500 bg-white border border-gray-300 hover:bg-gray-100 hover:text-gray-700 dark:bg-gray-800 dark:border-gray-700 dark:text-gray-400 dark:hover:bg-gray-700 dark:hover:text-white">4</a>
                </li>
                <li>
                    <a href="#"
                        class="flex items-center justify-center px-3 h-8 leading-tight text-gray-500 bg-white border border-gray-300 hover:bg-gray-100 hover:text-gray-700 dark:bg-gray-800 dark:border-gray-700 dark:text-gray-400 dark:hover:bg-gray-700 dark:hover:text-white">5</a>
                </li>
                <li>
                    <a href="#"
                        class="flex items-center justify-center px-3 h-8 leading-tight text-gray-500 bg-white border border-gray-300 rounded-e-lg hover:bg-gray-100 hover:text-gray-700 dark:bg-gray-800 dark:border-gray-700 dark:text-gray-400 dark:hover:bg-gray-700 dark:hover:text-white">Siguiente</a>
                </li>
            </ul>
        </nav>
    </div>
    <div>

    </div>
</template>

<script setup lang="ts">
import { computed, onMounted, ref, watch } from 'vue'
import { useQuery } from '@tanstack/vue-query'
import { initFlowbite } from 'flowbite'
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

const columns = ref<{ head: string; isShowing: boolean }[]>([])

watch(data, () => {
    if (data.value) {
        columns.value = Object.keys(data.value[0]).map((col) => {
            return { head: col, isShowing: true }
        })
    }
})

onMounted(() => {
    initFlowbite()
    if (data.value) {
        columns.value = Object.keys(data.value[0]).map((col) => {
            return { head: col, isShowing: true }
        })
    }
})

const rowsPerPage = ref<number>(3)
const currentPage = ref<number>(1)
const totalPages = computed(() => {
    return Math.ceil(data.value ? data.value.length / rowsPerPage.value : 0)
})

const rows = computed(() => {
    console.log({ currentPage, totalPages })
    const rowsToShow = data.value ? data.value : []
    return rowsToShow.map((row, index) => {
        if (
            index >= (currentPage.value - 1) * rowsPerPage.value &&
            index < currentPage.value * rowsPerPage.value
        ) {
            return row
        }
    })
})

const onChangeVisibilityColumn = (index: number) => {
    columns.value[index].isShowing = !columns.value[index].isShowing
}

</script>

<style scoped></style>
