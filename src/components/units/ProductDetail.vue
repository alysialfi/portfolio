<script setup>
    import Counter from './Counter.vue'
    defineProps([ 'product', 'colors' ])
    const emit = defineEmits([ 'get-product-for-cart' ])

    function renderImgSrc(src) {
        return new URL(src, import.meta.url).href
    }
    function getColorClass(color) {
        const colorLibs = {
            blue: 'bg-blue-800',
            red: 'bg-red-500',
            brown: 'bg-amber-900',
            yellow: 'bg-yellow-400'
        }
        return colorLibs[color]
    }

    function getProductDetail(data) {
        emit('get-product-for-cart', data)
    }
</script>

<template>
    <div class="bg-gray-100 rounded-lg flex px-4 py-2 justify-between text-black">
        <div class="flex items-center gap-4 w-1/2">
            <img :src="renderImgSrc(product.thumbnail)" alt="" srcset=""/>
            <div class="flex flex-col justify-center text-gray-500">
                <p class="font-bold text-xl text-black">{{ product.title }}</p>
                <p>{{ product.category }}</p>
                <p>{{ product.material }}</p>
                <p class="font-semibold text-gray-600 mt-1">color: {{ product.selectedColor }}</p>
            </div>
        </div>
        <div class="flex items-center justify-between w-1/2 gap-8">
            <span class="w-1/3 text-right font-bold text-xl">${{ product.price }}</span>
            <div class="flex gap-2 w-28 justify-end">
                <div v-for="(color, c) in colors" :key="c" class="flex">
                    <span @click="tes" :class="getColorClass(color)" class="w-6 h-6 rounded-full cursor-pointer"></span>
                </div>
            </div>
            <div class="flex justify-end">
                <Counter :item="product" @get-detail-data="getProductDetail"></Counter>
            </div>
        </div>
    </div>
</template>