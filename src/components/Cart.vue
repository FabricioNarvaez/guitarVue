<template>
    <div class="row justify-content-center justify-content-md-between">
        <div class="col-8 col-md-3">
            <a href="index.html">
                <img class="img-fluid" src="/img/logo.svg" alt="imagen logo">
            </a>
        </div>
        <nav class="col-md-6 a mt-5 d-flex align-items-start justify-content-end">
            <div class="carrito">
                <img @click="toggleCart" class="img-fluid cartImage" src="/img/carrito.png" alt="imagen carrito" />

                <div id="carrito" :class="{'cartActive': isCartOpened}" class="bg-white p-3">
                    <p v-if="!cart.length" class="text-center">El carrito esta vacío</p>
                    <div v-else>
                        <table class="w-100 table">
                            <thead>
                                <tr>
                                    <th>Imagen</th>
                                    <th>Nombre</th>
                                    <th>Precio</th>
                                    <th>Cantidad</th>
                                    <th></th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr v-for="cartItem in cart">
                                    <td>
                                        <img class="img-fluid" :src="`/img/${cartItem.imagen}.jpg`" :alt="`imagen guitarra ${cartItem.nombre}`">
                                    </td>
                                    <td>{{ cartItem.nombre }}</td>
                                    <td class="fw-bold">{{ cartItem.precio }}</td>
                                    <td class="flex align-items-start gap-4">
                                        <button @click="decreaseAmount(cartItem)" type="button" class="btn btn-dark">
                                            -
                                        </button>
                                        {{ cartItem.amount }}
                                        <button @click="increaseAmount(cartItem)" type="button" class="btn btn-dark">
                                            +
                                        </button>
                                    </td>
                                    <td>
                                        <button @click="$emit('deleteGuitar', cartItem)" class="btn btn-danger" type="button">
                                            X
                                        </button>
                                    </td>
                                </tr>
                            </tbody>
                        </table>

                        <p class="text-end">Total pagar: <span class="fw-bold">{{ cartTotal }} €</span></p>
                        <button @click="$emit('emptyCart')" class="btn btn-dark w-100 mt-3 p-2">Vaciar Carrito</button>
                    </div>
                </div>
            </div>
        </nav>
    </div>
</template>

<script setup>
    import { computed, ref } from 'vue';

    const isCartOpened = ref(false);
    const props = defineProps({
        cart: {
            type: Array,
            required: true
        }
    });

    const toggleCart = () => { isCartOpened.value = !isCartOpened.value;};const cartTotal = computed(() => props.cart.reduce((acc, item) => acc + item.precio * item.amount, 0));
    
    const increaseAmount = (guitar)=> { guitar.amount++ };
    const decreaseAmount = (guitar)=> { if(guitar.amount > 0) guitar.amount-- };
   
</script>

<style>
    .cartImage {
        transition: all 0.3s ease-in-out;
    }

    .cartImage:hover {
        transform: scale(1.2);
    }
</style>