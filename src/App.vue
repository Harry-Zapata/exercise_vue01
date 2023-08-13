<template>
    <div class="container">
        <div>
            <h1>
                Cena {{ contador }} con el rey godo
                <span style="color: green;">
                    {{ reyes[contador - 1].nombre.charAt(0).toUpperCase() + reyes[contador -
                        1].nombre.slice(1).toLowerCase() }}
                </span>
            </h1>

            <h2>Precio: <span style="color: green;">{{ reyes[contador - 1].precio }}$</span></h2>

            <div class="fines">
                <h3 v-if="reyes[contador - 1].finDeSemana" style="background: red;">(Solo Fines de semana)</h3>
                <h3 v-else style="background: green;">(De lunes a domingo)</h3>
            </div>

            <div class="oferta" v-if="reyes[contador - 1].precio < 100">
                <p>Ahora un 10% dto:
                    <span>
                        {{ reyes[contador - 1].precio - (reyes[contador - 1].precio * 0.1) }}
                    </span>
                </p>
                <img src="oferta.jpg" style="width: 10%;" alt="oferta">
            </div>
            <img style="width: 50%;" :src="url + reyes[contador - 1].nombre + '.png'" alt="">

        </div>
        <div class="paginador">
            <button @click="restar">Anterior</button>
            <p class="contador">{{ contador }}</p>
            <button @click="sumar">Siguiente</button>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue';
import { productos } from './datos.js';

const contador = ref(1);
const reyes = ref(productos);
const url = "https://www.html6.es/img/rey-"
const sumar = () => {
    if (reyes.value.length > contador.value) {
        contador.value++;
    } else {
        contador.value = 1
    }
};

const restar = () => {
    if (contador.value <= 1) {
        contador.value = reyes.value.length
    } else {
        contador.value--
    }
};


;
</script>


<style scoped>
* {
    font-family: monospace;
    text-align: center;
}

.container {
    width: 500px;
    height: 500px;
    border: 1px solid black;
    padding: 20px;
    position: relative;
}

.paginador {
    position: absolute;
    bottom: 10px;
    width: 100%;
}

button,
p {
    display: inline;
}

button {
    width: 100px;
}

.fines,
.oferta {
    display: flex;
    justify-content: center;
}

.contador {
    padding: 0 20px;
}

h3 {
    width: 60%;
}</style>