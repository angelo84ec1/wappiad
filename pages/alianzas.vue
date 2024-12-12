<template>
    <ui-header></ui-header>
   
   
<div class="mx-auto text-overlay">ALIANZAS</div>

    <div class="flex flex-wrap" style="padding-left: 15px; padding-right: 18px;">
        

<div class="p-4 flex items-center">


    <div class="flex flex-col lg:flex-row">
    <ImagenColumna />
    <FormularioColumna />
  </div>

 </div>
</div>




   <div class="spacer"></div>
 <ui-footer></ui-footer>
 </template>
<script>
import ImagenColumna from '~/components/ImagenColumna.vue';
import FormularioColumna from '~/components/FormularioColumna.vue';

export default {
  components: {
    ImagenColumna,
    FormularioColumna,
  },
};
</script>
 

<style scoped lang="scss">
body {

 position: relative;
}

.flex {
   overflow-x: hidden !important;
 position: relative;
}

.spacer {
 height: 15px; /* Altura del espacio entre los divs */
}

.image-container {
 position: relative;
 display: inline-block; /* Para asegurarse de que el contenedor se ajuste al tamaño de la imagen */
}

.image {
 max-width: 100%; /* Asegura que la imagen no sea más ancha que su contenedor */
}

h1.text-base {
   overflow-x: hidden !important;
 font-size: 22px;
}

.text-overlay {

 font-size: 35px;
 color: #FFF200;
 background: rgba(0, 0, 0); /* Fondo semitransparente para hacer que el texto sea legible */
padding: 40px;
}
h1.text-base {
   overflow-x: hidden !important;
 font-size: 22px;
}

.p-4 {
       background-color: #FBF8FF;
       border-radius: 9px;
       margin-top: 20px;


     }

     .text-xs {
       font-size: 18px;
       padding: 12px;
   }
</style>