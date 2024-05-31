<template>
    <div>
        <!-- Search bar  @search="handleSearch"  -->
        <SearchForm @search="handleSearch" />
        <!-- Radio buttons -->
        <!-- <FilterRadios @filter="handleRadioFilter" /> -->
        <!-- List of filters for statusers -->
        <FilterDropdown />
    </div>

    <!-- <div>
        <div class="p-1 bg-white dark:bg-gray-900">
            <label for="table-search" class="sr-only">Search</label>
            <div class="relative">
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
        <table class="custom-table">
            <thead>
                <tr>
                    <th>Encabezado 1</th>
                    <th>Encabezado 2</th>
                    <th>Encabezado 3</th>
                    <th>Encabezado 4</th>
                    <th>Encabezado 5</th>
                    <th>Encabezado 6</th>
                    <!-- Añade más columnas según sea necesario -->
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td>Dato 1</td>
                    <td>Dato 2</td>
                    <td>Dato 3</td>
                    <td>Dato 4</td>
                    <td>Dato 5</td>
                    <td>Dato 6</td>
                    <!-- Añade más celdas según sea necesario -->
                </tr>
                <tr>
                    <td>Dato 1</td>
                    <td>Dato 2</td>
                    <td>Dato 3</td>
                    <td>Dato 4</td>
                    <td>Dato 5</td>
                    <td>Dato 6</td>
                    <!-- Añade más celdas según sea necesario -->
                </tr>
                <tr>
                    <td>Dato 1</td>
                    <td>Dato 2</td>
                    <td>Dato 3</td>
                    <td>Dato 4</td>
                    <td>Dato 5</td>
                    <td>Dato 6</td>
                    <!-- Añade más celdas según sea necesario -->
                </tr>
                <tr>
                    <td>Dato 1</td>
                    <td>Dato 2</td>
                    <td>Dato 3</td>
                    <td>Dato 4</td>
                    <td>Dato 5</td>
                    <td>Dato 6</td>
                    <!-- Añade más celdas según sea necesario -->
                </tr>
                <tr>
                    <td>Dato 1</td>
                    <td>Dato 2</td>
                    <td>Dato 3</td>
                    <td>Dato 4</td>
                    <td>Dato 5</td>
                    <td>Dato 6</td>
                    <!-- Añade más celdas según sea necesario -->
                </tr>
                <tr>
                    <td>Dato 1</td>
                    <td>Dato 2</td>
                    <td>Dato 3</td>
                    <td>Dato 4</td>
                    <td>Dato 5</td>
                    <td>Dato 6</td>
                    <!-- Añade más celdas según sea necesario -->
                </tr>
                <tr>
                    <td>Dato 1</td>
                    <td>Dato 2</td>
                    <td>Dato 3</td>
                    <td>Dato 4</td>
                    <td>Dato 5</td>
                    <td>Dato 6</td>
                    <!-- Añade más celdas según sea necesario -->
                </tr>
                <!-- Añade más filas según sea necesario -->
            </tbody>
        </table>
    </div>
    <br />
    <div>
        <div class="relative overflow-x-auto shadow-md sm:rounded-lg">
            <!-- <div class="pb-4 bg-white dark:bg-gray-900">
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
                        placeholder="Search for items">
                </div>
            </div> -->
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
                        class="flex items-center justify-center px-3 h-8 leading-tight text-gray-500 bg-white border border-gray-300 hover:bg-gray-100 hover:text-gray-700 dark:bg-gray-800 dark:border-gray-700 dark:text-gray-400 dark:hover:bg-gray-700 dark:hover:text-white">Anterior</a>
                </li>
                <li>
                    <a href="#"
                        class="flex items-center justify-center px-3 h-8 text-blue-600 border border-gray-300 bg-blue-50 hover:bg-blue-100 hover:text-blue-700 dark:border-gray-700 dark:bg-gray-700 dark:text-white">1</a>
                </li>
                <li>
                    <a href="#"
                        class="flex items-center justify-center px-3 h-8 leading-tight text-gray-500 bg-white border border-gray-300 hover:bg-gray-100 hover:text-gray-700 dark:bg-gray-800 dark:border-gray-700 dark:text-gray-400 dark:hover:bg-gray-700 dark:hover:text-white">2</a>
                </li>
                <li>
                    <a href="#"
                        class="flex items-center justify-center px-3 h-8 ms-0 leading-tight text-gray-500 bg-white border border-gray-300 rounded-s-lg hover:bg-gray-100 hover:text-gray-700 dark:bg-gray-800 dark:border-gray-700 dark:text-gray-400 dark:hover:bg-gray-700 dark:hover:text-white">3</a>
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
                        class="flex items-center justify-center px-3 h-8 leading-tight text-gray-500 bg-white border border-gray-300 hover:bg-gray-100 hover:text-gray-700 dark:bg-gray-800 dark:border-gray-700 dark:text-gray-400 dark:hover:bg-gray-700 dark:hover:text-white">6</a>
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
import { useQuery } from '@tanstack/vue-query'
import axios from 'axios'
import {
    // FwbA,
    // FwbTable,
    // FwbTableBody,
    // FwbTableCell,
    // FwbTableHead,
    // FwbTableHeadCell,
    // FwbTableRow,
    FwbDropdown
    // FwbButton
} from 'flowbite-vue'
import type { MatrizResponseInterface } from '../interfaces/matriz.interface'

import FilterRadios from './FilterRadios.vue'
import FilterDropdown from './FilterDropdown.vue'

// Esta implementación es para la Búsqueda 
import SearchForm from './SearchForm.vue'
import { computed, onMounted, ref, watch, defineProps } from 'vue'

const searchFilter = ref<string>('');

const props = defineProps({
    items: {
        type: Array,
        required: true
    }
});

const filteredItems = computed(() => {
    const rowsToShow = data.value ? data.value : [];
    let items = rowsToShow;

    switch (radioFilter.value) {
        case 'today':
            //show items due today
            items = items.filter(item => {
                const itemDate = new Date(item.INTER_FINICIO);
                const today = new Date();
                return itemDate.getDate() === today.getDate()
                    && itemDate.getMonth() === today.getMonth()
                    && itemDate.getFullYear() === today.getFullYear();
            });
            break;
        case 'past':
            // show items past due
            items = items.filter(item => new Date(item.INTER_FINICIO) < new Date());
            break;

        default:
            break;
    }

    return items.filter((item, index) => {
        const withinRange = index >= (currentPage.value - 1) * rowsPerPage.value &&
            index < currentPage.value * rowsPerPage.value;

        // Realizar la búsqueda en todas las propiedades del objeto item
        const matchesSearch = Object.values(item).some(value => {
            // Aquí debes ajustar la lógica de comparación según tus necesidades
            // Por ejemplo, podrías convertir todo a minúsculas para hacer una búsqueda sin distinción entre mayúsculas y minúsculas
            return value.toString().toLowerCase().includes(searchFilter.value.toLowerCase());
        });

        return matchesSearch && withinRange;
    });
});

const handleSearch = (search) => {
    searchFilter.value = search;
};

// Esta implementación es para Filtrar
const radioFilter = ref<string>('');

const handleRadioFilter = (filter) => {
    radioFilter.value = filter;
};



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
    console.log({ currentPage, totalPages })
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

const onChangeVisibilityColumn = (index: number) => {
    columns.value[index].isShowing = !columns.value[index].isShowing
}

document.addEventListener('DOMContentLoaded', function() {
  const rows = document.querySelectorAll('.custom-table tbody tr');

  rows.forEach(row => {
    row.addEventListener('click', function() {
      // Verificar si la fila está seleccionada
      const isSelected = this.classList.contains('selected');

      // Remover la clase 'selected' de todas las filas
      rows.forEach(row => {
        row.classList.remove('selected');
      });

      // Si la fila no estaba seleccionada, agregar la clase 'selected'; de lo contrario, no hacer nada (deseleccionarla)
      if (!isSelected) {
        this.classList.add('selected');
      }
    });
  });
});

</script>

<style scoped>
/* Estilos generales de la tabla */
.custom-table {
  width: 100%;
  border-collapse: collapse; /* Fusiona los bordes de las celdas */
}

/* Estilos de las celdas del encabezado */
.custom-table th {
  background-color: #f2f2f2; /* Color de fondo del encabezado */
  padding: 10px; /* Espaciado interno del encabezado */
  border: 1px solid #ddd; /* Borde de las celdas del encabezado */
}

/* Estilos de las celdas de datos */
.custom-table td {
  padding: 10px; /* Espaciado interno de las celdas de datos */
  border: 1px solid #ddd; /* Borde de las celdas de datos */
}

/* Estilos alternativos para las filas */
.custom-table tbody tr:nth-child(even) {
  background-color: #f9f9f9; /* Color de fondo alternativo para filas pares */
}
/* Estilos de las filas al pasar el mouse sobre ellas */
.custom-table tbody tr:hover {
  background-color: #e2e2e2; /* Cambia el color de fondo al pasar el mouse */
}
/* Estilo de selección */
.custom-table .selected {
  background-color: #add8e6 !important; /* Color de fondo azul para la selección */
}
</style>
