<template>
    <div class="row mt-5">
        <div class="col-md-6 text-center text-md-start pt-5">
            <h1 class="display-2 fw-bold">Modelo {{ promoGuitar.nombre }}</h1>
            <p class="mt-5 fs-5 text-white">{{ promoGuitar.descripcion }}</p>
            <p class="text-primary fs-1 fw-black">{{ promoGuitar.precio }} €</p>
            <button @click="$emit('agregarCarrito', promoGuitar)"
                type="button"
                class="btn fs-4 bg-primary text-white py-2 px-5"
            >Agregar al Carrito</button>
        </div>
    </div>
</template>

<script setup>
    defineProps({
        promoGuitar: {
            type: Object,
            required: true
        }
    });

    
    defineEmits(['agregarCarrito']);
</script>