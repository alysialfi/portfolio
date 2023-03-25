<template>
    <div class="relative w-full h-screen">
        <div class="w-full h-full hidden md:block">
            <img id="cat" ref="cat" src="../assets/images/header/cat.svg" alt="a lined big cat body"
            class="absolute left-1/2 bottom-0 -translate-x-1/2 translate-y-0 opacity-0">
            <div id="cat-face" class="h-[90%] w-full absolute bottom-0">
                <div class="flex justify-center items-start md:pt-[18%] lg:pt-[15%] xl:pt-[11%] pl-10">
                    <img id="cat-face-inner" src="../assets/images/header/cat-face.svg" alt="" srcset="" class="opacity-0">
                </div>
                <div ref="mustacheLeft" class="absolute bottom-[35%] md:left-[9%] lg:left-[15%] xl:left-1/4">
                    <img src="../assets/images/header/mustache-left.svg" alt="" srcset="">
                </div>
                <div ref="mustacheRight" class="absolute bottom-[38%] md:right-[5%] lg:right-[15%] xl:right-[22%]">
                    <img src="../assets/images/header/mustache-right.svg" alt="" srcset="">
                </div>
            </div>
            <div ref="subTitleLeft" class="absolute bottom-16 left-16">
                <h3 class="text-base font-normal">
                    she/her <br>
                    Indonesian and <br>
                    a wanderlust
                </h3>
            </div>
            <div id="title" ref="title" class="w-full h-screen flex justify-center items-end pb-8">
                <h1 class="text-[9vw] font-normal text-center">Hi! It's <span class="text-[16vw] font-semibold">Alfi</span></h1>
            </div>
            <div ref="subTitleRight" class="absolute top-1/4 2xl:top-1/3 right-16">
                <h3 class="text-base font-normal">
                    so called front end developer <br>
                    sometimes do back end-ish <br>
                    things
                </h3>
            </div>
            <div ref="arrowDown" class="absolute bottom-10 left-1/2 -translate-x-1/2">
                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1" stroke="currentColor" class="w-12 h-12 text-yellow-200">
                    <path stroke-linecap="round" stroke-linejoin="round" d="M9 12.75l3 3m0 0l3-3m-3 3v-7.5M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
                </svg>
            </div>
        </div>
        <div class="block md:hidden">
            <img src="../assets/images/header/cat-small.svg" alt="" class="mt-10">
            <div class="mx-8">
                <h1>
                    <span class="text-7xl">Hi!</span> <br>
                    <span class="text-8xl">it's </span>
                    <span class="text-9xl font-semibold">Alfi</span>
                </h1>
                <h2 class="text-xl font-extralight mt-4">
                    so called front end developer sometimes do back end-ish things
                </h2>
                <h3 class="text-xl font-extralight mt-3">
                    she/her <br>
                    Indonesian and a wanderlust
                </h3>
            </div>
        </div>
    </div>
</template>