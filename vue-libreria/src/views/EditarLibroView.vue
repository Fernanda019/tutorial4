<script>
import axios from 'axios';
import { ref, onMounted } from 'vue';
import { useRoute } from 'vue-router';

export default {
    name: 'EditarLibroView',
    setup() {
        const route = useRoute();

        const editarLibro = ref({
            id: null,
            titulo: '',
            autor: '',
            ISBN: '',
            genero: '',
            precio: '',
            disponibilidad: ''
        })

        const cargarLibro = async () => {
            try {
                const response = await axios.get(`/api/libros/${route.params.id}`);
                editarLibro.value = response.data;
            } catch (error) {
                console.error('Error al cargar el libro:', error);
                alert("Error al cargar el libro. Por favor, inténtalo de nuevo.");
            }
        };

        const actualizarLibro = async () => {
            try {
                await axios.put(`/api/libros/${actualizarLibro.value.id}`, actualizarLibro.value);
                alert("Libro actualizado exitosamente.");
                // Aquí podrías redirigir al usuario a otra página o limpiar el formulario
            } catch (error) {
                console.error('Error al actualizar el libro:', error);
                alert("Error al actualizar el libro. Por favor, inténtalo de nuevo.");
            }
        };

        onMounted(() => {
            cargarLibro();
        });

        return{
            editarLibro,
            actualizarLibro,
        }

    }
};
</script>

<template>
    <main>
        <form @submit.prevent="actualizarLibro">
            <div>
                <div>
                    <label for="titulo">Título</label>
                    <input name="titulo" v-model="editarLibro.titulo" type="text" required placeholder="Título">
                </div>
                <div>
                    <label for="autor">Autor</label>
                    <input name="autor" v-model="editarLibro.autor" type="text" required placeholder="Autor">
                </div>
                <div>
                    <label for="ISBN">ISBN</label>
                    <input name="ISBN" v-model="editarLibro.ISBN" type="text" required placeholder="ISBN">
                </div>
                <div>
                    <label for="genero">Género</label>
                    <input name="genero" v-model="editarLibro.genero" type="text" required placeholder="Género">
                </div>
                <div>
                    <label for="precio">Precio</label>
                    <input name="precio" v-model="editarLibro.precio" type="text" required placeholder="Precio">
                </div>
                <div>
                    <label for="disponibilidad">Disponibilidad</label>
                    <input name="disponibilidad" v-model="editarLibro.disponibilidad" type="text" required placeholder="Disponibilidad">
                </div>
            </div>
            <button class="btn enviar" type="submit">Guardar Cambios</button>
        </form>
    </main>
</template>

<style scoped>
form {
    width: 90%;
    margin: 25px auto;
    padding: 20px;
    border: 1px solid #000000;
    box-shadow: 0 0 20px rgba(0, 0, 0, 0.2);
}

label {
    font-weight: bold;
    margin-bottom: 5px;
    display: block;
    font-size: 1rem;
}

input {
    width: 100%;
    padding: 5px;
    border: 1px solid #000000;
    margin-bottom: 15px;
    font-family: "Open Sans", sans-serif;
    font-size: 1rem;
}

input:focus {
    outline: none;
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
    width: 100%;
}

.enviar {
    margin-top: 20px;
    background-color: #14bd19;
    color: #fff;
}

.enviar:hover {
    background-color: #00ff0da5;
    color: #fff;
}
</style>