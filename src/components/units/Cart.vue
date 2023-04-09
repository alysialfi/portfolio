<script setup>
    import { ref } from 'vue';

    defineProps([ 'isModalOpen' ])
    const modalState = ref(true)

    function toggleModal() {
        return modalState.value = !modalState.value
    }
</script>

<template>
    <div class="relative w-8 h-8 z-20">
        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.8" stroke="currentColor" @click="$emit('toggleModal', toggleModal())" class="w-8 h-8 text-black cursor-pointer">
            <path stroke-linecap="round" stroke-linejoin="round" d="M2.25 3h1.386c.51 0 .955.343 1.087.835l.383 1.437M7.5 14.25a3 3 0 00-3 3h15.75m-12.75-3h11.218c1.121-2.3 2.1-4.684 2.924-7.138a60.114 60.114 0 00-16.536-1.84M7.5 14.25L5.106 5.272M6 20.25a.75.75 0 11-1.5 0 .75.75 0 011.5 0zm12.75 0a.75.75 0 11-1.5 0 .75.75 0 011.5 0z" />
        </svg>
        <div class="absolute w-5 h-5 text-sm text-center -top-1 -right-2 rounded-full bg-red-700">
            5
        </div>
        <div v-if="isModalOpen" class="absolute -bottom-14 right-0 w-48 p-4 rounded-md bg-white text-black">
            Halo
        </div>
    </div>
</template>