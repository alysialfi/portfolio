<script setup>
    defineProps([ 'product', 'colors' ])

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
            <div class="flex gap-2 w-1/3 justify-end">
                <span v-for="(color, c) in colors" :key="c" :class="getColorClass(color)" class="w-6 h-6 rounded-full cursor-pointer"></span>
            </div>
            <div class="flex items-center gap-2 w-1/3">
                <button>
                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M12 9v6m3-3H9m12 0a9 9 0 11-18 0 9 9 0 0118 0z" />
                    </svg>                  
                </button>
                <span>5</span>
                <button>
                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M12 9v6m3-3H9m12 0a9 9 0 11-18 0 9 9 0 0118 0z" />
                    </svg>                  
                </button>
            </div>
        </div>
    </div>
</template>