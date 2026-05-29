<script>
import { ref } from 'vue';
import axios from 'axios';

export default {
    setup() {

        const nuevoLibro = ref({
            titulo: '',
            autor: '',
            ISBN: '',
            genero: '',
            precio: '',
            disponibilidad: ''
        })

        const agregarLibro = async () => {
            try {
                await axios.post('/api/libros', nuevoLibro.value);
                alert("Libro agregado exitosamente.");
                // Limpiar el formulario después de agregar el libro
                nuevoLibro.value = {
                    titulo: '',
                    autor: '',
                    ISBN: '',
                    genero: '',
                    precio: '',
                    disponibilidad: ''
                };
            } catch (error) {
                console.error('Error al agregar el libro:', error);
                alert("Error al agregar el libro. Por favor, inténtalo de nuevo.");
            }
        };

        return{
            nuevoLibro,
            agregarLibro,
        }

    }
};
        
</script>

<template>
    <main>
        <form @submit.prevent="agregarLibro">
            <div>
                <div>
                    <label for="titulo">Título</label>
                    <input name="titulo" v-model="nuevolibro.titulo" type="text" required placeholder="Título">
                </div>
                <div>
                    <label for="autor">Autor</label>
                    <input name="autor" v-model="nuevolibro.autor" type="text" required placeholder="Autor">
                </div>
                <div>
                    <label for="ISBN">ISBN</label>
                    <input name="ISBN" v-model="nuevolibro.ISBN" type="text" required placeholder="ISBN">
                </div>
                <div>
                    <label for="genero">Género</label>
                    <input name="genero" v-model="nuevolibro.genero" type="text" required placeholder="Género">
                </div>
                <div>
                    <label for="precio">Precio</label>
                    <input name="precio" v-model="nuevolibro.precio" type="text" required placeholder="Precio">
                </div>
                <div>
                    <label for="disponibilidad">Disponibilidad</label>
                    <input name="disponibilidad" v-model="nuevolibro.disponibilidad" type="text" required placeholder="Disponibilidad">
                </div>
            </div>
            <button type="submit">Agregar Libro</button>
        </form>
    </main>
</template>

<style>

</style>