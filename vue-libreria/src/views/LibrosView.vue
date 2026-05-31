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
                    <td class="alinear">{{ libro.id }}</td>
                    <td>{{ libro.titulo }}</td>
                    <td>{{ libro.ISBN }}</td>
                    <td>{{ libro.genero }}</td>
                    <td class="alinear">{{ libro.precio }}</td>
                    <td>{{ libro.disponibilidad }}</td>
                    <div class="botones">
                        <button class="btn eliminar" @click="eliminarLibro(libro.id,libro.titulo)">
                            Eliminar
                        </button>
                        <router-link class="btneditar" :to="`/editarLibro/${libro.id}`">
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

<style scoped>
table {
    width: 90%;
    border-collapse: collapse;
    margin: 25px auto;
    box-shadow: 0 0 20px rgba(0, 0, 0, 0.2);
}

th, td {
    border: 1px solid #000000;
    padding: 10px;
}

th {
    background-color: #e2e2e2;
}

.alinear {
    text-align: center;
}

.botones {
    display: flex;
    justify-content: space-around;
    border: solid 1px #505050;
}

.btn {
    background-color: transparent;
    border: none;
    padding: 10px 15px;
    text-decoration: none;
    font-family: "Open Sans", sans-serif;
    color:#000000;
    font-size: 1rem;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s ease-in-out;
    margin: 5px;
}

.eliminar {
    background-color: #ff0000;
    color: #fff;
}

.eliminar:hover {
    background-color: #ff00009d;
    color: #fff;
}

.editar {
    background-color: #ffea00c7;
    color: #fff;
}

.editar:hover {
    background-color: #b2a402;
    color: #fff;
}
</style>