<template>
    <ui-header></ui-header>
   
   
    <div class="image-container" data-carousel-item>
    
    <img src="~/assets/images/banner_soporte.png" class="" alt="..." />
    <div class="text-overlay">Estamos aquí para escucharte! </div>
    <div class="text-overlay-file2">Envíanos cualquier pregunta, comentario, sugerencia o reclamo que tengas. </div>
  </div>
<div class="flex " style="padding-left: 15px; padding-right: 18px; width: 100%;" >
        

 <div class="flex items-center  " style="width: 100%;">
    
        <FormularioSoporte/>
        

 
     

  </div>
</div>




   <div class="spacer"></div>
 <ui-footer></ui-footer>
 </template>
<script>
import ImagenSoporte from '~/components/ImagenSoporte.vue';
import FormularioSoporte from '~/components/FormularioSoporte.vue';

export default {
  components: {
    ImagenSoporte,
    FormularioSoporte,
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

   .text-overlay {
  position: absolute;
  top: 50%; /* Coloca el texto en el centro vertical */
 left: 18%; /* Coloca el texto en el centro horizontal */
  transform: translate(-50%, -50%); /* Alinea el centro del texto con el centro del contenedor */
  font-family: 'Poppins', sans-serif; /* Establece la fuente 'Poppins' como tipografía */
  font-weight:300; /* Establece el grosor de fuente 'Medium' */
  /* El resto de tus estilos para el texto superpuesto */
  font-size: 1.5vw;
  color: white; /* Cambia el color del texto según tus preferencias */
  background: rgba(0, 0, 0, 0.6); /* Fondo semitransparente para hacer que el texto sea legible */
  padding: 2px 5px; /* Añade relleno al texto */
  border-radius: 5px; /* Añade esquinas redondeadas al fondo del texto */
}

.text-overlay-file2 {
  position: absolute;
  top: 65%; /* Coloca el texto en el centro vertical */
 left:32%; /* Coloca el texto en el centro horizontal */
 
  transform: translate(-50%, -50%); /* Alinea el centro del texto con el centro del contenedor */
  font-family: 'Poppins', sans-serif; /* Establece la fuente 'Poppins' como tipografía */
  font-weight:200; /* Establece el grosor de fuente 'Medium' */
  /* El resto de tus estilos para el texto superpuesto */
  font-size: 1.3vw; /* Tamaño del texto relativo al ancho de la pantalla */
  color: white;
  background: rgba(0, 0, 0, 0.6); /* Fondo semitransparente para hacer que el texto sea legible */
  padding: 0.5em 1em;
  border-radius: 5px;
}

.columborder {

    background: rgba(255, 255, 255, 0.733); /* Fondo semitransparente para hacer que el texto sea legible */
    padding: 35px 20px 35px 20px ;
    border-radius: 5px;
    border: 1px solid #585858c0; /* Borde de color negro */

}
</style>