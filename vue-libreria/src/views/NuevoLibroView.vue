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
            <button class="btn enviar" type="submit">Agregar Libro</button>
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
    background-color: #14bd19;
    color: #fff;
    margin-top: 20px;
}

.enviar:hover {
    background-color: #00ff0da5;
    color: #fff;
}
</style>