<template>
    <header class="py-5 header">
        <div class="container-xl">
            <Cart :cart="cart" @deleteGuitar="handleDeleteGuitar" @emptyCart="handleEmptyCart"/>

            <PromoGuitar :promoGuitar="promoGuitar" @agregarCarrito="handleAgregarCarrito"/>
        </div>

        <img class="header-guitarra" src="/img/header_guitarra.png" alt="imagen header">
    </header>
</template>

<script setup>
    import PromoGuitar from './PromoGuitar.vue';
    import Cart from './Cart.vue';

    const props = defineProps({
        cart: {
            type: Array,
            required: true
        },
        promoGuitar: {
            type: Object,
            required: true
        }
    });

    const emit = defineEmits(['agregarCarrito', 'emptyCart', 'deleteGuitar']);
    
    const handleDeleteGuitar = (guitar)=> {emit('deleteGuitar', guitar)};
    const handleAgregarCarrito = (guitar)=> {emit('agregarCarrito', guitar)};
    const handleEmptyCart = ()=> {emit('emptyCart')};
    
</script>