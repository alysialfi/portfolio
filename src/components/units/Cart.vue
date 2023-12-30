<script setup>
    import Counter from './Counter.vue'
    import { ref } from 'vue';

    const props = defineProps([ 'isModalOpen', 'products' ])
    const emit = defineEmits([ 'get-product-for-cart' ])
    const modalState = ref(true)

    function toggleModal() {
        return modalState.value = !modalState.value
    }
    function renderImgSrc(src) {
        return new URL(src, import.meta.url).href
    }

    function getProductDetail(data) {
        emit('get-product-for-cart', data)
    }

    function getProductLength() {
        if (props.products.length) {
            const arr = props.products.filter((product) => product.amount > 0);
            return arr.length
        }
    }
</script>

<template>
    <div class="relative w-8 h-8 z-20">
        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.8" stroke="currentColor" @click="$emit('toggleModal', toggleModal())" class="w-8 h-8 text-black cursor-pointer">
            <path stroke-linecap="round" stroke-linejoin="round" d="M2.25 3h1.386c.51 0 .955.343 1.087.835l.383 1.437M7.5 14.25a3 3 0 00-3 3h15.75m-12.75-3h11.218c1.121-2.3 2.1-4.684 2.924-7.138a60.114 60.114 0 00-16.536-1.84M7.5 14.25L5.106 5.272M6 20.25a.75.75 0 11-1.5 0 .75.75 0 011.5 0zm12.75 0a.75.75 0 11-1.5 0 .75.75 0 011.5 0z" />
        </svg>
        <div v-if="getProductLength() > 0" class="absolute w-5 h-5 text-sm text-center -top-1 -right-2 rounded-full bg-red-700">
            {{ getProductLength() }}
        </div>
        <div v-if="isModalOpen" class="absolute top-10 right-0 w-96 p-4 pb-8 rounded-md bg-white text-black overflow-scroll">
            <div v-if="getProductLength() > 0" class="h-96">
                <div class="bg-white font-semibold text-lg pb-1 border border-b-gray-300 border-t-0 border-l-0 border-r-0">
                    Cart ({{ getProductLength() }})
                </div>
                <div v-for="(product, p) in products" :key="p" class="mt-2 w-full flex gap-2">
                    <div v-if="product.amount > 0" class="w-full flex pb-1 border border-b-gray-300 border-t-0 border-l-0 border-r-0">
                        <img :src="renderImgSrc(product.thumbnail)" alt="" class="w-16">
                        <div class="flex-1">
                            <p class="font-semibold">{{ product.title }}</p>
                            <p>color: {{ product.selectedColor }}</p>
                            <p class="font-semibold mt-1">${{ product.price }}</p>
                        </div>
                        <div class="flex items-center gap-2 w-20 justify-end">
                            <Counter :item="product" @get-detail-data="getProductDetail"></Counter>
                        </div>
                    </div>
                </div>
            </div>
            <div v-else class="text-center h-3">
                Your cart is empty :(
            </div>
        </div>
    </div>
</template>
