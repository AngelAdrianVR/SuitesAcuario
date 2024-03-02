<template>
    <Head title="Bienvenido" />
    <div class="relative">

        <!-- <div v-if="showPreview" class="fixed inset-0 bg-black opacity-90 z-20"></div> -->

        <!-- Imagen centrada sin opacidad -->
        <!-- <div v-if="showPreview" @click="showPreview = false; currentServiceIndex = null;"
            class="fixed inset-0 flex justify-center items-center z-30">
            <div class="relative">
                <h1 class="text-[#FFD700] my-9 text-3xl text-center">{{ services[currentServiceIndex].title }}</h1>
                <img class="w-[600px] mx-auto opacity-100" :src="services[currentServiceIndex].image">
                <button @click="goToContact"
                    class="mx-auto mt-11 text-2xl rounded-full border-2 border-[#FFD700] text-black dark:text-black flex justify-between items-center py-1 px-5 bg-[#FFD700] transition-all">
                    Contáctanos
                </button>
            </div>
        </div> -->

        <!-- whatsapp button -->
        <a class="md:hidden z-50 w-14 h-14 lg:w-20 lg:h-20 rounded-full bg-green-600 shadow-md shadow-green-800/100 flex items-center justify-center fixed bottom-3 right-3 hover:scale-105"
            href="https://api.whatsapp.com/send?phone=526691178743&text=Hola!%20vi%20tu%20página%20,%20me%20interesa%20su%20servicio!"
            target="_blank" rel="noopener noreferrer">
            <i class="fa-brands fa-beat fa-whatsapp text-2xl lg:text-4xl text-gray-100"></i>
        </a>

        <!-- mobile menu (hamburger) -->
        <div v-if="showMobileMenu"
            class="flex flex-col z-30 w-2/3 bg-[#262626] rounded-xl fixed top-24 right-5 border-white border py-1 text-white">
           <button class="mx-2 rounded-sm px-1 py-px hover:text-primary text-white transition-colors ease-linear duration-200" @click="$inertia.visit('/')">Inicio</button>
            <button class="mx-2 rounded-sm px-1 py-px hover:text-primary text-white transition-colors ease-linear duration-200" @click="$inertia.visit('/')">Nosotros</button>
            <button class="mx-2 rounded-sm px-1 py-px hover:text-primary text-white transition-colors ease-linear duration-200" @click="$inertia.visit('/')">Suites</button>
            <button class="mx-2 rounded-sm px-1 py-px hover:text-primary text-white transition-colors ease-linear duration-200" @click="$inertia.visit('/')">Contacto</button>
            <a href="https://api.whatsapp.com/send?phone=526691178743&text=Hola!%20vi%20tu%20página%20,%20me%20interesa%20su%20servicio!" target="_blank" rel="noopener noreferrer">
                <i class="fa-brands fa-whatsapp text-xl ml-2 text-primary"></i>
            </a>
        </div>

        <!-- navbar -->
        <nav :class="['navbar', { 'fixed-navbar': isNavbarFixed }]"
            class="flex items-center justify-between py-4 lg:px-10 px-6 w-full relative">

            <!-- Logotipo -->
            <div class="flex space-x-2 items-center">
                <img src="../../../public/images/iso_logo.png" class="h-14" alt="logo" />
                <span class="font-bold text-primary text-xl">Suites Acuario Mazatlán</span>
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
                <!-- <button class="mx-2 rounded-[10px] px-1 py-px hover:bg-[#FFD700] hover:text-white"
                    @click="scrollToSection('Inicio')">Inicio</button>
                <button class="mx-2 rounded-[10px] px-1 py-px hover:bg-[#FFD700] hover:text-white"
                    @click="scrollToSection('Servicios')">Servicios</button>
                <button class="mx-2 rounded-[10px] px-1 py-px hover:bg-[#FFD700] hover:text-white"
                    @click="scrollToSection('Contacto')">Proyectos</button>
                <button class="mx-2 rounded-[10px] px-1 py-px hover:bg-[#FFD700] hover:text-white"
                    @click="scrollToSection('Contacto')">Contacto</button> -->
            </div>
            <div class="h-16 w-32 -mr-10 bg-primary hidden lg:block"></div>
        </nav>

        <main class="pt-24">
            <!-- portada -->
            <section>
                <figure class="w-full relative">
                    <img class="object-contain w-full" src="../../../public/images/home_1.png" alt="">
                    <!-- Texto centrado -->
                    <div class="absolute top-[40%] flex items-center justify-between w-full px-16">
                        <i @click.stop="handleMinusImage" class="fa-solid fa-angle-left text-white text-xl px-[23px] py-4 rounded-full bg-black/60 hover:scale-105"></i>
                        <h1 class="text-7xl font-bold w-1/2 text-white text-center">{{ frontPageTexts[currentTextIndex] }}</h1>
                        <i @click.stop="handlePlusImage" class="fa-solid fa-angle-right text-white text-xl px-[23px] py-4 rounded-full bg-black/60 hover:scale-105"></i>
                    </div>
                        <div class="absolute bottom-14 left-1/2 flex items-center justify-center space-x-3 text-xs">
                            <i @click="currentTextIndex = index" v-for="(dot, index) in frontPageTexts" :key="index" :class="{ '!text-primary text-base scale-110': currentTextIndex === index }" class="fa-solid fa-circle transition text-white ease-linear duration-200"></i>
                        </div>
                        <PrimaryButton class="absolute bottom-16 right-28 !px-14 !text-base">Enviar mensaje</PrimaryButton>
                </figure>
            </section>

            <!-- Contenido -->
            <section class="my-10 mx-2 lg:mx-24">
                <div class="lg:grid grid-cols-3 gap-x-12">
                    <div>
                        <div class="flex items-center space-x-5">
                            <h2 class="text-2xl text-primary font-bold">Nosotros</h2>
                            <div class="border-b-4 border-primary w-16 mt-[2px]"></div>
                        </div>
                        <p class="font-bold text-xl mt-5">BIENVENIDOS A <span class="ml-1 text-primary">SUITE ACUARIO MAZATLÁN</span></p>
                        <p class="mt-3 text-lg">Somos una empresa dedicada a proporcionar comodidad y tranquilidad en espacios residenciales de calidad, a precios asequibles.</p>
                        <p class="mt-9 text-lg">Nuestra suites son acogedoras y luminosas diseñadas para hacer realidad tus sueños. Con privacidad y una guía local para descubrir los mejores lugares.</p>
                    </div>

                    <figure class="col-span-2 w-full">
                        <img class="object-contain mx-auto w-3/4" src="../../../public/images/content_image.png" alt="">
                    </figure>
                </div>

                <!-- suites -->
                <div class="mt-20">
                    <div class="flex justify-center items-center space-x-7">
                        <div class="border-b-4 border-primary w-40 mt-[2px]"></div>
                        <h2 class="text-2xl font-bold">EXPLORE NUESTRAS <span class="text-primary">SUITES ACUARIO MAZATLÁN</span> </h2>
                        <div class="border-b-4 border-primary w-40 mt-[2px]"></div>
                    </div>

                    <div class="md:grid md:grid-cols-2 lg:grid-cols-3 gap-4 h-[535px] mt-16">
                        <SuiteCard v-for="suite in suites" :key="suite" :suite="suite" />
                    </div>
                </div>

                <!-- Ubicación  -->
                <div class="border border-grayD9 rounded-lg grid grid-cols-3 mt-52 mb-12">
                    <div class="col-span-2 lg:px-20">
                        <h2 class="text-2xl font-bold">UBICACIÓN</h2>
                        <p class="my-4">Nuestras suites están estratégicamente ubicadas en el corazón de la zona turística de Mazatlán, Sinaloa, México. 
                            A pocos pasos, encontrarás una vibrante selección de bares, tiendas y el renombrado acuario. Además, la playa se encuentra a tan solo 3 minutos a pie.
                            Sumérgete en la belleza natural de la región y descubre los encantos de nuestros parques y otros destinos que seguramente dejarán una
                            impresión duradera en tu memoria
                        </p>
                    </div>

                    <!-- images -->
                    <div class="py-9 px-7">
                        <figure class="border rounded-lg w-full h-full flex items-center">
                            <i class="fa-solid fa-angle-left"></i>
                            <img class="mx-auto" src="../../../public/images/location1.png" alt="">
                            <i class="fa-solid fa-angle-right"></i>
                        </figure>
                    </div>
                </div>
            </section>

            <!-- form -->
            <!-- <section class="lg:mx-24 md:mx-20 mx-1 mt-44 relative" id="Contacto">
                <div class="lg:grid grid-cols-5 gap-9 mb-6">
                    <div class="col-span-3 border-2 border-[#FFD700] rounded-[20px] py-10 px-5">
                        <div class="flex h-full">
                            <div @click="currentProyectIndex = currentProyectIndex == 0 ? (projects.length - 1) : currentProyectIndex - 1"
                                class="w-8 h-11/12 lg:h-full mr-2 flex justify-center items-center cursor-pointer">
                                <button>
                                    <i class="fa-solid fa-chevron-left"></i>
                                </button>
                            </div>
                            <figure class="w-1/2">
                                <img :src="projects[currentProyectIndex].image">
                            </figure>
                            <div class="w-1/2 flex flex-col ml-5 justify-start text-3xl">
                                <h1 class="text-center font-bold mb-12 lg:mb-32">PROYECTOS</h1>
                                <p class="text-center text-xl">{{ projects[currentProyectIndex].description }}</p>
                            </div>
                            <div @click="currentProyectIndex = currentProyectIndex == (projects.length - 1) ? 0 : currentProyectIndex + 1"
                                class="w-8 h-11/12 lg:h-full ml-2 flex justify-center items-center cursor-pointer">
                                <button>
                                    <i class="fa-solid fa-chevron-right"></i>
                                </button>
                            </div>
                        </div>
                    </div>
                    <form @submit.prevent="store" class="col-span-2 md:mt-12 lg:mt-0 mt-8 mx-8">
                        <h2 class="font-bold mb-3 text-xl text-[#FFD700]">CONTÁCTANOS</h2>
                        <div class="mb-5">
                            <label for="name">Nombre <span class="text-[#FFD700]">*</span></label>
                            <input v-model="form.name" type="text" id="name" required ref="nameInput"
                                class="active:ring-0 focus:ring-0 border-none outline-none bg-[#D9D9D9] block w-full text-[#808080] rounded-[10px] h-9"
                                placeholder="Escribe tu nombre" />
                            <p class="text-red-600 text-xs" v-if="form.errors?.name">{{ form.errors?.name }}</p>
                        </div>
                        <div class="mb-5">
                            <label for="phone">Teléfono <span class="text-[#FFD700]">*</span></label>
                            <input v-model="form.phone" type="text" id="phone" required
                                class="active:ring-0 focus:ring-0 border-none outline-none bg-[#D9D9D9] block w-full text-[#808080] rounded-[10px] h-9"
                                placeholder="Escribe tu teléfono" />
                            <p class="text-red-600 text-xs" v-if="form.errors?.phone">{{ form.errors?.phone }}</p>
                        </div>
                        <div class="mb-5">
                            <label for="service">Servicio</label>
                            <select v-model="form.service" id="service"
                                class="active:ring-0 focus:ring-0 border-none outline-none bg-[#D9D9D9] block w-full text-[#808080] rounded-[10px]">
                                <option v-for="(service, index) in services" :key="index" :value="service.title">{{
                                    service.title }}</option>
                            </select>
                        </div>
                        <div class="mb-5">
                            <label for="address">Dirección</label>
                            <input v-model="form.address" type="text" id="address"
                                class="active:ring-0 focus:ring-0 border-none outline-none bg-[#D9D9D9] block w-full text-[#808080] rounded-[10px] h-9"
                                placeholder="Escribe la dirección donde solicita el servicio" />
                            <p class="text-red-600 text-xs" v-if="form.errors?.address">{{ form.errors?.address }}</p>
                        </div>
                        <div class="mb-5">
                            <label for="address">Mensaje <span class="text-[#FFD700]">*</span></label>
                            <textarea v-model="form.message" rows="5" required
                                class="active:ring-0 focus:ring-0 border-none outline-none bg-[#D9D9D9] block w-full text-[#808080] rounded-[10px]"
                                placeholder="Dejános un mensaje "></textarea>
                            <p class="text-red-600 text-xs" v-if="form.errors?.message">{{ form.errors?.message }}</p>
                        </div>
                        <button type="submit"
                            class="mx-auto mt-5 rounded-full border-2 border-[#FFD700] text-black flex justify-between items-center py-1 px-5 hover:bg-[#FFD700] transition-all">
                            Enviar
                            <i class="fa-solid fa-chevron-right ml-6"></i>
                        </button>
                    </form> -->
                    <!-- <figure class="rounded-[20px] hidden lg:block">
                        <img class="rounded-[20px]" src="../../../public/assets/images/contact.png" />
                    </figure> -->
                <!-- </div>
            </section> -->

            <!-- <footer class="p-4 md:grid grid-cols-4 gap-3 text-white bg-[#1A1A1A] mt-24 md:relative">
                <figure class="h-full md:h-auto flex md:flex-col items-center space-y-2">
                    <img class="h-16 md:h-auto" src="../../../public/images/logo_light.png" />
                    <span class="font-bold text-[#FFD700] text-xl">INGENIERÍA ZAFIRO</span>
                </figure>
                <div class="flex flex-col">
                    <h2 class="text-xl text-[#FFD700] font-bold mb-5">Venta de terrenos</h2>
                    <li v-for="(lote, index) in lotes" :key="index">{{ lote.title }}</li>
                </div>
                <div class="flex flex-col">
                    <h2 class="text-xl text-[#FFD700] font-bold mb-5">Servicios</h2>
                    <li v-for="(service, index) in services" :key="index">{{ service.title }}</li>
                </div>
                <div class="flex flex-col mb-5">
                    <h2 class="text-xl text-[#FFD700] font-bold mb-5">Contacto</h2>
                    <p>
                        <i class="fa-solid fa-envelope mr-3"></i>
                        jose.rod@ingenieriazafiro.dtw.com.mx
                    </p>
                    <p>
                        <i class="fa-solid fa-phone mr-3"></i>
                        3312517732
                    </p>
                </div>
                <p class="col-span-full">
                    <small>Copyrigth &copy; 2023 </small>
                    <small class="block md:inline mb-5"> Ingeniería Zafiro. Todos los derechos reservados.</small>
                </p>
                <a href="https://dtw.com.mx" target="_blank"
                    class="col-span-full flex justify-end items-center space-x-2 mr-24">
                    <small>by Digtital Tech Work</small>
                    <img class="w-6" src="../../../public/images/dtw_logo.png">
                </a>
            </footer> -->
        </main>
    </div>
</template>

<script>
import { useForm, Link, Head } from "@inertiajs/vue3";
// import { useToast } from "vue-toastification";
import InputError from "@/Components/InputError.vue";
import PrimaryButton from "@/Components/PrimaryButton.vue";
import SuiteCard from "@/Components/MyComponents/SuiteCard.vue";

// suites images
import s1 from "../../../public/images/suite1.png";
import s2 from "../../../public/images/suite2.png";
import s3 from "../../../public/images/suite3.png";

export default {
    data() {
        const form = useForm({
            name: null,
            address: null,
            phone: null,
            service: null,
            message: null,
        });
        return {
            form,
            frontPageTexts: ['Descrube nuestras Suites en Mazatlán', 'Texto número 2 de portada', 'Texto número 3 de portada', 'Texto número 4 de portada'], // variable para texto de portada
            currentTextIndex: 0, // variable para texto de portada
            timer: null, // variable para texto de portada
            isNavbarFixed: false,
            currentTestimony: 0,
            lastScrollY: 0,
            showMobileMenu: false,
            currentProyectIndex: 0,
            currentServiceIndex: null,
            currentKirbyIndex: 0,
            showPreview: false,
            suites: [
                {
                    imagePath: s1,
                    name: 'Suite clásica',
                    price: '$500/Noche',
                    beds: '1 cama',
                    people: 'Ideal para 2 personas',
                    description: 'La Suite Clásica es la elección perfecta para aquellos que buscan una experiencia de alojamiento cómoda y asequible. Esta habitación cuenta con todas las comodidades básicas que necesitas para tu estancia.',
                },
                {
                    imagePath: s2,
                    name: 'Suite familiar',
                    price: '$600/Noche',
                    beds: '2 camas',
                    people: 'Ideal para 4 personas',
                    description: 'La Suite Duo es la elección perfecta para aquellos que buscan una experiencia de alojamiento cómoda y asequible. Esta habitación cuenta con todas las comodidades básicas que necesitas para tu estancia, incluyendo una cama.',
                },
                {
                    imagePath: s3,
                    name: 'Suite premium',
                    price: '$800/Noche',
                    beds: '1 cama',
                    people: 'Ideal para 2 personas',
                    description: 'La Suite es la elección perfecta para aquellos que buscan una experiencia de alojamiento cómoda y lujosa. Esta habitación cuenta con todas las comodidades básicas que necesitas para tu estancia.',
                },
            ]
        };
    },
    components: {
        PrimaryButton,
        SuiteCard,
        InputError,
        Link,
        Head,
    },  
    mounted() {
        window.addEventListener('scroll', this.handleScroll);
        // this.toast = useToast();
    },
    beforeDestroy() {
        window.removeEventListener('scroll', this.handleScroll);
    },
    methods: {
        handleScroll() {
            const currentScrollY = window.scrollY;

            if (currentScrollY > this.lastScrollY && currentScrollY > window.innerHeight) {
                // Si se hace scroll hacia abajo y se ha pasado el alto de la pantalla
                this.isNavbarFixed = false;
            } else {
                // Si se hace scroll hacia arriba
                this.isNavbarFixed = true;
            }

            this.lastScrollY = currentScrollY;
        },
        scrollToSection(sectionId) {
            const section = document.getElementById(sectionId);
            section.scrollIntoView({ behavior: 'smooth' });
            this.showMobileMenu = false;
        },
        // store() {
        //     this.form.post(route("messages.store"), {
        //         onSuccess: () => {
        //             this.toast.success("Mensaje enviado correctamente", {
        //                 timeout: 5000
        //             });

        //             this.form.reset();
        //             this.goToContact();
        //         },
        //         onError: () => {
        //             this.toast.error("Completar correctamente formulario", {
        //                 timeout: 5000
        //             });

        //             this.goToContact();
        //         }
        //     });
        // },
        goToContact() {
            this.showPreview = false;
            this.scrollToSection('Contacto');
            this.$refs.nameInput.focus();
        },
        handlePlusImage(){
            this.currentTextIndex === (this.frontPageTexts?.length - 1) ? this.currentTextIndex = 0 : this.currentTextIndex += 1
        },
        handleMinusImage(){
            this.currentTextIndex === 0 ? this.currentTextIndex = this.frontPageTexts?.length - 1 : this.currentTextIndex -= 1
        },
        startTimer() {
            this.timer = setInterval(() => {
                this.currentTextIndex = (this.currentTextIndex + 1) % this.frontPageTexts.length;
            }, 4000);
            }
    },
    mounted() {
        this.startTimer();
    },
    beforeUnmount() {
        clearInterval(this.timer);
    },
};
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
</style>
