<template>
    <Head title="Bienvenido" />
    <div class="relative">

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
                <figure class="w-full relative">
                    <img class="object-contain w-full" :src="frontPageTexts[currentTextIndex].img" alt="">
                    <!-- Texto centrado -->
                    <div class="absolute top-[40%] flex items-center justify-between w-full px-3 md:px-16">
                        <i @click.stop="handleMinusImage" class="fa-solid fa-angle-left text-white text-xs lg:text-xl px-3 lg:px-[23px] py-2 lg:py-4 rounded-full bg-black/60 hover:scale-105"></i>
                        <h1 class="text-lg lg:text-7xl font-bold w-2/3 text-white text-center">{{ frontPageTexts[currentTextIndex].text }}</h1>
                        <i @click.stop="handlePlusImage" class="fa-solid fa-angle-right text-white text-xs lg:text-xl px-3 lg:px-[23px] py-2 lg:py-4 rounded-full bg-black/60 hover:scale-105"></i>
                    </div>
                        <div class="absolute bottom-2 lg:bottom-14 left-44 lg:left-1/2 flex items-center justify-center space-x-3 text-xs">
                            <i @click="currentTextIndex = index" v-for="(dot, index) in frontPageTexts" :key="index" :class="{ '!text-primary text-base scale-110': currentTextIndex === index }" class="fa-solid fa-circle transition text-white ease-linear duration-200"></i>
                        </div>
                        <PrimaryButton class="absolute bottom-16 right-28 !px-14 !text-base hidden lg:block">Enviar mensaje</PrimaryButton>
                </figure>
            </section>

            <!-- Contenido -->
            <section :class="{ 'active': showSection1 }" class="my-10 mx-3 lg:mx-24 fade-in">
                <div class="lg:grid grid-cols-3 gap-x-12">
                    <div>
                        <div class="flex items-center space-x-5">
                            <h2 class="text-2xl text-primary font-bold">Nosotros</h2>
                            <div class="border-b-4 border-primary w-16 mt-[2px]"></div>
                        </div>
                        <p class="font-bold text-lg md:text-xl mt-5">BIENVENIDOS A <span class="ml-1 text-primary">SUITE ACUARIO MAZATLÁN</span></p>
                        <p class="mt-3 text-lg">Somos una empresa dedicada a proporcionar comodidad y tranquilidad en espacios residenciales de calidad, a precios asequibles.</p>
                        <p class="mt-9 text-lg">Nuestra suites son acogedoras y luminosas diseñadas para hacer realidad tus sueños. Con privacidad y una guía local para descubrir los mejores lugares.</p>
                    </div>

                    <figure class="col-span-2 w-full mt-10 md:mt-0">
                        <img class="object-contain mx-auto w-full md:w-3/4" src="../../../public/images/content_image.png" alt="">
                    </figure>
                </div>

                <!-- suites -->
                <div :class="{ 'active': showSection2 }" class="mt-20 fade-in-right">
                    <div class="flex justify-center items-center lg:space-x-7">
                        <div class="border-b-4 border-primary w-40 mt-[2px]"></div>
                        <h2 class="text-lg lg:text-2xl font-bold text-center text">EXPLORE NUESTRAS <span class="text-primary">SUITES ACUARIO MAZATLÁN</span> </h2>
                        <div class="border-b-4 border-primary w-40 mt-[2px]"></div>
                    </div>

                    <div class="md:grid md:grid-cols-2 lg:grid-cols-3 gap-4 h-[535px] mt-16 space-y-7 md:space-y-0">
                        <SuiteCard v-for="suite in suites" :key="suite" :suite="suite" />
                    </div>
                </div>

                <!-- Ubicación  -->
                <div :class="{ 'active': showSection3 }" class="fade-in border border-grayD9 rounded-xl lg:grid grid-cols-3 mt-[1290px] lg:mt-52 mb-12 py-10 px-4 relative">
                    <div class="col-span-2 lg:px-20 my-auto">
                        <h2 class="text-lg lg:text-2xl font-bold">UBICACIÓN</h2>
                        <p class="my-4 text-[#5C5C5C] leading-7">Nuestras suites están estratégicamente ubicadas en el corazón de la zona turística de Mazatlán, Sinaloa, México. 
                            A pocos pasos, encontrarás una vibrante selección de bares, tiendas y el renombrado acuario. Además, la playa se encuentra a tan solo 3 minutos a pie.
                            Sumérgete en la belleza natural de la región y descubre los encantos de nuestros parques y otros destinos que seguramente dejarán una
                            impresión duradera en tu memoria
                        </p>
                        <div class="flex items-center space-x-4 my-4">
                            <div class="flex flex-col items-center text-[#5C5C5C] border-r-2 border-grayD9 space-y-2 pr-4">
                                <p>Acuario</p>
                                <svg width="23" height="23" viewBox="0 0 13 20" fill="none" xmlns="http://www.w3.org/2000/svg">
                                <path fill-rule="evenodd" clip-rule="evenodd" d="M12.6311 18.0442C12.0888 17.5735 11.6544 16.9914 11.3574 16.3376C10.99 15.3065 10.8068 14.2188 10.8163 13.1242C10.758 12.0753 10.6914 11.0263 10.6581 9.97742C10.6581 9.28646 10.6165 8.5955 10.6581 7.89622C10.7147 6.81936 10.6924 5.7398 10.5915 4.66619C10.5144 3.91422 10.3059 3.18162 9.97551 2.50174C9.85438 2.26565 9.71813 2.03763 9.5676 1.8191C9.40751 1.59935 9.22627 1.39581 9.02648 1.21139C8.41039 0.632072 7.64234 0.23976 6.81185 0.0801713C5.98135 -0.0794172 5.12261 0.000289258 4.33567 0.310003C3.54874 0.619717 2.86602 1.14668 2.36707 1.8295C1.86812 2.51232 1.57349 3.32287 1.5175 4.1667C1.46372 4.18691 1.41323 4.21496 1.36766 4.24995C1.24174 4.38722 1.12757 4.53481 1.02634 4.69116C0.806341 5.00422 0.608824 5.33249 0.435277 5.67349C0.256053 6.01828 0.113742 6.38104 0.0107113 6.75572C-0.00766679 6.81423 -0.00224293 6.87763 0.0258068 6.93217C0.0538566 6.98671 0.102272 7.028 0.160558 7.04709C0.204113 7.06186 0.251066 7.06342 0.295506 7.05157C0.339947 7.03972 0.379888 7.01499 0.410302 6.98049C0.398244 7.02407 0.398244 7.0701 0.410302 7.11368C0.439381 7.17738 0.49237 7.22707 0.557804 7.252C0.623238 7.27693 0.695855 7.27509 0.759944 7.24688C0.92929 7.17945 1.105 7.12924 1.28441 7.09704C1.52583 7.03876 1.77557 6.99714 2.02532 6.95551C1.29169 7.94865 0.770292 9.08214 0.49355 10.2854C0.373954 10.7857 0.298739 11.2954 0.26878 11.8089C0.238715 12.6032 0.342849 13.3968 0.576799 14.1565C0.824129 15.0536 1.31717 15.8638 2.00034 16.4957C2.16029 16.6292 2.3332 16.7464 2.51648 16.8454L1.63405 17.4864C1.18451 17.7778 0.876492 17.836 0.801569 18.1357C0.77927 18.1885 0.768325 18.2453 0.769444 18.3026C0.770563 18.3598 0.783722 18.4162 0.808065 18.468C0.832408 18.5198 0.867389 18.566 0.910733 18.6034C0.954077 18.6408 1.00481 18.6687 1.05964 18.6852C1.39417 18.7862 1.74253 18.834 2.09191 18.8267C2.5581 18.8267 3.11587 18.8267 3.54043 18.7684C3.19911 19.1514 3.03262 19.1514 3.03262 19.4261C3.01541 19.5242 3.03707 19.6251 3.09302 19.7074C3.14897 19.7898 3.2348 19.8471 3.33231 19.8673C3.50445 19.9279 3.68339 19.967 3.8651 19.9838C4.14217 20.0054 4.4205 20.0054 4.69758 19.9838C5.26187 19.9452 5.8202 19.8447 6.36254 19.6841C7.10623 19.4703 7.8238 19.1743 8.50202 18.8017L8.95988 18.8933C9.34986 18.9333 9.74167 18.9527 10.1337 18.9516C10.5151 18.9621 10.8966 18.9398 11.2742 18.885C11.5565 18.8434 11.8248 18.7349 12.0567 18.5686C12.0941 18.5436 12.1234 18.5082 12.1411 18.4669C12.1589 18.4255 12.1642 18.3799 12.1566 18.3355C12.2149 18.3855 12.2565 18.4354 12.3148 18.4771C12.3382 18.5023 12.3665 18.5224 12.398 18.5361C12.4295 18.5499 12.4635 18.557 12.4979 18.557C12.5323 18.557 12.5663 18.5499 12.5978 18.5361C12.6294 18.5224 12.6577 18.5023 12.6811 18.4771C12.713 18.4486 12.7376 18.4129 12.7528 18.373C12.768 18.3331 12.7734 18.2901 12.7685 18.2476C12.7636 18.2052 12.7485 18.1646 12.7246 18.1291C12.7007 18.0937 12.6687 18.0646 12.6311 18.0442ZM1.15121 6.53095C0.951753 6.59492 0.75703 6.67281 0.568474 6.76404L0.535175 6.81399C0.658995 6.5216 0.812416 6.24266 0.993039 5.98151C1.19627 5.68724 1.4217 5.40894 1.66735 5.14903C1.93374 4.84934 1.85049 4.58294 2.33333 5.22395C2.45741 5.39185 2.57138 5.56698 2.67465 5.74842L2.81617 5.91491L2.49983 6.06476C2.01699 6.2812 1.57578 6.3811 1.15121 6.53095ZM11.7404 18.0858C11.563 18.1783 11.366 18.2268 11.166 18.2273C10.8222 18.2283 10.4791 18.1948 10.142 18.1274C9.71145 18.0874 9.28344 18.0235 8.85999 17.9359C8.44953 17.8728 8.04743 17.7639 7.66121 17.6113C7.1386 17.3969 6.66962 17.07 6.28762 16.6539C6.1794 16.4042 5.66326 16.529 5.77148 16.8537C6.26485 17.5296 6.91281 18.0777 7.66121 18.4521C7.31157 18.5686 6.9203 18.6768 6.51239 18.7684C5.90761 18.9216 5.28789 19.0082 4.66428 19.0265H4.23972C4.57444 18.5849 4.854 18.104 5.0722 17.5946C5.09098 17.5372 5.08672 17.4747 5.06032 17.4203C5.03391 17.366 4.98743 17.324 4.93067 17.3033C4.90229 17.2928 4.87209 17.2882 4.84188 17.2897C4.81168 17.2912 4.78209 17.2988 4.75488 17.312C4.72768 17.3252 4.70342 17.3438 4.68356 17.3666C4.6637 17.3894 4.64865 17.416 4.63931 17.4448C4.56438 17.6113 4.50611 17.6362 4.05657 18.1441L2.25841 17.9359L3.03262 17.0702C3.52084 17.2403 4.03123 17.3384 4.54773 17.3615C4.61141 17.358 4.67172 17.3318 4.71772 17.2877C4.76371 17.2435 4.79233 17.1843 4.79837 17.1208C4.80442 17.0573 4.78749 16.9938 4.75067 16.9417C4.71384 16.8896 4.65956 16.8525 4.59768 16.8371C3.8058 16.7738 3.05412 16.462 2.44988 15.9463C1.90593 15.3732 1.53634 14.6571 1.38431 13.8818C1.19918 13.2157 1.12051 12.5245 1.15121 11.8339C1.15763 11.3655 1.19657 10.8982 1.26776 10.4353C1.43519 9.25495 1.84321 8.12157 2.46653 7.10536C2.49493 7.06676 2.51025 7.02009 2.51025 6.97216C2.51025 6.92424 2.49493 6.87757 2.46653 6.83897L2.66633 6.79734C3.97332 6.42273 3.6653 5.89826 3.39891 5.3405C3.18737 4.93107 2.9056 4.56195 2.56643 4.24995C2.4043 4.11104 2.20418 4.02403 1.99202 4.00021C2.09713 3.32537 2.37891 2.69035 2.80877 2.15962C3.23862 1.62888 3.80124 1.22132 4.43951 0.978298C5.11692 0.712309 5.85713 0.64939 6.56971 0.797228C7.2823 0.945067 7.93639 1.29726 8.45207 1.81078C8.60388 1.96369 8.74049 2.13097 8.85999 2.31027C8.98555 2.49001 9.09688 2.67928 9.19298 2.87636C9.46052 3.47804 9.62919 4.11897 9.69247 4.77441C9.78358 5.80959 9.80861 6.84953 9.76739 7.88789C9.76739 8.60383 9.76739 9.31143 9.84231 10.019C9.91724 11.068 10.0171 12.1252 10.1087 13.1741C10.1437 14.3417 10.3832 15.4941 10.8163 16.579C11.0786 17.1293 11.4334 17.6305 11.8652 18.0608C11.8223 18.0595 11.7796 18.0681 11.7404 18.0858Z" fill="#5C5C5C"/>
                                <path fill-rule="evenodd" clip-rule="evenodd" d="M4.38183 7.32224C4.59471 7.80712 4.75923 8.31183 4.873 8.82903C5.03117 9.32852 5.77207 8.82903 5.48071 8.41279C5.31738 7.7807 5.03172 7.18676 4.6399 6.66458C4.45885 6.42418 4.20926 6.24424 3.92397 6.14844C3.57432 6.26498 3.60762 6.42316 3.74915 6.59798C4.14041 6.81442 4.16539 6.96427 4.38183 7.32224Z" fill="#5C5C5C"/>
                                <path fill-rule="evenodd" clip-rule="evenodd" d="M6.13813 13.897C5.96331 13.6723 5.48047 13.6723 5.48047 14.255C5.48047 14.8378 5.48047 14.946 5.54707 15.6453C5.55735 15.8517 5.57959 16.0574 5.61367 16.2613C5.63612 16.3192 5.67556 16.369 5.72681 16.4041C5.77807 16.4392 5.83874 16.458 5.90087 16.458C5.963 16.458 6.02367 16.4392 6.07493 16.4041C6.12619 16.369 6.16563 16.3192 6.18808 16.2613C6.18808 15.9783 6.13813 15.8367 6.1298 15.562C6.10483 14.8544 6.14645 14.6463 6.13813 13.897Z" fill="#5C5C5C"/>
                                <path fill-rule="evenodd" clip-rule="evenodd" d="M5.72141 12.6912L5.19695 12.6246C4.94721 12.6246 4.54762 12.6246 4.18965 12.558H4.05645L4.13138 12.4498C4.24792 12.2167 4.38112 11.9836 4.51432 11.7588C4.64751 11.5341 4.80569 11.3176 4.97218 11.1012L5.71309 10.1438C5.79072 10.0074 5.82553 9.85075 5.81299 9.69428C5.79269 9.49405 5.75367 9.29616 5.69644 9.10321C5.45502 8.92007 5.22193 8.97834 5.01381 9.37793C5.147 9.65265 5.16365 9.5361 4.28122 10.5684C4.09526 10.7967 3.92291 11.0357 3.76508 11.2843C3.60779 11.5378 3.46331 11.7989 3.33219 12.0668C3.33219 12.1334 3.14072 12.4581 3.0991 12.5996C3.06756 12.6852 3.06179 12.7781 3.08251 12.8668C3.10322 12.9556 3.14951 13.0364 3.21565 13.0991C3.40793 13.2653 3.6458 13.3697 3.89828 13.3988C4.30586 13.4224 4.71445 13.4224 5.12203 13.3988H5.36345V13.5487C5.62152 13.84 5.86294 13.7818 6.07938 13.3738V13.0741C6.06609 12.9813 6.02464 12.8949 5.96062 12.8264C5.89661 12.7579 5.81311 12.7107 5.72141 12.6912Z" fill="#5C5C5C"/>
                                <path fill-rule="evenodd" clip-rule="evenodd" d="M5.14503 2.83481C4.98986 2.95016 4.86899 3.10556 4.79539 3.28435C4.72033 3.46003 4.69238 3.65225 4.71427 3.84203C4.73617 4.03181 4.80717 4.21261 4.92026 4.36658C5.04943 4.5324 5.22723 4.65366 5.42876 4.71338C5.6303 4.77309 5.84546 4.76826 6.04411 4.69957C6.31793 4.63249 6.55784 4.46774 6.71879 4.23628C6.87974 4.00483 6.95065 3.72257 6.91822 3.44253C6.88653 3.2531 6.80425 3.07576 6.68006 2.92927C6.55587 2.78277 6.39439 2.67256 6.21271 2.61029C6.03103 2.54803 5.8359 2.53602 5.64796 2.57554C5.46001 2.61506 5.28625 2.70465 5.14503 2.83481ZM5.79437 3.85044C5.75066 3.86993 5.70142 3.87308 5.65559 3.85933C5.60976 3.84558 5.57038 3.81584 5.54462 3.77552C5.48393 3.69415 5.4544 3.59374 5.46137 3.49247C5.59457 2.80151 6.19396 3.16781 6.19396 3.49247C6.19396 3.67562 6.03579 3.80049 5.79437 3.85044Z" fill="#5C5C5C"/>
                                </svg>
                            </div>
                            <div class="flex flex-col items-center text-[#5C5C5C] border-r-2 border-grayD9 space-y-2 pr-3">
                                <p>Playa</p>
                                <svg width="23" height="23" viewBox="0 0 14 14" fill="none" xmlns="http://www.w3.org/2000/svg">
                                    <g clip-path="url(#clip0_6634_128)">
                                    <path d="M13.5 13.4805H13C12.4696 13.4805 11.9609 13.2698 11.5858 12.8947C11.2107 12.5196 11 12.0109 11 11.4805C11 12.0109 10.7893 12.5196 10.4142 12.8947C10.0391 13.2698 9.53043 13.4805 9 13.4805C8.46957 13.4805 7.96086 13.2698 7.58579 12.8947C7.21071 12.5196 7 12.0109 7 11.4805C7 12.0109 6.78929 12.5196 6.41421 12.8947C6.03914 13.2698 5.53043 13.4805 5 13.4805C4.46957 13.4805 3.96086 13.2698 3.58579 12.8947C3.21071 12.5196 3 12.0109 3 11.4805C3 12.0109 2.78929 12.5196 2.41421 12.8947C2.03914 13.2698 1.53043 13.4805 1 13.4805H0.5" stroke="#5C5C5C" stroke-linecap="round" stroke-linejoin="round"/>
                                    <path d="M9.99951 9.48104C9.4845 8.85488 8.83719 8.35057 8.10408 8.00433C7.37098 7.65809 6.57029 7.47852 5.75953 7.47852C4.94877 7.47852 4.14808 7.65809 3.41498 8.00433C2.68187 8.35057 2.03456 8.85488 1.51953 9.48104" stroke="#5C5C5C" stroke-linecap="round" stroke-linejoin="round"/>
                                    <path d="M6.5 7.5307C6.56 5.2707 7.25 3.2107 8.75 2.4707" stroke="#5C5C5C" stroke-linecap="round" stroke-linejoin="round"/>
                                    <path d="M5.76172 0.570101C6.40995 0.442458 7.08245 0.568361 7.64061 0.921859C8.19876 1.27536 8.60003 1.82951 8.76172 2.4701" stroke="#5C5C5C" stroke-linecap="round" stroke-linejoin="round"/>
                                    <path d="M12.41 2.84026C11.9497 2.34328 11.3239 2.03145 10.65 1.96332C9.97602 1.89519 9.30041 2.07546 8.75 2.47026" stroke="#5C5C5C" stroke-linecap="round" stroke-linejoin="round"/>
                                    <path d="M5.07812 3.53978C5.46997 2.96248 6.05078 2.53982 6.72062 2.34453C7.39045 2.14923 8.10742 2.19352 8.74813 2.46978C9.39079 2.62695 9.9472 3.02775 10.2999 3.58753C10.6526 4.14731 10.7739 4.82224 10.6382 5.46978" stroke="#5C5C5C" stroke-linecap="round" stroke-linejoin="round"/>
                                    </g>
                                    <defs>
                                    <clipPath id="clip0_6634_128">
                                    <rect width="14" height="14" fill="white"/>
                                    </clipPath>
                                    </defs>
                                </svg>
                            </div>
                            <div class="flex flex-col items-center text-[#5C5C5C] border-r-2 border-grayD9 space-y-2 pr-3">
                                <p>Bares</p>
                                <svg width="23" height="23" viewBox="0 0 14 14" fill="none" xmlns="http://www.w3.org/2000/svg">
                                    <path d="M2.67857 3H11.3214M7 8.5L1.65877 1.70207C1.55591 1.57116 1.5 1.4095 1.5 1.24302C1.5 0.832661 1.83266 0.5 2.24302 0.5H11.757C12.1673 0.5 12.5 0.83266 12.5 1.24302C12.5 1.4095 12.4441 1.57116 12.3412 1.70207L7 8.5Z" stroke="#5C5C5C" stroke-linecap="round" stroke-linejoin="round"/>
                                    <path d="M7 8.5V13.5" stroke="#5C5C5C" stroke-linecap="round" stroke-linejoin="round"/>
                                    <path d="M4 13.5H10" stroke="#5C5C5C" stroke-linecap="round" stroke-linejoin="round"/>
                                </svg>
                            </div>
                            <div class="flex flex-col items-center text-[#5C5C5C] border-r-2 border-grayD9 space-y-2 pr-3">
                                <p>Tiendas</p>
                                <svg width="23" height="23" viewBox="0 0 14 14" fill="none" xmlns="http://www.w3.org/2000/svg">
                                    <g clip-path="url(#clip0_6634_141)">
                                    <path d="M1.5 8.5V13C1.5 13.1326 1.55268 13.2598 1.64645 13.3536C1.74021 13.4473 1.86739 13.5 2 13.5H12C12.1326 13.5 12.2598 13.4473 12.3536 13.3536C12.4473 13.2598 12.5 13.1326 12.5 13V8.5" stroke="#5C5C5C" stroke-linecap="round" stroke-linejoin="round"/>
                                    <path d="M8 8.5V13.5" stroke="#5C5C5C" stroke-linecap="round" stroke-linejoin="round"/>
                                    <path d="M1.5 10H8" stroke="#5C5C5C" stroke-linecap="round" stroke-linejoin="round"/>
                                    <path d="M0.5 4L2 0.5H12L13.5 4H0.5Z" stroke="#5C5C5C" stroke-linecap="round" stroke-linejoin="round"/>
                                    <path d="M4.78 4V5C4.78 5.53043 4.56929 6.03914 4.19421 6.41421C3.81914 6.78929 3.31043 7 2.78 7H2.5C1.96957 7 1.46086 6.78929 1.08579 6.41421C0.710714 6.03914 0.5 5.53043 0.5 5V4" stroke="#5C5C5C" stroke-linecap="round" stroke-linejoin="round"/>
                                    <path d="M9.25 4V5C9.25 5.53043 9.03929 6.03914 8.66421 6.41421C8.28914 6.78929 7.78043 7 7.25 7H6.75C6.21957 7 5.71086 6.78929 5.33579 6.41421C4.96071 6.03914 4.75 5.53043 4.75 5V4" stroke="#5C5C5C" stroke-linecap="round" stroke-linejoin="round"/>
                                    <path d="M13.5 4V5C13.5 5.53043 13.2893 6.03914 12.9142 6.41421C12.5391 6.78929 12.0304 7 11.5 7H11.25C10.7196 7 10.2109 6.78929 9.83579 6.41421C9.46071 6.03914 9.25 5.53043 9.25 5V4" stroke="#5C5C5C" stroke-linecap="round" stroke-linejoin="round"/>
                                    </g>
                                    <defs>
                                    <clipPath id="clip0_6634_141">
                                    <rect width="14" height="14" fill="white"/>
                                    </clipPath>
                                    </defs>
                                </svg>
                            </div>
                        </div>
                        <div class="flex justify-end">
                            <ThirthButton v-if="!showMap" @click="showMap = true" class="!rounded-md !px-14">Ver mapa</ThirthButton>
                            <ThirthButton v-else @click="showMap = false" class="!rounded-md !px-14">Cerrar mapa</ThirthButton>
                        </div>
                    </div>

                    <!-- images -->
                    <div class="lg:py-9 p-4 lg:px-7">
                        <figure class="rounded-lg w-full h-full flex justify-center items-center ">
                            <i class="fa-solid fa-angle-left px-2"></i>
                            <img class="mx-auto w-[400px]" src="../../../public/images/location1.png" alt="">
                            <i class="fa-solid fa-angle-right px-2"></i>
                        </figure>
                    </div>

                    <!-- mapa -->
                    <div class="col-span-2 lg:p-7 mb-4 lg:mb-16">
                        <iframe
                        v-if="showMap"
                            class="mt-5 rounded-lg"
                            :src="getEmbedMapUrl(urlMaps)"
                            width="600"
                            height="380"
                            frameborder="0"
                            style="border: 0; width: 100%;"
                            allowfullscreen
                        ></iframe>
                    </div>

                    <!-- Decoraciones -->
                    <img class="hidden lg:block absolute top-0 right-2/3" src="../../../public/images/decoration_location.png" alt="">
                    <img class="hidden lg:block absolute bottom-0 right-11/10" src="../../../public/images/decoration_location_b.png" alt="">

                </div>
            </section>

            <footer :class="{ 'active': showSection4 }" class="fade-in p-4 md:grid grid-cols-4 gap-3 text-white bg-[#1A1A1A] mt-24 md:relative">
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
                    class="col-span-full flex justify-end items-center space-x-2 mr-24">
                    <small>by Digtital Tech Work</small>
                    <img class="w-6" src="../../../public/images/dtw_logo.png">
                </a>
            </footer>
        </main>
    </div>
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
            form,
            showSection1: false, // variables para transiciones por seccion
            showSection2: false, // variables para transiciones por seccion
            showSection3: false, // variables para transiciones por seccion
            showSection4: false, // variables para transiciones por seccion
            showMap: false, // variables para el mapa
            urlMaps: 'https://www.google.com.mx/maps/place/Cl%C3%ADnica+Dental+COB+%7C+Dra.Xochitl+Samaniego+%7C+Ortodoncia+%7C+Invisalign+Mazatl%C3%A1n/@23.2273919,-106.4277923,20.89z/data=!4m14!1m7!3m6!1s0x869f53ae682ea40b:0xc2ae8db4aee4b886!2sSuites+Acuario+Mazatl%C3%A1n!8m2!3d23.2274559!4d-106.4278131!16s%2Fg%2F11hzsn6mqy!3m5!1s0x869f53708963eac9:0x4f0a55f45005e42e!8m2!3d23.2275382!4d-106.4277535!16s%2Fg%2F1th57f4q?entry=ttu', // variables para el mapa
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

        window.addEventListener('scroll', this.handleScroll);
        this.startTimer();
        // this.toast = useToast();
    },
    beforeUnmount() {
        clearInterval(this.timer);
    },
    beforeDestroy() {
        window.removeEventListener('scroll', this.handleScroll);
    },
    methods: {
        handleScroll() {
            const currentScrollY = window.scrollY;

            // transiasiones en dispositivos móviles
            if (window.innerWidth <= 768) {

                if (currentScrollY > 400) {
                this.showSection2 = true;
                }

                if (currentScrollY > 2500) {
                this.showSection3 = true;
                }
            } else { // transisiones en computadoras y tablets
                // Ajusta los valores de offset según sea necesario
                if (currentScrollY > 400) {
                    this.showSection1 = true;
                }

                if (currentScrollY > 1100) {
                    this.showSection2 = true;
                }

                if (currentScrollY > 1900) {
                    this.showSection3 = true;
                }

                if (currentScrollY > 2300) {
                    this.showSection4 = true;
                }
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
  transform: translateX(350px);
  transition: opacity 1s ease, transform 1s ease;
}

.fade-in-right.active {
  opacity: 1;
  transform: translateX(0);
}
</style>
