<script setup>
    import { onMounted, ref, reactive } from 'vue';

    const isModalOpen = ref(false)
    const states = reactive({
        products: [
            {
                thumbnail: '../../assets/images/products/red-backpack.png',
                title: 'Red Backpack',
                category: 'Woman bag',
                material: '80% leather 20% cotton',
                selectedColor: 'red',
                price: 30
            },
            {
                thumbnail: '../../assets/images/products/anyaman-handbag.png',
                title: 'Anyaman Hand Bag',
                category: 'Woman bag',
                material: '80% leather 20% cotton',
                selectedColor: 'brown',
                price: 50
            },
            {
                thumbnail: '../../assets/images/products/navy-backpack.png',
                title: 'Navy Backpack',
                category: 'Man bag',
                material: '80% cotton 20% polyester',
                selectedColor: 'navy',
                price: 30
            }
        ],
        productColors: [ 'blue', 'red', 'brown', 'yellow' ]
    })
</script>

<template>
    <div class="w-full h-screen">
        <h3>Connecting components in a page? Why not</h3>
    </div>
</template>