<template>
    <div class="rounded-lg border border-grayD9">
        <!-- imagen -->
        <figure class="h-1/2 w-full relative">
            <img class="h-full w-full rounded-t-lg" :src="suite.imagePath" alt="">
            <p class="absolute -bottom-4 right-5 px-3 py-1 bg-black/75 text-white">{{ suite.price }}</p>
        </figure>

        <!-- información -->
        <div class="h-[60%] py-7 mx-2 md:px-5">
            <h2 class="font-bold text-lg mb-2">{{ suite.name }}</h2>
            <div class="flex items-center space-x-1 md:space-x-2 text-xs md:text-sm">
                <div class="flex items-center space-x-2 border-r border-[#DD99DD9D] pr-2">
                    <i class="fa-solid fa-bed text-primary"></i>
                    <p>{{ suite.beds }}</p>
                </div>
                <div class="flex items-center space-x-2 border-r border-[#DD99DD9D] pr-2">
                    <i class="fa-solid fa-bed text-primary"></i>
                    <p>Estancia</p>
                </div>
                <div class="flex items-center space-x-2 border-r border-[#DD99DD9D] pr-2">
                    <i class="fa-solid fa-kitchen-set text-primary"></i>
                    <p>Cocina básica</p>
                </div>
                <div class="flex items-center space-x-2">
                    <i class="fa-solid fa-car text-primary"></i>
                    <p>Estacionamiento</p>
                </div>
            </div>

            <p class="text-center text-[#5C5C5C] my-3">{{ suite.people }}</p>
            <p class="text-[#5C5C5C] h-32">{{ suite.description }}</p>

            <div class="flex justify-center mt-4 lg:my-4">
                <PrimaryButton class="!px-16 mb-auto">Ver más</PrimaryButton>
            </div>
        </div>
    </div>
</template>

<script>
import PrimaryButton from '@/Components/PrimaryButton.vue';

export default {

components:{
    PrimaryButton
},
props:{
    suite: Object
}
}
</script>
