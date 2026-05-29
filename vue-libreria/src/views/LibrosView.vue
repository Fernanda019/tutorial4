<script>
import router from '@/router';
import axios from 'axios';
import { ref, onMounted } from 'vue';

export default {
    name: 'LibrosView',
    setup() {
        const libros = ref([]);

        onMounted(() => {
            axios.get('/api/libros')
              .then(response => {
                  console.log("RESPUESTA COMPLETA:", response.data);
                  libros.value = response.data;
              })
                .catch(error => {
                    console.error('Error al obtener los libros:', error);
                });
        });

        const eliminarLibro = async (id, titulo) => {
            const confirmDelete = window.confirm(
                `¿Estás seguro de que deseas eliminar el libro '${titulo}'?`
            );
            if (confirmDelete) {
                try {
                    await axios.delete(`/api/libros/${id}`);
                } catch (error) {
                    console.error('Error al eliminar el libro:', error);
                }
            }

            onMounted(()=>{
                listarLibros();
            })
        };
        return {
            libros,
            listarLibros,
        };
    }
};

</script>

<template>
    <main>
        <table>
            <thead>
                <tr>
                    <th>id</th>
                    <th>Titulo</th>
                    <th>ISBN</th>
                    <th>Genero</th>
                    <th>Precio</th>
                    <th>Disponibilidad</th>
                    <th>Acciones</th>
                </tr>
            </thead>

            <tbody>
                <tr v-for="libro in libros" :key="libro.id">
                    <td>{{ libro.id }}</td>
                    <td>{{ libro.titulo }}</td>
                    <td>{{ libro.ISBN }}</td>
                    <td>{{ libro.genero }}</td>
                    <td>{{ libro.precio }}</td>
                    <td>{{ libro.disponibilidad }}</td>
                    <div>
                        <button @click="eliminarLibro(libro.id,libro.titulo)">
                            Eliminar
                        </button>
                        <router-link :to="`/editarLibro/${libro.id}`">
                            <button>
                                Editar
                            </button>
                        </router-link>
                    </div>
                </tr>
            </tbody>
        </table>
    </main>
</template>

<style>
</style>