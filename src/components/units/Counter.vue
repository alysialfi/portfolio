<script setup>
    import { ref, watch } from 'vue';
    const props = defineProps([ 'item' ])
    const emit = defineEmits([ 'get-detail-data' ])

    const amount = ref(props.item.amount)

    watch(amount, (newAmount) => {
        emit('get-detail-data', {id: props.item.id, amount: amount.value})
    })
</script>

<template>
    <div class="flex items-center gap-2 w-full">
        <button @click="amount--" :disabled="amount === 0" class="disabled:text-gray-500">
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
                <path stroke-linecap="round" stroke-linejoin="round" d="M15 12H9m12 0a9 9 0 11-18 0 9 9 0 0118 0z" />
            </svg>
        </button>
        <span>{{ item.amount }}</span>
        <button @click="amount++">
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
                <path stroke-linecap="round" stroke-linejoin="round" d="M12 9v6m3-3H9m12 0a9 9 0 11-18 0 9 9 0 0118 0z" />
            </svg>
        </button>
    </div>
</template>
