<script setup>
    import { onMounted, ref, reactive } from 'vue';
    import ProductDisplay from "./units/ProductDetail.vue";
    import Cart from "./units/Cart.vue";

    const isModalOpen = ref(false)
    const states = reactive({
        products: [
            {
                id: 0,
                thumbnail: '../../assets/images/products/red-backpack.png',
                title: 'Red Backpack',
                category: 'Woman bag',
                material: '80% leather 20% cotton',
                selectedColor: 'red',
                price: 30,
                amount: 0
            },
            {
                id: 1,
                thumbnail: '../../assets/images/products/anyaman-handbag.png',
                title: 'Anyaman Hand Bag',
                category: 'Woman bag',
                material: '80% leather 20% cotton',
                selectedColor: 'brown',
                price: 50,
                amount: 0
            },
            {
                id: 2,
                thumbnail: '../../assets/images/products/navy-backpack.png',
                title: 'Navy Backpack',
                category: 'Man bag',
                material: '80% cotton 20% polyester',
                selectedColor: 'navy',
                price: 30,
                amount: 0
            }
        ],
        productColors: [ 'blue', 'red', 'brown', 'yellow' ]
    })

    function getOrRemoveProductCart(data) {
        const selectedCartProduct = states.products.find((product) => product.id === data.id)
        selectedCartProduct.amount = data.amount
    }
</script>

<template>
    <div id="Component" class="flex w-full h-screen items-end justify-center flex-wrap">
        <div class="w-full font-semibold text-2xl text-center">Connecting components in a page? Why not</div>
        <div class="relative w-4/5 px-32 pt-10 bg-white rounded-t-3xl bottom-0">
            <div v-if="isModalOpen" @click="isModalOpen = false" class="absolute w-full h-full top-0 right-0 bg-black bg-opacity-50 z-0"></div>
            <div class="flex justify-end mb-4">
                <Cart :isModalOpen="isModalOpen" :products="states.products" @toggle-modal="(val) => isModalOpen = val" @get-product-for-cart="getOrRemoveProductCart"></Cart>
            </div>
            <ProductDisplay v-for="(product, p) in states.products" :key="p" :product="product" :colors="states.productColors" @get-product-for-cart="getOrRemoveProductCart" class="mb-4"></ProductDisplay>
        </div>
    </div>
</template>
