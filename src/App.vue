<template>
    <HeaderComponent :cart="cart" :promoGuitar="promoGuitar" @agregarCarrito="agregarCarrito"/>

    <main class="container-xl mt-5">
        <h2 class="text-center">Nuestra Colección</h2>

        <div class="row mt-5">
            <Guitar v-for="guitar in guitars" :guitar="guitar" @agregarCarrito="agregarCarrito" />
        </div>
    </main>

    <FooterComponent />
</template>

<script setup>
    import { ref, reactive } from "vue";
    import { db } from "./data/guitarras";

    import HeaderComponent from "./components/HeaderComponent.vue";
    import FooterComponent from "./components/FooterComponent.vue";
    import Guitar from "./components/Guitar.vue";

    const guitars = ref(db);
    const cart = ref([]);
    const promoGuitar = ref({});

    const promoGuitarName = "VAI";
    promoGuitar.value = guitars.value.find((guitar) => guitar.nombre === promoGuitarName);

    const agregarCarrito = (guitar) => {
        const existItem = cart.value.find((item) => item.id === guitar.id);
        if (existItem) {
            existItem.amount++;
        } else {
            cart.value.push(guitar);
            guitar.amount = 1;
            console.log(cart.value);
        }
    }
</script>