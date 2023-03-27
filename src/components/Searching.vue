<script setup>
    import { onMounted, ref } from 'vue';
    import gsap from 'gsap';
    import { SteppedEase } from 'gsap';

    const typedText = ref(null);

    onMounted(() => {
        gsap.fromTo(typedText.value, 4, {
            width: '0',
            }, {
            scrollTrigger: '#Searching',
            width: '320px',
            ease:  SteppedEase.config(37)
        }, 0);
        gsap.fromTo(typedText.value, 0.3, {
            'border-right-color': 'rgba(255,255,255,0.75)'
            }, {
            'border-right-color': 'rgba(255,255,255,0)',
            repeat: -1,
            ease:  SteppedEase.config(37)
        }, 0);
    })

</script>

<template>
    <div id="Searching" class="w-full h-screen flex justify-center items-center">
        <div id="typed-text" ref="typedText" class="border border-b-0 border-l-0 border-t-0 border-r-white whitespace-nowrap overflow-hidden">
            <p id="text" class="text-lg text-center">these are pretty much what i do for living...</p>
        </div>
    </div>
</template>