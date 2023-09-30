
<template>
    <div
      class="text-center mt-5 border border-black border-1 rounded bg-gray-100 text-black"
      style="white-space: nowrap"
    >
      <div class="sm:text-2xl flex justify-center">
        <h1>
          Cena {{ id + 1 }} con el rey godo&nbsp;
        </h1>
        <h1 :class="colorTitulo">
          {{ nombre }}
        </h1>
      </div>
  
      <div class="sm:text-2xl flex justify-center mt-2">
        <h2>Precio:&nbsp; </h2>
        <h2 :class="colorTitulo">
          {{ precio }}€
        </h2>
      </div>
  
      <div class="sm:text-2xl mt-2 flex justify-center">
        <button
          v-if="finDeSemana"
          class="btn bg-red-600 text-white rounded py-2 px-4"
          disabled
        >
          (Solo fines de semana)
        </button>
        <button
          v-else-if="!finDeSemana"
          class="btn bg-green-600 text-white rounded py-2 px-4"
          disabled
        >
          (De lunes a viernes)
        </button>
      </div>
  
      <div :class="{ 'invisible': mensaje }" class="flex justify-center mt-2">
        <span>Ahora un 10% de descuento &nbsp;</span>
        <span :class="colorTitulo, mensaje">{{ precioDescuento }}€</span>
        <img :src="oferta" class="img" width="40" height="40">
      </div>
  
      <br>
  
      <br>
  
      <img
        class="flex justify-center items-center mx-auto mt-2"
        :src="imagen"
        alt=""
      >
  
      <button
        class="btn bg-gray-200 text-black rounded py-2 px-4 mt-4 mb-4 sm:text-2xl"
        @click="increment()"
      >
        Siguiente {{ id + 1 }}/{{ productos.length }}
      </button>
    </div>
  </template>

<script setup>
import { ref, computed } from 'vue';

// DATA
const productos = [
    {
        nombre: "ervigio",
        precio: 110,
        finDeSemana: true
    }, {
        nombre: "ATANAGILDO",
        precio: 125,
        finDeSemana: false
    }, {
        nombre: "LEOVIGILDO",
        precio: 73,
        finDeSemana: true
    }, {
        nombre: "ATAULFO",
        precio: 69,
        finDeSemana: true
    }, {
        nombre: "SISEBUTO",
        precio: 105,
        finDeSemana: false
    }, {
        nombre: "TEODORICO",
        precio: 112,
        finDeSemana: true
    }, {
        nombre: "RECESVINTO",
        precio: 71,
        finDeSemana: false
    }
]

const id = ref(0);

// Tranforma el nombre en capitalize
const nombre = computed(() => {
    const capName = productos[id.value].nombre.toLocaleLowerCase();
    return capName.charAt(0).toUpperCase() + capName.slice(1);
})


const precio = ref(productos[0].precio)
const finDeSemana = ref(productos[0].finDeSemana);
const finDeSemanaColor = ref('green');

const descuento = ref(false);
const mensaje = ref('invisible');

const oferta = "/oferta.jpg"


const precioDescuento = computed(() => {
    return (precio.value - (precio.value * 10 / 100)).toFixed(2)
})

const imagen = computed(() => {
    const rey = nombre.value.toLowerCase();
    return `https://www.html6.es/img/rey_${rey}.png`;
})



const colorTitulo = ref('green');

const increment = () => {
    id.value++;

    if (id.value >= productos.length) {
        id.value = 0;
    }

    precio.value = productos[id.value].precio;
    finDeSemana.value = productos[id.value].finDeSemana;

    if (!finDeSemana.value) {
        finDeSemanaColor.value = 'red';
    } else {
        finDeSemanaColor.value = 'green';
    }

    if (precio.value < 100) {
        descuento.value = true;
        mensaje.value = '';

    }
    else {
        descuento.value = false;
        mensaje.value = 'invisible';
    }
}
</script>

<style scoped>
.custom-card {
  margin-left: 0;
  margin-right: 0;
}
.green {
    color: green;

}

.red {
    color: red;
}
</style>