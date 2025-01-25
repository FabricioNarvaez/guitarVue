<template>
    <HeaderComponent :cart="cart" :promoGuitar="promoGuitar"
    @agregarCarrito="agregarCarrito" @emptyCart="emptyCart" @deleteGuitar="deleteGuitar"/>

    <main class="container-xl mt-5">
        <h2 class="text-center">Nuestra Colección</h2>

        <div class="row mt-5">
            <Guitar v-for="guitar in guitars" :guitar="guitar" @agregarCarrito="agregarCarrito" />
        </div>
    </main>

    <FooterComponent />
</template>

<script setup>
    import { ref, reactive, onMounted, watch } from "vue";
    import { db } from "./data/guitarras";

    import HeaderComponent from "./components/Header.vue";
    import FooterComponent from "./components/Footer.vue";
    import Guitar from "./components/Guitar.vue";

    const guitars = ref(db);
    const cart = ref([]);
    const promoGuitar = ref({});

    const promoGuitarName = "VAI";
    promoGuitar.value = guitars.value.find((guitar) => guitar.nombre === promoGuitarName);

    const saveCartOnLocalStorage = () => {
        localStorage.setItem('cart', JSON.stringify(cart.value));
    }

    const agregarCarrito = (guitar) => {
        const existItem = cart.value.find((item) => item.id === guitar.id);
        if (existItem) {
            existItem.amount++;
        } else {
            cart.value.push(guitar);
            guitar.amount = 1;
        };
    };

    const emptyCart = () => {
        cart.value = [];
    };

    const deleteGuitar = (guitar) =>{
        const foundIndex = cart.value.findIndex(item => item.id === guitar.id);
        cart.value.splice(foundIndex, 1);
    };

    onMounted(()=>{
        const cartStorage = localStorage.getItem('cart');
        if(cartStorage){
            cart.value = JSON.parse(cartStorage);
        }

        watch(cart.value, ()=>{saveCartOnLocalStorage();});
    });
</script>