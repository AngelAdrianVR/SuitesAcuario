<template>

    <Head title="Bienvenido">
        <title>Bienvenido</title>
        <meta name="description"
            content="Somos una empresa dedicada a proporcionar comodidad y tranquilidad en espacios residenciales de calidad, a precios asequibles. Nuestra suites son acogedoras y luminosas diseñadas para hacer realidad tus sueños. Con privacidad y una guía local para descubrir los mejores lugares.">
        <meta name="keywords"
            content="Suites, Mazatlán, Playa, Hotel, Descanso, Diversión, Buen servicio, Vacaciones, Seguridad, Acogedor, Sol, Mar, Relajar, Disfrutar">
        <meta name="robots" content="index">
        <meta name="author" content="DTW">
    </Head>
    <div class="relative overflow-hidden">

        <!-- whatsapp button -->
        <a class="md:hidden z-50 w-14 h-14 lg:w-20 lg:h-20 rounded-full bg-green-600 shadow-md shadow-green-800/100 flex items-center justify-center fixed bottom-3 right-3 hover:scale-105"
            href="https://api.whatsapp.com/send?phone=6691178743&text=¡Hola!%20vi%20tu%20página,%20quiero%20más%20información%20sobre%20las%20suites"
            target="_blank" rel="noopener noreferrer">
            <i class="fa-brands fa-beat fa-whatsapp text-2xl lg:text-4xl text-gray-100"></i>
        </a>

        <!-- mobile menu (hamburger) -->
        <div v-if="showMobileMenu"
            class="flex flex-col z-30 w-2/3 bg-[#262626] rounded-xl fixed top-24 right-5 border-white border py-1 text-white">
            <button
                class="mx-2 rounded-sm px-1 py-px hover:text-primary text-white transition-colors ease-linear duration-200">Inicio</button>
            <button
                class="mx-2 rounded-sm px-1 py-px hover:text-primary text-white transition-colors ease-linear duration-200"
                @click="scrollToSection('nosotros')">Nosotros</button>
            <button
                class="mx-2 rounded-sm px-1 py-px hover:text-primary text-white transition-colors ease-linear duration-200"
                @click="scrollToSection('suites')">Suites</button>
            <button
                class="mx-2 rounded-sm px-1 py-px hover:text-primary text-white transition-colors ease-linear duration-200"
                @click="scrollToSection('ubicación')">Ubicación</button>
        </div>

        <!-- navbar -->
        <nav :class="['navbar', { 'fixed-navbar': isNavbarFixed }]"
            class="flex items-center justify-between py-4 lg:px-10 px-6 w-full relative">

            <!-- Logotipo -->
            <div class="flex space-x-2 items-center">
                <img src="../../../public/images/iso_logo.png" class="h-9 md:h-14" alt="logo suites acuario mazatlán" />
                <span class="font-bold text-primary text-base md:text-xl">Suites Acuario Mazatlán</span>
            </div>

            <!-- Hamburger button  -->
            <button @click="showMobileMenu = !showMobileMenu" class="lg:hidden">
                <i class="fa-solid fa-bars text-xl text-primary"></i>
            </button>

            <!-- info de contacto  -->
            <div class="absolute top-0 right-0 bg-white py-2 pl-5 pr-36 lg:flex items-center space-x-5 hidden ">
                <div @click="abrirClienteCorreo()" class="flex items-center space-x-3 cursor-pointer">
                    <i class="fa-regular fa-envelope text-sm text-primary"></i>
                    <p class="text-sm underline">mztsuitesacuario@gmail.com</p>
                </div>
                <div class="flex items-center space-x-3">
                    <i class="fa-brands fa-whatsapp text-sm text-primary"></i>
                    <a href="https://api.whatsapp.com/send?phone=6691178743&text=¡Hola!%20vi%20tu%20página,%20quiero%20más%20información%20sobre%20las%20suites"
                        target="_blank" class="text-sm underline">+52 (669) 1178743</a>
                </div>
            </div>

            <!-- nav links -->
            <div class="lg:flex justify-center mr-12 hidden">
                <button
                    class="mx-2 rounded-sm px-1 py-px hover:text-primary text-white transition-colors ease-linear duration-200">Inicio</button>
                <button
                    class="mx-2 rounded-sm px-1 py-px hover:text-primary text-white transition-colors ease-linear duration-200"
                    @click="scrollToSection('nosotros')">Nosotros</button>
                <button
                    class="mx-2 rounded-sm px-1 py-px hover:text-primary text-white transition-colors ease-linear duration-200"
                    @click="scrollToSection('suites')">Suites</button>
                <button
                    class="mx-2 rounded-sm px-1 py-px hover:text-primary text-white transition-colors ease-linear duration-200"
                    @click="scrollToSection('ubicación')">Ubicación</button>
                <a href="https://api.whatsapp.com/send?phone=6691178743&text=¡Hola!%20vi%20tu%20página,%20quiero%20más%20información%20sobre%20las%20suites"
                    target="_blank" rel="noopener noreferrer">
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

        <main class="pt-16 md:pt-20">
            <!-- portada -->
            <section>
                <figure class="w-full h-full relative">
                    <img class="object-contain w-full h-full" :src="frontPageTexts[currentTextIndex].img" alt="playa">
                    <!-- Texto centrado -->
                    <div class="absolute top-[40%] flex items-start justify-between w-full px-3 md:px-16">
                        <button @click.stop="handleMinusImage"
                            class="text-white text-xs lg:text-xl px-3 lg:px-[23px] py-2 lg:py-4 rounded-full bg-black/60 hover:scale-105">
                            <i class="fa-solid fa-angle-left"></i>
                        </button>
                        <h1 class="text-lg lg:text-7xl font-bold w-2/3 text-white text-center">
                            {{ frontPageTexts[currentTextIndex].text }}</h1>
                        <button @click.stop="handlePlusImage"
                            class="text-white text-xs lg:text-xl px-3 lg:px-[23px] py-2 lg:py-4 rounded-full bg-black/60 hover:scale-105">
                            <i class="fa-solid fa-angle-right"></i>
                        </button>
                    </div>
                    <div
                        class="absolute bottom-2 lg:bottom-14 left-44 lg:left-1/2 flex items-center justify-center space-x-3 text-xs">
                        <button @click="currentTextIndex = index" v-for="(dot, index) in frontPageTexts" :key="index"
                            :class="{ '!text-primary text-base scale-110': currentTextIndex === index }"
                            class="transition text-white ease-linear duration-200">
                            <i class="fa-solid fa-circle"></i>
                        </button>
                    </div>
                    <a class="absolute bottom-16 right-28 !px-14 !text-base hidden lg:block text-center py-2 bg-primary border border-transparent rounded-full font-semibold text-white tracking-widest hover:bg-primary active:bg-primary active:scale-95 disabled:active:scale-100 disabled:cursor-not-allowed disabled:opacity-50 disabled:bg-gray2 focus:outline-none focus:ring-0 transition ease-in-out duration-100"
                        href="https://api.whatsapp.com/send?phone=6691178743&text=¡Hola!%20vi%20tu%20página,%20quiero%20más%20información%20sobre%20las%20suites">
                        Enviar mensaje
                    </a>
                </figure>
            </section>

            <!-- Contenido -->
            <section :class="{ 'active': showSection1 }" class="my-10 mx-3 lg:mx-24 fade-in-right">
                <div class="lg:grid grid-cols-3 gap-x-12" id="nosotros">
                    <div>
                        <div class="flex items-center space-x-5">
                            <h2 class="text-2xl text-primary font-bold">Nosotros</h2>
                            <div class="border-b-4 border-primary w-16 mt-[2px]"></div>
                        </div>
                        <h2 class="font-bold text-lg md:text-xl mt-5">BIENVENIDOS A <span
                                class="ml-1 text-primary">SUITE
                                ACUARIO MAZATLÁN</span></h2>
                        <p class="mt-3 text-lg text-[#5c5c5c] text-justify">Somos una empresa dedicada a proporcionar
                            comodidad y tranquilidad en
                            espacios residenciales de calidad, a precios asequibles.</p>
                        <p class="mt-9 text-lg text-[#5c5c5c] text-justify">Nuestra suites son acogedoras y luminosas
                            diseñadas para hacer realidad
                            tus sueños. Con privacidad y una guía local para descubrir los mejores lugares.</p>
                    </div>

                    <figure class="col-span-2 w-full mt-10 md:mt-0">
                        <img class="object-contain mx-auto w-full md:w-3/4"
                            src="../../../public/images/content_image.png" alt="personas en mar de mazatlán">
                    </figure>
                </div>

                <!-- suites -->
                <div :class="{ 'active': showSection2 }" class="mt-20 fade-in-left" id="suites">
                    <div class="flex justify-center items-center lg:space-x-7">
                        <div class="border-b-4 border-primary w-40 mt-[2px]"></div>
                        <h2 class="text-lg lg:text-2xl font-bold text-center text">EXPLORE NUESTRAS <span
                                class="text-primary">SUITES ACUARIO MAZATLÁN</span> </h2>
                        <div class="border-b-4 border-primary w-40 mt-[2px]"></div>
                    </div>

                    <div class="md:grid md:grid-cols-2 lg:grid-cols-3 gap-4 h-[535px] mt-16 space-y-7 md:space-y-0">
                        <SuiteCard v-for="suite in suites" :key="suite" :suite="suite" />
                    </div>
                </div>

                <!-- Ubicación  -->
                <div :class="{ 'active': showSection3 }" id="ubicación"
                    class="fade-in-right border border-grayD9 rounded-xl lg:grid grid-cols-3 mt-[1290px] lg:mt-52 mb-12 py-10 px-4 relative">
                    <div class="col-span-2 lg:px-20 my-auto">
                        <h2 class="text-lg lg:text-2xl font-bold">UBICACIÓN</h2>
                        <p class="my-4 text-[#5C5C5C] leading-7 text-justify">Nuestras suites están estratégicamente
                            ubicadas en el
                            corazón de la zona turística de Mazatlán, Sinaloa, México.
                            A pocos pasos, encontrarás una vibrante selección de bares, tiendas y el renombrado acuario.
                            Además, la playa se encuentra a tan solo 3 minutos a pie.
                            Sumérgete en la belleza natural de la región y descubre los encantos de nuestros parques y
                            otros destinos que seguramente dejarán una
                            impresión duradera en tu memoria
                        </p>
                        <div class="flex items-center space-x-4 my-4">
                            <div
                                class="flex flex-col items-center text-[#5C5C5C] border-r-2 border-grayD9 space-y-2 pr-4">
                                <p>Acuario</p>
                                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" height="24"
                                    width="24" id="Fish--Streamline-Ultimate">
                                    <desc>Fish Streamline Icon: https://streamlinehq.com</desc>
                                    <path stroke="#5c5c5c" stroke-linecap="round" stroke-linejoin="round"
                                        d="M9 22.5c-1.5 0 -3 -5 -3.5 -7s-2 0 -3 0c-1.1 0 -2 -1.567 -2 -3.5s0.9 -3.5 2 -3.5c1 0 2.5 2 3 0s2 -7 3.5 -7"
                                        stroke-width="1"></path>
                                    <path stroke="#5c5c5c" stroke-linecap="round" stroke-linejoin="round"
                                        d="M5 22.5h5c3.5 0 6.25 -2.167 8 -4.5 1.5 -2 2.5 -5 4 -5s1.5 -1 1.5 -1 0 -1 -1.5 -1 -2.5 -3 -4 -5c-1.75 -2.333 -4.5 -4.5 -8 -4.5H5"
                                        stroke-width="1"></path>
                                    <path stroke="#5c5c5c" stroke-linecap="round" stroke-linejoin="round"
                                        d="M13.5 13 12 14c-1.5 1 -1.5 -2 -1.5 -2s0 -3.00002 1.5 -2.00002L13.5 11"
                                        stroke-width="1"></path>
                                    <path stroke="#5c5c5c"
                                        d="M16.75 10.499c-0.1381 0 -0.25 -0.1119 -0.25 -0.25 0 -0.138 0.1119 -0.24998 0.25 -0.24998"
                                        stroke-width="1">
                                    </path>
                                    <path stroke="#5c5c5c"
                                        d="M16.75 10.499c0.1381 0 0.25 -0.1119 0.25 -0.25 0 -0.138 -0.1119 -0.24998 -0.25 -0.24998"
                                        stroke-width="1">
                                    </path>
                                </svg>
                            </div>
                            <div
                                class="flex flex-col items-center text-[#5C5C5C] border-r-2 border-grayD9 space-y-2 pr-3">
                                <p>Playa</p>
                                <svg width="23" height="23" viewBox="0 0 14 14" fill="none"
                                    xmlns="http://www.w3.org/2000/svg">
                                    <g clip-path="url(#clip0_6634_128)">
                                        <path
                                            d="M13.5 13.4805H13C12.4696 13.4805 11.9609 13.2698 11.5858 12.8947C11.2107 12.5196 11 12.0109 11 11.4805C11 12.0109 10.7893 12.5196 10.4142 12.8947C10.0391 13.2698 9.53043 13.4805 9 13.4805C8.46957 13.4805 7.96086 13.2698 7.58579 12.8947C7.21071 12.5196 7 12.0109 7 11.4805C7 12.0109 6.78929 12.5196 6.41421 12.8947C6.03914 13.2698 5.53043 13.4805 5 13.4805C4.46957 13.4805 3.96086 13.2698 3.58579 12.8947C3.21071 12.5196 3 12.0109 3 11.4805C3 12.0109 2.78929 12.5196 2.41421 12.8947C2.03914 13.2698 1.53043 13.4805 1 13.4805H0.5"
                                            stroke="#5C5C5C" stroke-linecap="round" stroke-linejoin="round" />
                                        <path
                                            d="M9.99951 9.48104C9.4845 8.85488 8.83719 8.35057 8.10408 8.00433C7.37098 7.65809 6.57029 7.47852 5.75953 7.47852C4.94877 7.47852 4.14808 7.65809 3.41498 8.00433C2.68187 8.35057 2.03456 8.85488 1.51953 9.48104"
                                            stroke="#5C5C5C" stroke-linecap="round" stroke-linejoin="round" />
                                        <path d="M6.5 7.5307C6.56 5.2707 7.25 3.2107 8.75 2.4707" stroke="#5C5C5C"
                                            stroke-linecap="round" stroke-linejoin="round" />
                                        <path
                                            d="M5.76172 0.570101C6.40995 0.442458 7.08245 0.568361 7.64061 0.921859C8.19876 1.27536 8.60003 1.82951 8.76172 2.4701"
                                            stroke="#5C5C5C" stroke-linecap="round" stroke-linejoin="round" />
                                        <path
                                            d="M12.41 2.84026C11.9497 2.34328 11.3239 2.03145 10.65 1.96332C9.97602 1.89519 9.30041 2.07546 8.75 2.47026"
                                            stroke="#5C5C5C" stroke-linecap="round" stroke-linejoin="round" />
                                        <path
                                            d="M5.07812 3.53978C5.46997 2.96248 6.05078 2.53982 6.72062 2.34453C7.39045 2.14923 8.10742 2.19352 8.74813 2.46978C9.39079 2.62695 9.9472 3.02775 10.2999 3.58753C10.6526 4.14731 10.7739 4.82224 10.6382 5.46978"
                                            stroke="#5C5C5C" stroke-linecap="round" stroke-linejoin="round" />
                                    </g>
                                    <defs>
                                        <clipPath id="clip0_6634_128">
                                            <rect width="14" height="14" fill="white" />
                                        </clipPath>
                                    </defs>
                                </svg>
                            </div>
                            <div
                                class="flex flex-col items-center text-[#5C5C5C] border-r-2 border-grayD9 space-y-2 pr-3">
                                <p>Bares</p>
                                <svg width="23" height="23" viewBox="0 0 14 14" fill="none"
                                    xmlns="http://www.w3.org/2000/svg">
                                    <path
                                        d="M2.67857 3H11.3214M7 8.5L1.65877 1.70207C1.55591 1.57116 1.5 1.4095 1.5 1.24302C1.5 0.832661 1.83266 0.5 2.24302 0.5H11.757C12.1673 0.5 12.5 0.83266 12.5 1.24302C12.5 1.4095 12.4441 1.57116 12.3412 1.70207L7 8.5Z"
                                        stroke="#5C5C5C" stroke-linecap="round" stroke-linejoin="round" />
                                    <path d="M7 8.5V13.5" stroke="#5C5C5C" stroke-linecap="round"
                                        stroke-linejoin="round" />
                                    <path d="M4 13.5H10" stroke="#5C5C5C" stroke-linecap="round"
                                        stroke-linejoin="round" />
                                </svg>
                            </div>
                            <div
                                class="flex flex-col items-center text-[#5C5C5C] border-r-2 border-grayD9 space-y-2 pr-3">
                                <p>Tiendas</p>
                                <svg width="23" height="23" viewBox="0 0 14 14" fill="none"
                                    xmlns="http://www.w3.org/2000/svg">
                                    <g clip-path="url(#clip0_6634_141)">
                                        <path
                                            d="M1.5 8.5V13C1.5 13.1326 1.55268 13.2598 1.64645 13.3536C1.74021 13.4473 1.86739 13.5 2 13.5H12C12.1326 13.5 12.2598 13.4473 12.3536 13.3536C12.4473 13.2598 12.5 13.1326 12.5 13V8.5"
                                            stroke="#5C5C5C" stroke-linecap="round" stroke-linejoin="round" />
                                        <path d="M8 8.5V13.5" stroke="#5C5C5C" stroke-linecap="round"
                                            stroke-linejoin="round" />
                                        <path d="M1.5 10H8" stroke="#5C5C5C" stroke-linecap="round"
                                            stroke-linejoin="round" />
                                        <path d="M0.5 4L2 0.5H12L13.5 4H0.5Z" stroke="#5C5C5C" stroke-linecap="round"
                                            stroke-linejoin="round" />
                                        <path
                                            d="M4.78 4V5C4.78 5.53043 4.56929 6.03914 4.19421 6.41421C3.81914 6.78929 3.31043 7 2.78 7H2.5C1.96957 7 1.46086 6.78929 1.08579 6.41421C0.710714 6.03914 0.5 5.53043 0.5 5V4"
                                            stroke="#5C5C5C" stroke-linecap="round" stroke-linejoin="round" />
                                        <path
                                            d="M9.25 4V5C9.25 5.53043 9.03929 6.03914 8.66421 6.41421C8.28914 6.78929 7.78043 7 7.25 7H6.75C6.21957 7 5.71086 6.78929 5.33579 6.41421C4.96071 6.03914 4.75 5.53043 4.75 5V4"
                                            stroke="#5C5C5C" stroke-linecap="round" stroke-linejoin="round" />
                                        <path
                                            d="M13.5 4V5C13.5 5.53043 13.2893 6.03914 12.9142 6.41421C12.5391 6.78929 12.0304 7 11.5 7H11.25C10.7196 7 10.2109 6.78929 9.83579 6.41421C9.46071 6.03914 9.25 5.53043 9.25 5V4"
                                            stroke="#5C5C5C" stroke-linecap="round" stroke-linejoin="round" />
                                    </g>
                                    <defs>
                                        <clipPath id="clip0_6634_141">
                                            <rect width="14" height="14" fill="white" />
                                        </clipPath>
                                    </defs>
                                </svg>
                            </div>
                        </div>
                        <div class="flex justify-end">
                            <ThirthButton v-if="!showMap" @click="showMap = true" class="!rounded-md !px-14">Ver mapa
                            </ThirthButton>
                            <ThirthButton v-else @click="showMap = false" class="!rounded-md !px-14">Cerrar mapa
                            </ThirthButton>
                        </div>
                    </div>

                    <!-- images -->
                    <div class="lg:py-9 p-4 lg:px-7">
                        <figure class="rounded-lg w-full h-full flex justify-center items-center ">
                            <i class="fa-solid fa-angle-left px-2"></i>
                            <img class="mx-auto w-[400px]" src="../../../public/images/location1.png"
                                alt="muchacho nadando en un acuario con un tiburón">
                            <i class="fa-solid fa-angle-right px-2"></i>
                        </figure>
                    </div>

                    <!-- mapa -->
                    <div class="col-span-2 lg:p-7 mb-4 lg:mb-16">
                        <div v-show="showMap" ref="map" style="height: 400px;"></div>
                    </div>
                    <!-- <div class="col-span-2 lg:p-7 mb-4 lg:mb-16">
                        <iframe v-if="showMap" class="mt-5 rounded-lg" :src="getEmbedMapUrl(urlMaps)" width="600"
                            height="380" frameborder="0" style="border: 0; width: 100%;" allowfullscreen></iframe>
                    </div> -->

                    <!-- Decoraciones -->
                    <img class="hidden lg:block absolute top-0 right-2/3"
                        src="../../../public/images/decoration_location.png"
                        alt="lineas grises como decoración del sitio web">
                    <img class="hidden lg:block absolute bottom-0 right-11/10"
                        src="../../../public/images/decoration_location_b.png"
                        alt="lineas grises como decoración del sitio web">

                </div>
            </section>

            <footer :class="{ 'active': showSection4 }"
                class="fade-in p-4 md:grid grid-cols-4 gap-3 text-white bg-[#1A1A1A] mt-24 md:relative">
                <div>
                    <figure class="flex space-x-2 items-center h-full md:h-auto space-y-2 mt-7">
                        <img src="../../../public/images/iso_logo.png" class="h-14"
                            alt="logo de suites acurio mazatlán" />
                        <span class="font-bold text-primary text-xl">Suites Acuario Mazatlán</span>
                    </figure>

                    <p class="col-span-full mt-4">
                        <small class="text-base">Comodidad y serenidad: tu hogar en Mazatlán te espera</small>
                    </p>

                    <p class="col-span-full mt-7">
                        <small>Copyrigth &copy; 2024 </small>
                        <small class="block md:inline mb-5"> SuitesAcuario Mazatlán. Todos los derechos
                            reservados.</small>
                    </p>
                </div>
                <div class="flex flex-col text-center self-start">
                    <h2 class="text-xl font-bold mb-5">Reservaciones</h2>
                    <span>mztsuitesacuario@gmail.com</span>
                    <h2 class="text-xl text-[#15B91C] mt-5">WHATSAPP</h2>
                    <a href="https://api.whatsapp.com/send?phone=6691178743&text=¡Hola!%20vi%20tu%20página,%20quiero%20más%20información%20sobre%20las%20suites"
                        target="_blank" rel="noopener noreferrer">
                        <p class="text-xl text-[#15B91C]"><i class="fa-brands fa-whatsapp mr-3"></i>+52 (669) 1178743
                        </p>
                    </a>
                </div>
                <div class="flex flex-col text-center">
                    <h2 class="text-xl font-bold mb-5">Ubicación</h2>
                    <a href="https://www.google.com.mx/maps/place/Suites+Acuario+Mazatl%C3%A1n/@23.2274608,-106.430388,17z/data=!3m1!4b1!4m6!3m5!1s0x869f53ae682ea40b:0xc2ae8db4aee4b886!8m2!3d23.2274559!4d-106.4278131!16s%2Fg%2F11hzsn6mqy?entry=ttu"
                        target="_blank" rel="noopener noreferrer">
                        <p class="text-xl text-white">Av. de los Deportes 14, Tellería, 82149 Mazatlán, Sin.</p>
                    </a>
                </div>
                <div class="flex flex-col space-y-3 mb-3 text-center">
                    <h2 class="text-xl font-bold mb-5">Síguenos</h2>
                    <div class="flex lg:flex-col justify-center space-x-4 lg:space-x-0">
                        <a href="https://www.facebook.com/suitesAcuario2021" target="_blank"><i
                                class="fa-brands fa-facebook text-white text-4xl cursor-pointer"></i></a>
                        <i class="fa-brands fa-square-instagram text-white text-4xl cursor-pointer"></i>
                        <a href="https://api.whatsapp.com/send?phone=6691178743&text=¡Hola!%20vi%20tu%20página,%20quiero%20más%20información%20sobre%20las%20suites"
                            target="_blank" rel="noopener noreferrer"><i
                                class="fa-brands fa-whatsapp text-white text-4xl cursor-pointer"></i></a>
                    </div>
                </div>
                <a href="https://dtw.com.mx" target="_blank"
                    class="col-span-full flex justify-end items-center space-x-2 mr-24">
                    <small>by Digtital Tech Work</small>
                    <img class="w-6" src="../../../public/images/dtw_logo.png"
                        alt="logo de DTW (agencia de programación)">
                </a>
            </footer>
        </main>
    </div>
</template>

<script>
import { useForm, Link, Head } from "@inertiajs/vue3";
import InputError from "@/Components/InputError.vue";
import PrimaryButton from "@/Components/PrimaryButton.vue";
import SuiteCard from "@/Components/MyComponents/SuiteCard.vue";
import ThirthButton from "@/Components/MyComponents/ThirthButton.vue";

// suites images
import s1 from "../../../public/images/suite1.png";
import s2 from "../../../public/images/suite2.png";
import s3 from "../../../public/images/suite3.png";

// home images
import h1 from "../../../public/images/home_1.png";
import h2 from "../../../public/images/home_2.png";
import h3 from "../../../public/images/home_3.png";
import h4 from "../../../public/images/home_4.png";


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
            // mapa
            map: null,
            marker: null,
            coordinates: { lat: 23.2274559, lng: -106.4278131 },
            form,
            showSection1: false, // variables para transiciones por seccion
            showSection2: false, // variables para transiciones por seccion
            showSection3: false, // variables para transiciones por seccion
            showSection4: false, // variables para transiciones por seccion
            showMap: false, // variables para el mapa
            // urlMaps: 'https://www.google.com.mx/maps/place/Cl%C3%ADnica+Dental+COB+%7C+Dra.Xochitl+Samaniego+%7C+Ortodoncia+%7C+Invisalign+Mazatl%C3%A1n/@23.2273919,-106.4277923,20.89z/data=!4m14!1m7!3m6!1s0x869f53ae682ea40b:0xc2ae8db4aee4b886!2sSuites+Acuario+Mazatl%C3%A1n!8m2!3d23.2274559!4d-106.4278131!16s%2Fg%2F11hzsn6mqy!3m5!1s0x869f53708963eac9:0x4f0a55f45005e42e!8m2!3d23.2275382!4d-106.4277535!16s%2Fg%2F1th57f4q?entry=ttu', // variables para el mapa
            frontPageTexts: [
                {
                    text: 'Descrube nuestras Suites en Mazatlán',
                    img: h1
                },
                {
                    text: 'Tu hogar lejos de casa. Explora nuestras suites',
                    img: h2
                },
                {
                    text: 'Disfruta de los mejores lugares en Mazatlán desde la comodidad de nuestras Suites',
                    img: h3
                },
                {
                    text: 'Descubre la magia de Mazatlán desde el confort de nuestras Suites',
                    img: h4
                },
            ], // variable para texto de portada
            currentTextIndex: 0, // variable para texto de portada
            timer: null, // variable para texto de portada
            isNavbarFixed: false,
            lastScrollY: 0,
            showMobileMenu: false,
            showPreview: false,
            suites: [
                {
                    id: 1,
                    imagePath: s1,
                    name: 'Suite clásica',
                    price: '$500/Noche',
                    beds: '1 cama',
                    people: 'Ideal para 2 personas',
                    description: 'La Suite Clásica es la elección perfecta para aquellos que buscan una experiencia de alojamiento cómoda y asequible. Esta habitación cuenta con todas las comodidades básicas que necesitas para tu estancia.',
                },
                {
                    id: 2,
                    imagePath: s2,
                    name: 'Suite familiar',
                    price: '$600/Noche',
                    beds: '2 camas',
                    people: 'Ideal para 4 personas',
                    description: 'La Suite Duo es la elección perfecta para aquellos que buscan una experiencia de alojamiento cómoda y asequible. Esta habitación cuenta con todas las comodidades básicas que necesitas para tu estancia, incluyendo una cama.',
                },
                {
                    id: 3,
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
        ThirthButton,
        SuiteCard,
        InputError,
        Link,
        Head,
    },
    mounted() {
        // Verifica si el ancho de la pantalla es menor que cierto valor (puedes ajustar el valor según sea necesario)
        if (window.innerWidth <= 768) {
            this.showSection1 = true;
        }
        if (this.$refs.map) {
            this.initMap();
        } else {
            console.error('Map element not found.');
        }
        window.addEventListener('scroll', this.handleScroll);
        this.startTimer();
    },
    beforeUnmount() {
        clearInterval(this.timer);
    },
    beforeDestroy() {
        window.removeEventListener('scroll', this.handleScroll);
    },
    methods: {
        initMap() {
            this.map = new google.maps.Map(this.$refs.map, {
                center: this.coordinates,
                zoom: 15,
            });

            this.marker = new google.maps.Marker({
                position: this.coordinates,
                map: this.map,
                title: 'Ubicación',
            });
        },
        scrollToSection(sectionName) {
            const section = document.getElementById(sectionName);

            if (section) {
                // Usa el método scrollIntoView para realizar un scroll suave hacia la sección
                section.scrollIntoView({
                    behavior: 'smooth',
                    block: 'start',
                });
            }
        },
        abrirClienteCorreo() {
            // Reemplaza 'tucorreo@dominio.com' con tu dirección de correo electrónico
            const direccionCorreo = 'mztsuitesacuario@gmail.com';

            // Crea el enlace 'mailto' con la dirección de correo electrónico
            const enlaceCorreo = `mailto:${direccionCorreo}`;

            // Abre el cliente de correo predeterminado del usuario
            window.location.href = enlaceCorreo;
        },
        handleScroll() {
            const currentScrollY = window.scrollY;

            // transiasiones en dispositivos móviles
            if (window.innerWidth <= 768) {

                if (currentScrollY > 350) {
                    this.showSection2 = true;
                }

                if (currentScrollY > 2450) {
                    this.showSection3 = true;
                }
            } else { // transisiones en computadoras y tablets
                // Ajusta los valores de offset según sea necesario
                if (currentScrollY > 350) {
                    this.showSection1 = true;
                }

                if (currentScrollY > 1000) {
                    this.showSection2 = true;
                }

                if (currentScrollY > 1850) {
                    this.showSection3 = true;
                }

                if (currentScrollY > 2250) {
                    this.showSection4 = true;
                }
            }

            if (currentScrollY > this.lastScrollY && currentScrollY > 300) {
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
        goToContact() {
            this.showPreview = false;
            this.scrollToSection('Contacto');
            this.$refs.nameInput.focus();
        },
        handlePlusImage() {
            this.currentTextIndex === (this.frontPageTexts?.length - 1) ? this.currentTextIndex = 0 : this.currentTextIndex += 1
        },
        handleMinusImage() {
            this.currentTextIndex === 0 ? this.currentTextIndex = this.frontPageTexts?.length - 1 : this.currentTextIndex -= 1
        },
        startTimer() {
            this.timer = setInterval(() => {
                this.currentTextIndex = (this.currentTextIndex + 1) % this.frontPageTexts.length;
            }, 4000);
        },
        getEmbedMapUrl(mapsUrl) {
            // Asegurarte de que mapsUrl tenga el formato correcto
            const formattedUrl = mapsUrl.replace('https://www.google.com/maps/place/', '');

            // Agregar "/embed/v1/" y la key al inicio de la URL
            return `https://www.google.com/maps/embed/v1/place?key=AIzaSyA0s1a7phLN0iaD6-UE7m4qP-z21pH0eSc&q=${formattedUrl}`;
        },
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

.fade-in {
    opacity: 0;
    transform: translateY(250px);
    transition: opacity 1s ease, transform 1s ease;
}

.fade-in.active {
    opacity: 1;
    transform: translateY(0);
}

.fade-in-right {
    opacity: 0;
    transform: translateX(50px);
    transition: opacity 1s ease, transform 1s ease;
}

.fade-in-right.active {
    opacity: 1;
    transform: translateX(0);
}

.fade-in-left {
    opacity: 0;
    transform: translateX(-50px);
    transition: opacity 1s ease, transform 1s ease;
}

.fade-in-left.active {
    opacity: 1;
    transform: translateX(0);
}
</style>
-