<script setup>
    import { onMounted, ref, reactive } from 'vue';
    import gsap from 'gsap';
    import { SteppedEase } from 'gsap';

    const typedText = ref(null);
    const query = ref('');
    const queryResult = ref(null);
    const isSearching = ref(false);
    const states = reactive({
        queryHistories: [],
        selectedHistories: []
    });

    async function submitQuery() {
        queryResult.value = '';
        isSearching.value = true;
        queryResult.value = await callAPIWikipedia()
        storeQueryToHistory()
        isSearching.value = false;
    }

    async function callAPIWikipedia() {
        const api = await fetch(`https://en.wikipedia.org/w/api.php?format=json&action=query&prop=extracts&exintro&explaintext&redirects=1&redirects=1&titles=${query.value}`);
        const response = await api.json()
        const pageid = Object.keys(response.query.pages)[0]
        return response.query.pages[pageid].extract
    }

    function storeQueryToHistory() {
        states.queryHistories.push(query.value)
    }

    function deleteHistory() {
        states.selectedHistories.forEach((history) => {
            states.queryHistories.splice(history, 1)
        })
        states.selectedHistories = []
    }

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
    <div id="Searching" class="w-full h-screen">
        <div class="flex w-full justify-center items-center">
            <div id="typed-text" ref="typedText" class="border border-b-0 border-l-0 border-t-0 border-r-white whitespace-nowrap overflow-hidden">
                <p id="text" class="text-lg text-center m-auto">these are pretty much what i do for living...</p>
            </div>
        </div>
        <div id="search-box" class="opacity-0 px-10 md:p-0">
            <div class="w-full mt-28 text-center text-2xl font-semibold">API Consume/searching/filtering? Got em</div>
            <div class="flex w-full justify-center">
                <div class="m-auto w-full md:w-1/2 mt-6 relative">
                    <div class="w-full">
                        <input type="text" name="search-input" id="search-input" v-model="query" @keyup.enter="submitQuery" placeholder="ask Wikipedia anything..."
                        class="w-full h-10 p-4 text-black rounded-md">
                        <div class="absolute right-4 top-2.5">
                            <svg v-if="!query.length" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor" class="w-5 h-5 text-black">
                                <path stroke-linecap="round" stroke-linejoin="round" d="M21 21l-5.197-5.197m0 0A7.5 7.5 0 105.196 5.196a7.5 7.5 0 0010.607 10.607z" />
                            </svg>
                            <svg v-else xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" @click="query = ''" class="w-5 h-5 text-black cursor-pointer">
                                <path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
                            </svg>
                        </div>
                    </div>
                    <div class="w-full mt-4">
                        <div v-if="isSearching" class="w-full flex justify-center gap-3 mb-4">
                            <span class="block w-4 h-4 bg-white rounded-full animate-[ping_1.5s_ease-in-out_infinite]"></span>
                            <span class="block w-4 h-4 bg-white rounded-full animate-[ping_2.5s_ease-in-out_infinite]"></span>
                            <span class="block w-4 h-4 bg-white rounded-full animate-[ping_1.5s_ease-in-out_infinite]"></span>
                        </div>
                        <p v-if="queryResult === undefined" class="text-center">
                            Uh no. There's no related answer :(
                        </p>
                        <div v-else :class="queryResult === null || isSearching ? 'h-0' : 'h-60 px-4 py-2'" class="bg-white text-black rounded-md transition-[height] duration-300 overflow-scroll">
                            <span>
                                {{ queryResult }}
                            </span>
                        </div>
                    </div>
                    <div class="w-full mt-6 h-60 overflow-scroll">
                        <div class="flex justify-between pb-1 bg-black border border-b-white border-l-0 border-t-0 border-r-0 sticky top-0">
                            <span class="block w-[95%]">Recent queries</span>
                            <span class="block ml-auto">
                                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-5 h-5 cursor-pointer" @click="deleteHistory()">
                                    <path stroke-linecap="round" stroke-linejoin="round" d="M14.74 9l-.346 9m-4.788 0L9.26 9m9.968-3.21c.342.052.682.107 1.022.166m-1.022-.165L18.16 19.673a2.25 2.25 0 01-2.244 2.077H8.084a2.25 2.25 0 01-2.244-2.077L4.772 5.79m14.456 0a48.108 48.108 0 00-3.478-.397m-12 .562c.34-.059.68-.114 1.022-.165m0 0a48.11 48.11 0 013.478-.397m7.5 0v-.916c0-1.18-.91-2.164-2.09-2.201a51.964 51.964 0 00-3.32 0c-1.18.037-2.09 1.022-2.09 2.201v.916m7.5 0a48.667 48.667 0 00-7.5 0" />
                                </svg>
                            </span>
                        </div>
                        <div v-for="(history, h) in states.queryHistories" :key="h" class="mt-2">
                            <input type="checkbox" name="" :id="`qh-${h}`" :value="h" v-model="states.selectedHistories" class="border-none outline-none peer">
                            <label :for="`qh-${h}`" class="ml-2 peer-checked:font-semibold">{{ history }}</label>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
