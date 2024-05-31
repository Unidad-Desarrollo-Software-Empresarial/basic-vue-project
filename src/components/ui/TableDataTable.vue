<template>
    <div>
        <table class="custom-table">
            <thead>
                <tr>
                    <th v-for="(column, index) in columns" :key="index">
                        <span @click="onChangeVisibilityColumn(index)">
                            {{ column.name }}
                        </span>
                    </th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(row, rowIndex) in rows" :key="rowIndex" @click="toggleRowSelection(rowIndex)"
                    :class="{ 'selected': selectedRowIndex === rowIndex }">
                    <td v-for="(cell, cellIndex) in row" :key="cellIndex" v-show="columns[cellIndex].isShowing">
                        {{ cell }}
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';

const rows = ref([
  ['Data 1', 'Data 2'],
  ['Data 3', 'Data 4'],
  ['Data 1', 'Data 2'],
  ['Data 3', 'Data 4'],
  ['Data 1', 'Data 2'],
  ['Data 3', 'Data 4'],
  // Agrega más datos según tu necesidad
]);

const columns = ref([
  { name: 'Columna 1', isShowing: true },
  { name: 'Columna 2', isShowing: true },
  // Agrega más columnas según tu necesidad
]);

let selectedRowIndex = ref<number | null>(null);

const onChangeVisibilityColumn = (index: number) => {
  columns.value[index].isShowing = !columns.value[index].isShowing;
}

const toggleRowSelection = (index: number) => {
  selectedRowIndex.value = selectedRowIndex.value === index ? null : index;
}


document.addEventListener('DOMContentLoaded', function () {
    const rows = document.querySelectorAll('.custom-table tbody tr');

    rows.forEach(row => {
        row.addEventListener('click', function () {
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
    border: 1px solid #ddd;  /* Borde de las celdas de datos */
}

/* Estilos alternativos para las filas */
.custom-table tbody tr:nth-child(even) {
    background-color: #White; /* Color de fondo alternativo para filas pares */
}

/* Estilos para filas impares */
.custom-table tbody tr:nth-child(odd) {
  background-color: #F8F8F8; /* Color de fondo alternativo para filas impares */
}

/* Estilos de las filas al pasar el mouse sobre ellas */
.custom-table tbody tr:hover {
    background-color: #EBEBEB; /* Cambia el color de fondo al pasar el mouse  #e2e2e2*/
}

/* Estilo de selección */
.selected {
  background-color: #53B5EA !important; /* Color de fondo azul cuando la fila está seleccionada */
  color: white;
}

</style>