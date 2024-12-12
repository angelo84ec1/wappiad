

<template>

<div id="default-carousel" class="relative w-full" data-carousel="slide">
    <!-- Carousel wrapper -->
    <div class="relative h-56 overflow-hidden rounded-lg md:h-96">
         <!-- Item 1 -->
        <div class="hidden duration-700 ease-in-out" data-carousel-item>
            <img src="~/assets/images/banner_chica.png" class="absolute block w-full -translate-x-1/2 -translate-y-1/2 top-1/2 left-1/2" alt="...">
        </div>
        <!-- Item 2 -->
        <div class="hidden duration-700 ease-in-out" data-carousel-item>
            <img src="~/assets/images/banner_asistencia_hogar.png" class="absolute block w-full -translate-x-1/2 -translate-y-1/2 top-1/2 left-1/2" alt="...">
        </div>
       
    </div>
    <!-- Slider indicators -->
    <div class="absolute z-30 flex -translate-x-1/2 bottom-5 left-1/2 space-x-3 rtl:space-x-reverse">
        <button type="button" class="w-3 h-3 rounded-full" aria-current="true" aria-label="Slide 1" data-carousel-slide-to="0"></button>
        <button type="button" class="w-3 h-3 rounded-full" aria-current="false" aria-label="Slide 2" data-carousel-slide-to="1"></button>
   
    </div>
    <!-- Slider controls -->
    <button type="button" class="absolute top-0  flex items-center justify-center h-full px-4  cursor-pointer" >
        <span class=" inline-flex items-center justify-center w-10 h-10  ">
           
           
        </span>
    </button>
    <button type="button" class="absolute top-0  flex items-center justify-center h-full px-4 cursor-pointer" >
        <span class="inline-flex items-center justify-center w-10 h-10   ">
  
        </span>
    </button>
</div>
</template>


<script>

import { ref, onMounted } from 'vue';
import { Carousel } from 'flowbite'; // o el nombre correcto de la librería que estás utilizando

export default {
  setup() {
    const carouselElement = document.getElementById('default-carousel');

    // ... otras variables y elementos necesarios

    onMounted(() => {
      const carousel = new Carousel(carouselElement, items, options, instanceOptions);
    });

    // ... otras configuraciones y datos

    return {
      // ... otras variables y funciones
    };
  },
};
</script>
