<template>
    <header class="container">
        <!-- Navbar -->
        <nav
            class="flex justify-between md:justify-around py-4 bg-white/80 backdrop-blur-md shadow-md w-full px-10 fixed top-0 left-0 right-0 z-10 md:px-3">
            <!-- Logo Container -->
            <div class="flex items-center">
                <!-- Logo -->
                <a class="cursor-pointer">
                    <h3 class="text-3xl text-blue-500 pl-10 font-bold">
                        EventPro
                    </h3>
                </a>
            </div>

            <!-- Links Section -->
            <div class="items-center md:space-x-8 justify-center justify-items-start md:justify-items-center md:flex md:pt-2 w-full left-0 top-16 px-5 md:px-10 py-3 md:py-0 border-t md:border-t-0">

                <NuxtLink to="/"
                    class="flex text-gray-600 hover:text-blue-500 cursor-pointer transition-colors duration-300">
                    Home
                </NuxtLink>

                <NuxtLink to="#service"
                    class="flex text-gray-600 hover:text-blue-500 cursor-pointer transition-colors duration-300">
                    Services
                </NuxtLink>

                <NuxtLink to="#about"
                    class="flex text-gray-600 hover:text-blue-500 cursor-pointer transition-colors duration-300">
                    About Us
                </NuxtLink>
            </div>

            <!-- Auth Links -->
            <div class="flex items-center space-x-5 md:flex">

                <!-- Login -->
                <NuxtLink to="login">
                    <a
                        class="flex text-gray-600 hover:text-blue-500 cursor-pointer transition-colors duration-300 font-semibold pr-10">
                        
                        <svg
                            class="fill-current h-5 w-5 mr-2 mt-0.5"
                            xmlns="http://www.w3.org/2000/svg"
                            xmlns:xlink="http://www.w3.org/1999/xlink"
                            version="1.1"
                            width="24"
                            height="24"
                            viewBox="0 0 24 24">
                            <path
                                d="M10,17V14H3V10H10V7L15,12L10,17M10,2H19A2,2 0 0,1 21,4V20A2,2 0 0,1 19,22H10A2,2 0 0,1 8,20V18H10V20H19V4H10V6H8V4A2,2 0 0,1 10,2Z" />
                        </svg>

                        Login
                    </a>
                </NuxtLink>
            </div>

            <!-- Hamberger Menu -->
            <button
                class="w-10 h-10 md:hidden justify-self-end rounded-full hover:bg-gray-100">
                <svg
                    class="mx-auto"
                    xmlns="http://www.w3.org/2000/svg"
                    xmlns:xlink="http://www.w3.org/1999/xlink"
                    version="1.1"
                    width="24"
                    height="24"
                    viewBox="0 0 24 24">
                    <path d="M3,6H21V8H3V6M3,11H21V13H3V11M3,16H21V18H3V16Z" />
                </svg>
            </button>
        </nav>
    </header>

    <div>
        <slot />
    </div>


 <!-- Footer -->
 <footer class="bg-gray-800 pt-10 sm:mt-10 w-full">
    <div class="max-w-6xl m-auto text-gray-800 flex-col justify-left">
        <!-- Col-1 -->
        <div class="p-5 w-1/2 sm:w-4/12 md:w-3/12">
            <!-- Col Title -->
            <div class="text-xs uppercase text-gray-400 font-medium mb-6">
                EventPro 
            </div>

            <!-- Links -->
            <!-- <a
                href="#"
                class="my-3 block text-gray-300 hover:text-gray-100 text-sm font-medium duration-700">
                GitHub
            </a>
            <a
                href="#"
                class="my-3 block text-gray-300 hover:text-gray-100 text-sm font-medium duration-700">
                Discord
            </a>
            <a
                href="#"
                class="my-3 block text-gray-300 hover:text-gray-100 text-sm font-medium duration-700">
                Twitter
            </a>
            <a
                href="#"
                class="my-3 block text-gray-300 hover:text-gray-100 text-sm font-medium duration-700">
                YouTube
            </a> -->
            
        </div>
    </div>

    <!-- Copyright Bar -->
    <div class="pt-2">
        <div
            class="flex pb-5 px-3 m-auto pt-5 border-t border-gray-500 text-gray-400 text-sm flex-col md:flex-row max-w-6xl">
            <div class="mt-2">© EventPro | 2023. All Rights Reserved.</div>
        </div>
    </div>
</footer>

</template>