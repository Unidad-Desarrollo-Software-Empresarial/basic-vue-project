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
                <tr v-for="(item, index) in tableData" :key="index">
                    <td>{{ item.id }}</td>
                    <td>{{ item.nombre }}</td>
                    <!-- Agrega más columnas según tu estructura de datos -->
                    <td><button @click="handleRowClick(item.id)" type="button" class="btn btn-primary">Editar</button>
                    </td>
                </tr>
            </tbody>
        </table>
        <div v-if="selectedRow !== null">
            <p>El ID de la fila seleccionada es: {{ selectedRow }}</p>
            <!-- Muestra otros datos de la fila seleccionada -->
        </div>
    </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { useRouter } from 'vue-router';

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
    // console.log(selectedRow.value);
};
</script>

<style scoped>
.btn {
    display: inline-block;
    margin-bottom: 0;
    font-weight: normal;
    text-align: center;
    vertical-align: middle;
    cursor: pointer;
    background-image: none;
    border: 1px solid transparent;
    white-space: nowrap;
    padding: 8px 12px;
    font-size: 14px;
    line-height: 1.42857143;
    border-radius: 4px;
    -webkit-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none
}

.btn:focus,
.btn:active:focus,
.btn.active:focus {
    outline: thin dotted;
    outline: 5px auto -webkit-focus-ring-color;
    outline-offset: -2px
}

.btn:hover,
.btn:focus {
    color: #555555;
    text-decoration: none
}

.btn:active,
.btn.active {
    outline: 0;
    background-image: none;
    -webkit-box-shadow: inset 0 3px 5px rgba(0, 0, 0, 0.125);
    box-shadow: inset 0 3px 5px rgba(0, 0, 0, 0.125)
}

.btn.disabled,
.btn[disabled],
fieldset[disabled] .btn {
    cursor: not-allowed;
    pointer-events: none;
    opacity: 0.65;
    filter: alpha(opacity=65);
    -webkit-box-shadow: none;
    box-shadow: none
}

.btn-default {
    color: #555555;
    background-color: #ffffff;
    border-color: rgba(0, 0, 0, 0.1)
}

.btn-default:hover,
.btn-default:focus,
.btn-default:active,
.btn-default.active,
.open>.dropdown-toggle.btn-default {
    color: #555555;
    background-color: #e6e6e6;
    border-color: rgba(0, 0, 0, 0.1)
}

.btn-default:active,
.btn-default.active,
.open>.dropdown-toggle.btn-default {
    background-image: none
}

.btn-default.disabled,
.btn-default[disabled],
fieldset[disabled] .btn-default,
.btn-default.disabled:hover,
.btn-default[disabled]:hover,
fieldset[disabled] .btn-default:hover,
.btn-default.disabled:focus,
.btn-default[disabled]:focus,
fieldset[disabled] .btn-default:focus,
.btn-default.disabled:active,
.btn-default[disabled]:active,
fieldset[disabled] .btn-default:active,
.btn-default.disabled.active,
.btn-default[disabled].active,
fieldset[disabled] .btn-default.active {
    background-color: #ffffff;
    border-color: rgba(0, 0, 0, 0.1)
}

.btn-default .badge {
    color: #ffffff;
    background-color: #555555
}

.btn-primary {
    color: #ffffff;
    background-color: #4ec0da;
    border-color: #4ec0da
}

.btn-primary:hover,
.btn-primary:focus,
.btn-primary:active,
.btn-primary.active,
.open>.dropdown-toggle.btn-primary {
    color: #ffffff;
    background-color: #178acc;
    border-color: #1684c2
}

.btn-primary:active,
.btn-primary.active,
.open>.dropdown-toggle.btn-primary {
    background-image: none
}

.btn-primary.disabled,
.btn-primary[disabled],
fieldset[disabled] .btn-primary,
.btn-primary.disabled:hover,
.btn-primary[disabled]:hover,
fieldset[disabled] .btn-primary:hover,
.btn-primary.disabled:focus,
.btn-primary[disabled]:focus,
fieldset[disabled] .btn-primary:focus,
.btn-primary.disabled:active,
.btn-primary[disabled]:active,
fieldset[disabled] .btn-primary:active,
.btn-primary.disabled.active,
.btn-primary[disabled].active,
fieldset[disabled] .btn-primary.active {
    background-color: #4ec0da;
    border-color: #4ec0da
}

.btn-primary .badge {
    color: #4ec0da;
    background-color: #ffffff
}
</style>