<script setup>
import { initFlowbite } from "flowbite";
import { usePaymentStore } from "@/store/payment/index.js";
import { useRouter } from "vue-router";
import { reactive } from "vue";
import pkg1Img from "@/assets/videos/plan_silver.png";
import pkg2Img from "@/assets/videos/planb.png";
import pkg3Img from "@/assets/videos/planc.png";
import lottieAnimation from "@/assets/images/animation_lklw6so3.json";

const store = usePaymentStore();
const router = useRouter();
const user = true;


const Subscription = reactive([
  {
    id: 4,
    name: "Plan Silver",
    image: pkg1Img,
    heading: "Online",
    price: 60,
    discount: 0,
    
    benifits: [
      "Coordinación de Asistencia Multas de tránsito ",
"Coordinación de Asistencia Legal por Robo o Accidente ",
"Remolque de vehículos livianos ",
"Auxilio Mecánico (Coordinación de Auxilio Vial) ",
"Más beneficios en camino",
    ],
  },
  {
    id: 5,
    name: " Plan Gold",
    image: pkg2Img,
    heading: "value",
    price: 80,
    discount: 0,

    benifits: [
      "Auxilio Mecánico (Coordinación de Auxilio Vial)",
"Coordinación de Ángel Guardian",
"Coordinación de Traslado del vehículo a taller para mantenimiento",
"Coordinación de Asistencia Legal por Robo o Accidente",
"Remolque de vehículos livianos",
"Auxilio Mecánico (Coordinación de Auxilio Vial)",
"Mecánica Ligera",
"Más beneficios en camino",
    ],
  },
  {
    id: 6,
    name: " Plan Black ",
    image: pkg3Img,
    heading: "pro",
    price:120,
    discount: 0,
    
    benifits: [
      "Coordinación Asistencia Multas de tránsito",
"Coordinación Angel Guardian",
"Coordinación de traslado del auto a taller para realizar mantenimiento o cambio de neumáticos",
"Coordinación de Tramitador Personal",
"Coordinación de Asistencia para Permiso de conducción",
"Coordinación de Asistencia Legal Telefónica por Robo o Accidente",
"Coordinación de Auxilio Vial",
"Coordinación de Mecánica Ligera",
"Coordinación de Golpes Leves",
"Coordinación de asistencia en reposición de retrovisores por robo o daño",
"Coordinación Marido de alquiler (handyman)",
"Coordinación de Asistencia hogar (plomería, cerrajería, Vidiería y Electricidad)",
"Más beneficios en camino",



    ],
  },
]);



const addToCart = (item) => {
  if (user) {
    store.cart.push(item);
    store.successMessage("Añadido al Carrito");
    router.push("products");
  }
};

// initialize components based on data attribute selectors
onMounted(() => {
  initFlowbite();
});




</script>

<template>
  <ui-header></ui-header>
  <div class="spacer"></div>
  <div class="bannerfoot" data-carousel-item>
    
    <img src="~/assets/images/img_planes.png" class="" alt="..." />
  </div>
  <div class="spacer"></div>
  

    <div class="columcss grid grid-cols-3 gap-4">
    <div
      v-for="sub in Subscription"
      :key="sub.name"
      class="w-full subscription-card bg-[#fff] rounded-[10px] shadow-[0px 1px 2px #E1E3E5] border border-[#E1E3E5] divide-y"
    >
      <div class="pt-[15px] px-[25px] pb-[25px]">
        <div class="flex justify-end">
          <div
            class="bg-[#F6F6F7] rounded-[20px] flex justify-center align-center px-[12px]"
          >
            <p class="text-[#00153B] heading text-[12px] leading-[28px] font-bold">
              {{ sub.heading }}
            </p>
          </div>
        </div>

        <div>
          <p class="text-[#DF2F91] text-[34px] leading-[24px] font-bold">
            {{ sub.name }}
          </p>

          <img :src="sub.image" alt="Image" :style="{ padding: '20px' }" />

          <p class="subscription-price text-[40px] leading-[63px] font-bold">
            $ {{ sub.price }} +IVA
          </p>
        </div>

        <div>
          <p
            class="text-[#717F87] text-[18px] leading-[28px] font-medium"
            v-for="detail in sub.details"
          >
            {{ detail }}
          </p>
        </div>
      </div>

      <div
        class="pt-[25px] px-[25px] pb-[35px] i-mdi-home hover:i-mdi-home-alert text-5xl text-green-800"
      >
        <div>
          <div
            v-for="(benifit, index) in sub.benifits"
            :key="index"
            class="flex items-center space-x-2"
          >
            <!-- SVG icon -->
            <svg
            class="h-5 w-5 text-[#DF2F91]"
              width="24"
              height="24"
              viewBox="0 0 24 24"
              stroke-width="2"
              stroke="currentColor"
              fill="none"
              stroke-linecap="round"
              stroke-linejoin="round"
            >
            <path d="M5 13l4 4L19 7"></path>
             
            </svg>

            <!-- Texto del beneficio -->
            <p class="flex-grow text-[#717F87] text-[14px] leading-[24px] font-medium">
              {{ benifit }}
            </p>
          </div>
        </div>

        <div class="mt-[25px]">
          <button class="button" @click="addToCart(sub)">Añadir Carrito +</button>
        </div>
      </div>
    </div>
  </div>

  <div class="spacer"></div>
  <ui-footer></ui-footer>
</template>

<style scoped lang="scss">
body {
  position: relative;
}

.spacer {
  height: 15px; /* Altura del espacio entre los divs */
}

.bannerfoot {
  position: relative;
  text-align: center; /* Alinea el texto en el centro horizontal */
}

.text-left-center {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh; /* Establece la altura del contenedor a la altura de la ventana */
  /* Añade estilos adicionales para el contenedor según tus necesidades */

  position: absolute;
  top: 50%;
  left: 500px;
  transform: translate(0, -50%);
  font-size: 60px;
  font-family: "Poppins", sans-serif; /* Establece la fuente a Poppins y utiliza sans-serif como fuente de respaldo */
  font-weight: bold; /* Establece la fuente en negrita */
  font-size: 60px; /* Establece el tamaño de fuente en 30px */
  color: #0200AB; /* Puedes ajustar el color según tus preferencias */
  padding-top: 0;
  padding-bottom: 0;
  padding-left: 25px;
  padding-right: 0;
}

/* Media query para ajustar estilos en pantallas más pequeñas */
@media (max-width: 768px) {
  .text-left-center {
    position: absolute;
    top: 50%;
    left: 50px;
    transform: translate(0, -50%);
    font-size: 30px; /* Establece el tamaño de fuente en 30px */
    /* Cambia el diseño o estilos en pantallas más pequeñas si es necesario */
  }
}

.button {
  background-color: #0200AB;
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
  background-color: #2F1071;
}

/* Estilos normales del contenedor */

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



/* Estilos para el contenedor de las columnas */
.flex {
  display: flex; /* Utilizar Flexbox */
  justify-content: space-between; /* Distribuir el espacio entre las columnas */
  z-index: -1;
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
  color: #000000;
}




.contenedor-imagen {
  max-width: 100%;
  height: auto;
}

.columcss {
  padding: 25px;
}
</style>
