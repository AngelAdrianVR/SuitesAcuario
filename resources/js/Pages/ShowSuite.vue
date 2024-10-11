<template>
    <Head title="Bienvenido" />

        <div v-if="showPreview" class="fixed inset-0 bg-black opacity-90 z-20"></div>

        <!-- Imagenenes -->
        <div v-if="showPreview" @click="showPreview = false"
            class="fixed inset-0 flex justify-center items-center border z-30">
            <!-- Change image -->
            <div class="absolute top-1/2 lg:top-1/2 w-4/5 lg:w-2/3 flex justify-between items-center">
                <i @click.stop="handleMinusImage"
                    class="fa-solid fa-angle-left text-white text-lg px-[19px] py-3 rounded-full bg-gray-400/60 hover:scale-105"></i>
                <i @click.stop="handlePlusImage"
                    class="fa-solid fa-angle-right text-white text-lg px-[19px] py-3 rounded-full bg-gray-400/60 hover:scale-105"></i>
            </div>
            <div>
                <img class="w-[700px] rounded-lg mx-auto" :src="suites[suite - 1].images[currentImageIndex]">
            </div>
        </div>
        
        <!-- mobile menu (hamburger) -->
        <div v-if="showMobileMenu"
            class="flex flex-col z-30 w-2/3 bg-[#262626] rounded-xl fixed top-20 right-2 border-white border py-1 text-white">
           <button class="mx-2 rounded-sm px-1 py-px hover:text-primary text-white transition-colors ease-linear duration-200" @click="$inertia.visit('/')">Inicio</button>
            <button class="mx-2 rounded-sm px-1 py-px hover:text-primary text-white transition-colors ease-linear duration-200" @click="$inertia.visit('/')">Nosotros</button>
            <button class="mx-2 rounded-sm px-1 py-px hover:text-primary text-white transition-colors ease-linear duration-200" @click="$inertia.visit('/')">Suites</button>
            <button class="mx-2 rounded-sm px-1 py-px hover:text-primary text-white transition-colors ease-linear duration-200" @click="$inertia.visit('/')">Contacto</button>
        </div>

        <!-- navbar -->
        <nav :class="['navbar', { 'fixed-navbar': isNavbarFixed }]"
            class="flex items-center justify-between py-4 lg:px-10 px-6 w-full relative">

            <!-- Logotipo -->
            <div class="flex space-x-2 items-center">
                <img src="../../../public/images/iso_logo.png" class="h-9 md:h-14" alt="logo" />
                <span class="font-bold text-primary text-base md:text-xl">Suites Acuario Mazatlán</span>
            </div>

            <!-- Hamburger button  -->
            <button @click="showMobileMenu = !showMobileMenu" class="lg:hidden">
                <i class="fa-solid fa-bars text-xl text-primary"></i>
            </button>

            <!-- info de contacto  -->
            <div class="absolute top-0 right-0 bg-white border-b-8 border-black py-2 pl-5 pr-36 lg:flex items-center space-x-5 hidden ">
                <div class="flex items-center space-x-3">
                    <i class="fa-regular fa-envelope text-sm text-primary"></i>
                    <p class="text-sm underline">mztsuitesacuario@gmail.com</p>
                </div>
                <div class="flex items-center space-x-3">
                    <i class="fa-brands fa-whatsapp text-sm text-primary"></i>
                    <p class="text-sm underline">+52 (669) 1178743</p>
                </div>
            </div>

            <!-- nav links -->
            <div class="lg:flex justify-center mr-12 hidden">        
                <button class="mx-2 rounded-sm px-1 py-px hover:text-primary text-white transition-colors ease-linear duration-200" @click="$inertia.visit('/')">Inicio</button>
                <button class="mx-2 rounded-sm px-1 py-px hover:text-primary text-white transition-colors ease-linear duration-200" @click="$inertia.visit('/')">Nosotros</button>
                <button class="mx-2 rounded-sm px-1 py-px hover:text-primary text-white transition-colors ease-linear duration-200" @click="$inertia.visit('/')">Suites</button>
                <button class="mx-2 rounded-sm px-1 py-px hover:text-primary text-white transition-colors ease-linear duration-200" @click="$inertia.visit('/')">Contacto</button>
                <a href="https://api.whatsapp.com/send?phone=526691178743&text=Hola!%20vi%20tu%20página%20,%20me%20interesa%20su%20servicio!" target="_blank" rel="noopener noreferrer">
                    <i class="fa-brands fa-whatsapp text-xl ml-2 text-primary"></i>
                </a>
            </div>
            <div class="h-16 w-32 -mr-10 bg-primary hidden lg:block"></div>
        </nav>
        
        <!-- Contenido -->
        <main @click="showMobileMenu = false" class="lg:py-10 lg:px-32 px-3 mt-24">
            <!-- migajas de pan -->
            <p class="flex items-center text-sm text-[#4A4A4A]">
                <Link href="/" class="flex items-center text-gray-400">
                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                        stroke="currentColor" class="w-4 h-4 mr-1">
                        <path stroke-linecap="round" stroke-linejoin="round"
                            d="m2.25 12 8.954-8.955c.44-.439 1.152-.439 1.591 0L21.75 12M4.5 9.75v10.125c0 .621.504 1.125 1.125 1.125H9.75v-4.875c0-.621.504-1.125 1.125-1.125h2.25c.621 0 1.125.504 1.125 1.125V21h4.125c.621 0 1.125-.504 1.125-1.125V9.75M8.25 21h8.25" />
                    </svg>
                    <span>Inicio</span>
                </Link>
                <i class="fa-solid fa-chevron-right mx-2"></i>
                <span class="text-black">
                    {{ suites[suite - 1].name }}
                </span>
            </p>

            <!-- imagenes -->
            <div class="lg:grid grid-cols-2 gap-9 mt-5 relative space-y-3 lg:space-y-0">
                <figure :class="{ 'active': image1 }" class="w-full h-[600px] flex justify-center lg:fade-in">
                    <img class="object-contain rounded-xl w-full" :src="suites[suite - 1].images[0]" alt="">
                </figure>
                <div class="grid grid-cols-2 gap-7 sm:mt-7 lg:mt-0">
                    <figure v-if="suites[suite - 1].images?.length > 1" :class="{ 'active': image2 }" class="w-full lg:fade-in">
                        <img class="object-contain rounded-xl w-full h-[286px]"
                            :src="suites[suite - 1].images[1]" alt="">
                    </figure>
                    <figure v-if="suites[suite - 1].images?.length > 2" :class="{ 'active': image3 }" class="w-full lg:fade-in-right">
                        <img class="object-contain rounded-xl w-full h-[286px]"
                            :src="suites[suite - 1].images[2]" alt="">
                    </figure>
                    <figure v-if="suites[suite - 1].images?.length > 3" :class="{ 'active': image4 }" class="w-full lg:fade-in">
                        <img class="object-contain rounded-xl w-full h-[286px]"
                            :src="suites[suite - 1].images[3]" alt="">
                    </figure>
                    <figure v-if="suites[suite - 1].images?.length > 4" :class="{ 'active': image5 }" class="w-full lg:fade-in-right ">
                        <img class="object-contain rounded-xl w-full h-[286px]"
                            :src="suites[suite - 1].images[4]" alt="">
                    </figure>
                </div>
                <button @click="showPreview = true" v-if="suites[suite - 1].images?.length > 5 || true"
                    class="absolute -bottom-5 right-20 rounded-[10px] bg-white border border-[#D9D9D9] py-2 px-3">
                    Mostrar todas las fotos
                    <i class="fa-regular fa-images ml-2 text-xs"></i>
                </button>
            </div>

            <div class="flex justify-start items-center space-x-2 lg:space-x-7 mt-20 mb-12">
                <div class="border-b-4 border-primary w-40 mt-[2px]"></div>
                <h2 class="text-lg lg:text-xl font-bold text-center text">HABITACIÓN <span class="text-primary uppercase ml-1">{{ suites[suite - 1].name }}</span> </h2>
                <div class="border-b-4 border-primary w-40 mt-[2px]"></div>
            </div>

            <p class="lg:w-1/2 text-[#5C5C5C]">{{ suites[suite - 1].description }}</p>
            <p class="lg:w-1/2 text-[#5C5C5C] mt-7">Esta suite cuenta con una cama y las siguiente amenidades :</p>

            <div class="grid grid-cols-2 lg:grid-cols-3 gap-7 my-7">
                <div v-for="amenity in suites[suite - 1].amenities" :key="amenity" class="flex items-center space-x-4">
                    <i class="fa-regular fa-circle-check text-primary"></i>
                    <p class="font-bold">{{ amenity }}</p>
                </div>
            </div>

            <div class="flex justify-end">
                <PrimaryButton class="!px-16">Enviar mensaje</PrimaryButton>
            </div>
        </main>

        <footer class="p-4 md:grid grid-cols-4 gap-3 text-white bg-[#1A1A1A] mt-24 md:relative">
                <div>
                    <figure class="flex space-x-2 items-center h-full md:h-auto space-y-2 mt-7">
                        <img src="../../../public/images/iso_logo.png" class="h-14" alt="logo" />
                        <span class="font-bold text-primary text-xl">Suites Acuario Mazatlán</span>
                    </figure>

                    <p class="col-span-full mt-4">
                        <small class="text-base">Comodidad y serenidad: tu hogar en Mazatlán te espera</small>
                    </p>

                     <p class="col-span-full mt-7">
                        <small>Copyrigth &copy; 2024 </small>
                        <small class="block md:inline mb-5"> SuitesAcuario Mazatlán. Todos los derechos reservados.</small>
                    </p>
                </div>
                <div class="flex flex-col text-center self-start">
                    <h2 class="text-xl font-bold mb-5">Reservaciones</h2>
                    <span>mztsuitesacuario@gmail.com</span>
                    <h2 class="text-xl text-[#15B91C] mt-5">WHATSAPP</h2>
                    <a href="https://api.whatsapp.com/send?phone=526691178743&text=Hola!%20vi%20tu%20página%20,%20me%20interesa%20su%20servicio!" target="_blank" rel="noopener noreferrer">
                        <p class="text-xl text-[#15B91C]"><i class="fa-brands fa-whatsapp mr-3"></i>+52 (669) 1178743</p>
                    </a>
                </div>
                <div class="flex flex-col text-center">
                    <h2 class="text-xl font-bold mb-5">Ubicación</h2>
                    <a href="https://www.google.com.mx/maps/place/Suites+Acuario+Mazatl%C3%A1n/@23.2274608,-106.430388,17z/data=!3m1!4b1!4m6!3m5!1s0x869f53ae682ea40b:0xc2ae8db4aee4b886!8m2!3d23.2274559!4d-106.4278131!16s%2Fg%2F11hzsn6mqy?entry=ttu" target="_blank" rel="noopener noreferrer">
                        <p class="text-xl text-white">Av. de los Deportes 14, Tellería, 82149 Mazatlán, Sin.</p>
                    </a>
                </div>
                <div class="flex flex-col space-y-3 mb-3 text-center">
                    <h2 class="text-xl font-bold mb-5">Síguenos</h2>
                    <div class="flex lg:flex-col justify-center space-x-4 lg:space-x-0">
                        <a href="https://www.facebook.com/suitesAcuario2021" target="_blank"><i class="fa-brands fa-facebook text-white text-4xl cursor-pointer"></i></a>
                        <i class="fa-brands fa-square-instagram text-white text-4xl cursor-pointer"></i>
                        <a href="https://api.whatsapp.com/send?phone=526691178743&text=Hola!%20vi%20tu%20página%20,%20me%20interesa%20su%20servicio!" target="_blank" rel="noopener noreferrer"><i class="fa-brands fa-whatsapp text-white text-4xl cursor-pointer"></i></a>
                    </div>
                </div>               
                <a href="https://dtw.com.mx" target="_blank"
                    class="col-span-full flex justify-end items-center space-x-2 mr-16">
                    <small>by Digtital Tech Work</small>
                    <img class="w-20" src="../../../public/images/white_logo.png">
                </a>
            </footer>

</template>

<script>
import { useForm, Link, Head } from "@inertiajs/vue3";
// import { useToast } from "vue-toastification";
import InputError from "@/Components/InputError.vue";
import PrimaryButton from "@/Components/PrimaryButton.vue";
import SuiteCard from "@/Components/MyComponents/SuiteCard.vue";
import ThirthButton from "@/Components/MyComponents/ThirthButton.vue";

// suites images
import s1 from "../../../public/images/suite1.png";
import s2 from "../../../public/images/suite2.png";
import s3 from "../../../public/images/suite3.png";

export default {
data() {
    return {
        isNavbarFixed: false,
        currentImageIndex: 0,
        showMobileMenu: false,
        showPreview: false,
        image1: false, // variables para transiciones por imagen
        image2: false, // variables para transiciones por imagen
        image3: false, // variables para transiciones por imagen
        image4: false, // variables para transiciones por imagen
        image5: false, // variables para transiciones por imagen
        suites: [
            {
                id: 1,
                images: [s1, s2, s3],
                name: 'Suite clásica',
                price: '$500/Noche',
                beds: '1 cama',
                people: 'Ideal para 2 personas',
                amenities: ['Ideal para 2 personas', 'Sala/estancia', 'Baño completo', 'Cama matrimonial', 'Cocina básica', 'Comedor o barra con bancos', 'Aire acondicionado', 'Estacionamiento'],
                description: 'La Suite Clásica es la elección perfecta para aquellos que buscan una experiencia de alojamiento cómoda y asequible. Esta habitación cuenta con todas las comodidades básicas que necesitas para tu estancia.',
            },
            {
                id: 2,
                images: [s2, s1, s3],
                name: 'Suite familiar',
                price: '$600/Noche',
                beds: '2 camas',
                people: 'Ideal para 4 personas',
                amenities: ['Ideal para 2 personas', 'Sala/estancia', 'Baño completo', 'Cama matrimonial', 'Cocina básica', 'Comedor o barra con bancos', 'Aire acondicionado', 'Estacionamiento'],
                description: 'La Suite Duo es la elección perfecta para aquellos que buscan una experiencia de alojamiento cómoda y asequible. Esta habitación cuenta con todas las comodidades básicas que necesitas para tu estancia, incluyendo una cama.',
            },
            {
                id: 3,
                images: [s3, s1, s2],
                name: 'Suite premium',
                price: '$800/Noche',
                beds: '1 cama',
                people: 'Ideal para 2 personas',
                amenities: ['Ideal para 2 personas', 'Sala/estancia', 'Baño completo', 'Cama matrimonial', 'Cocina básica', 'Comedor o barra con bancos', 'Aire acondicionado', 'Estacionamiento'],
                description: 'La Suite es la elección perfecta para aquellos que buscan una experiencia de alojamiento cómoda y lujosa. Esta habitación cuenta con todas las comodidades básicas que necesitas para tu estancia.',
            },
        ]
    }
},
components:{
PrimaryButton,
ThirthButton,
SuiteCard,
InputError,
Head,
Link
},
props:{
suite: String
},
methods:{
    handleScroll() {
        const currentScrollY = window.scrollY;

         // transiasiones en dispositivos móviles
            if (window.innerWidth <= 768) {

                // if (currentScrollY > 400) {
                // this.image2 = true;
                // }

                // if (currentScrollY > 2500) {
                // this.image3 = true;
                // }
            } else { // transisiones en computadoras y tablets
                // Ajusta los valores de offset según sea necesario
                // if (currentScrollY > 400) {
                    this.image1 = true;
                // }

                // if (currentScrollY > 1100) {
                    this.image2 = true;
                // }

                // if (currentScrollY > 1900) {
                    this.image3 = true;
                // }

                // if (currentScrollY > 2) {
                    this.image4 = true;
                // }
            }

        if (currentScrollY > this.lastScrollY && currentScrollY > window.innerHeight) {
            // Si se hace scroll hacia abajo y se ha pasado el alto de la pantalla
            this.isNavbarFixed = false;
        } else {
            // Si se hace scroll hacia arriba
            this.isNavbarFixed = true;
        }

        this.lastScrollY = currentScrollY;
    },
    handlePlusImage(){
        this.currentImageIndex === (this.suites[this.suite - 1].images.length - 1) ? this.currentImageIndex = 0 : this.currentImageIndex += 1
    },
    handleMinusImage(){
        this.currentImageIndex === 0 ? this.currentImageIndex = this.suites[this.suite - 1].images.length - 1 : this.currentImageIndex -= 1
    },
},
mounted() {
    window.addEventListener('scroll', this.handleScroll);
    // this.toast = useToast();
},
beforeDestroy() {
    window.removeEventListener('scroll', this.handleScroll);
},
}
</script>

<style>
/* Estilos para la barra de navegación */
.navbar {
    position: absolute;
    top: 0;
    background-color: #000000;
    opacity: 0.9;
}

.fixed-navbar {
    position: fixed;
    box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
    z-index: 100;
}

html {
    scroll-behavior: smooth;
}

.fade-in {
  opacity: 0;
  transform: translateY(200px);
  transition: opacity 1s ease, transform 0.7s ease;
}

.fade-in.active {
  opacity: 1;
  transform: translateY(0);
}

.fade-in-right {
  opacity: 0;
  transform: translateX(280px);
  transition: opacity 1s ease, transform 1.2s ease;
}

.fade-in-right.active {
  opacity: 1;
  transform: translateX(0);
}
</style>
