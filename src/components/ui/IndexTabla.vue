<template>
    <div>
        <table>
            <thead>
                <tr>
                    <th>ID</th>
                    <th>Nombre</th>
                    <th>Acción</th>
                    <!-- Agrega más columnas según tu estructura de datos -->
                </tr>
            </thead>
            <tbody>
                <tr v-for="(item, index) in tableData" :key="index" >
                    <td>{{ item.id }}</td>
                    <td>{{ item.nombre }}</td>
                    <!-- Agrega más columnas según tu estructura de datos -->
                    <td><button @click="handleRowClick(item.id)">Editar</button></td>
                </tr>
            </tbody>
        </table>
        <div v-if="selectedRow !== null">
            <p>El ID de la fila seleccionada es: {{ selectedRow.id }}</p>
            <!-- Muestra otros datos de la fila seleccionada -->
        </div>
    </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';

interface TableRow {
  id: number;
  nombre: string;
  // Agrega más propiedades según tu estructura de datos
}

const tableData = ref<TableRow[]>([
  { id: 1, nombre: 'Ejemplo 1' },
  { id: 2, nombre: 'Ejemplo 2' },
  // Agrega más datos de ejemplo según sea necesario
]);

const selectedRow = ref<number | null>(null);

const handleRowClick = (index: number) => {
  selectedRow.value = index;
//   console.log(index);
    console.log(selectedRow.value);
};
</script>

<style scoped></style>