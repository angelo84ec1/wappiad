<script >

import { useRouter } from 'vue-router';
import { reactive } from 'vue';
import ImageLinks from '~/components/ImageLinks.vue'; // Ajusta la ruta según la ubicación real


export default {
  components: {
    ImageLinks,

  },
};


</script>

<template >   

    <ui-header class="mb-3 bg-secondary bg-indigo-600 bg-gray-800 p-5 text-white mt-minus-100"></ui-header>
    

        
    <div>
    <ImageSlider />
  </div>



<div class="spacer"></div>

<div class="grid grid-cols-1 md:grid-cols-4 gap-4">
  <!-- Columna 1 -->
  <div class=" bg-[#FFFFFF] p-1 text-center text-sm">
    <img src="~/assets/images/helicoptero.png" class="img1" alt="...">
    <h3 class="classtitulo text-lg font-normal text-gray-900 text-sm">
        RAPIDEZ
                </h3>
                <div style="border-top: 2px solid #FFF200; width: 30%; margin: 0 auto;"></div> 
    <h3 class="classb text-lg font-normal text-gray-900 text-sm">
        Al contratar un seguro con nosotros, te ofrecemos seguridad y respaldo las 24 horas del día. No te dejamos solo en momentos difíciles, estamos aquí para protegerte y brindarte tranquilidad.
                </h3>
  </div>

  <!-- Columna 2 -->
  <div class="bg-[#FFFFFF] p-1 text-center text-sm">
    <img src="~/assets/images/ahorro.png" class="img1 mt-10 " alt="...">
    <h3 class="classtitulo text-lg font-normal text-gray-900 text-sm">
        EXCLUSIVIDAD
                </h3>
                <div style="border-top: 2px solid #FFF200; width: 30%; margin: 0 auto;"></div> 
    <h3 class="classb text-lg font-normal text-gray-900 text-sm">
        Adquirir una membresía en un club ofrece múltiples beneficios financieros. 
En primer lugar, obtienes  acceso a descuentos exclusivos en  una variedad de productos y  servicios, lo que te permite ahorrar
                </h3>
  </div>

  <!-- Columna 3 -->
  <div class="bg-[#FFFFFF] p-1 text-center text-sm">
    <img src="~/assets/images/seguridad.png" class="img1" alt="...">
    <h3 class="classtitulo text-lg font-normal text-gray-900 text-sm">
        PROTECCIÓN
                </h3>
                <div style="border-top: 2px solid #FFF200; width: 30%; margin: 0 auto;"></div> 
    <h3 class="classb text-lg font-normal text-gray-900 text-sm">
        Nuestra póliza de seguro garantiza protección total para ti y tus seres queridos, brindando paz mental ante imprevistos. Contamos con una sólida reputación y un equipo dedicado a tu seguridad financiera
                </h3>
  </div>

  <!-- Columna 4 -->
  <div class="bg-[#FFFFFF] p-1 text-center text-sm">
    <img src="~/assets/images/experiencia.png" class="img1" alt="...">
    <h3 class="classtitulo text-lg font-normal text-gray-900 text-sm">
        EXPERIENCIA
                </h3>
                <div style="border-top: 2px solid #FFF200; width: 30%; margin: 0 auto;"></div> 
    <h3 class="classb text-lg font-normal text-gray-900 text-sm">
        Cuando eliges nuestro seguro, obtienes décadas de experiencia en la industria, respaldando tus necesidades y preocupaciones. Nuestro equipo experto está listo para brindarte asesoramiento y soluciones a medida 
                </h3>
  </div>
</div>
<div class="spacerfoot"></div>
<div class="bannerfoot">
  <img src="~/assets/images/banner_beneficios.png" class=" " alt="...">
</div>

<div >
  <ImageLinks />
</div>
 

<div class="bannerfoot">
  <img src="~/assets/images/banner_compra_online.png" class=" " alt="...">
</div>
   
    <ui-footer></ui-footer>
 
</template>



<style lang="scss" scoped>
.subscription-card {
    width: 100%;
    max-width: 400px;
    margin: 2rem;
    box-shadow: rgba(0, 0, 0, 0.16) 0px 10px 36px 0px, rgba(0, 0, 0, 0.06) 0px 0px 0px 1px;

    @media (width <640px) {
        margin: 1rem;
    }
}

.heading {
    margin-left: 1rem;
    margin-top: 4px;
    padding: 0px 8px;
    background-color: rgb(109, 109, 177);
    border-radius: 16px;
    font-size: 0.8rem;
    color: white;
    font-weight: bold;
}

.wrapper {
    @media (width <640px) {
        margin: 0;
        padding: 0;
    }
}


.button {
  background-color: #8b5cf6;
  border-radius: 9px;
  padding: 15px 25px;
  color: #fff;
  font-size: 14px;
  line-height: 17px;
  font-weight: bold;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
}

/* Estilo de hover */
.button:hover {
  background-color: #4a4a4a;
}

/* Estilos normales del contenedor */
.container {
  width: 100%;
  padding: 6px 16px;
  border-radius: 8px;
  background-image: linear-gradient(135deg, #8b5cf6, #00ffff);
  color: #000; /* Cambiar el color de texto según tus preferencias */

  /* Estilos adicionales para ajustar el contenido en diferentes tamaños de pantalla */
  /* ... (otros estilos que puedas necesitar) */
}

/* Estilo del contenedor en modo oscuro */
.dark .container {
  background-color: #333; /* Cambiar el color oscuro según tus preferencias */
  color: #fff; /* Cambiar el color de texto en modo oscuro según tus preferencias */
}

/* Estilos del fondo degradado en la sección */


.titulo {

    font-size: 60px;
  background-image: linear-gradient(135deg, #f0f0f0, #cccccc);
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
}



.sectionfooter {
  position: relative;
  overflow: hidden;
  background-image: linear-gradient(135deg, #8b5cf6, #00ffff);
  width: 100%;
  height: 550px;
  z-index: -1;



}

/* Estilos para el contenedor de las columnas */
.flex {
  display: flex; /* Utilizar Flexbox */
  justify-content: space-between; /* Distribuir el espacio entre las columnas */
  z-index: -1;
  
}

.custom-link {
    border-radius: 9px;

  z-index: 0;
  
}


/* Estilos para cada columna */
.column {
  flex: 1; /* Permitir que las columnas ocupen el mismo ancho */
  padding: 16px; 
  z-index: -1;
}


.desk {
  flex: 1; /* Permitir que las columnas ocupen el mismo ancho */
  padding: 16px; 
  z-index: -1;
}

.subscription-price {
  color: #8b5cf6;
}


.contenedor-imagen{
  max-width: 100%;
  height: auto;
}

.classb{

    border-radius: 9px;
background: #FFFFFF;
font-size: 15px;
flex-shrink: 0;
padding: 15px 25px;
}


.img1{

    display: block; /* Para asegurarse de que la imagen sea un elemento de bloque */
  margin: 0 auto; /* Centra horizontalmente la imagen dentro de su contenedor */
  position: relative; /* Si es necesario para otros estilos */
  overflow: hidden; /* Si es necesario para otros estilos */
  margin-top: -65px; /* Tu valor personalizado para el margen superior */
}

@media only screen and (max-width: 1076px) {
  .img1  {
    display: block; /* Para asegurarse de que la imagen sea un elemento de bloque */
  margin: 0 auto; /* Centra horizontalmente la imagen dentro de su contenedor */
  position: relative; /* Si es necesario para otros estilos */
  overflow: hidden; /* Si es necesario para otros estilos */
  margin-top: -40px; /* Tu valor personalizado para el margen superior */
  }
}

.spacer {
  height: 100px; /* Altura del espacio entre los divs */
}

.spacerfoot {
  height: 25px; /* Altura del espacio entre los divs */
}

.classtitulo{


font-size: 20px;
font-weight: bold; /* Agregar negrita */
flex-shrink: 0;
padding: 15px 25px;
}

.bannerfoot img {

  width: 100%; /* Ajustar la imagen al 100% del ancho de su contenedor */
  height: auto; /* Mantener la proporción de aspecto original */
  display: block; /* Para asegurarse de que la imagen sea un elemento de bloque */

}

.carousel__item {
  min-height: 200px;
  width: 100%;
  background-color: var(--vc-clr-primary);
  color: var(--vc-clr-white);
  font-size: 20px;
  border-radius: 8px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.carousel__slide {
  padding: 10px;
}

.carousel__prev,
.carousel__next {
  box-sizing: content-box;
  border: 5px solid white;
}

</style>

