<template>
  <main>
    <header>
      <img
        v-if="dataUser && dataUser.datos_personales?.foto?.url"
        :src="getProfilePicture(dataUser.datos_personales.foto.url)"
        :alt="dataUser.datos_personales.nombres ?? 'profile-picture'"
        class="header__photo"
      />
      <div class="header__text">
        <h1 v-if="dataUser && dataUser.datos_personales">
          Bienvenido, {{ dataUser.datos_personales.nombres }}
          {{ dataUser.datos_personales.apellidos }}
        </h1>

      </div>
    </header>
    <div class="home__content">
      <div class="home__actions">
        <h2>Datos personales</h2>
        <div class="home__buttons">
          <button class="button button--secondary" @click.prevent="save()">
            <img src="~/assets/images/save-green.png" alt="" /> Guardar cambios
          </button>
         
          
        </div>
      </div>
      
      <form ref="formPersonalData" class="form">
        <div class="form__group">
          <h2>Sobre tí</h2>
          <div class="two-columns">
            <BaseFileInput
              label="Foto de perfil"
              name="foto"
              @file-updated="captureFile($event)"
            />
            <BaseInputImageFromWebcam
              label="Foto de perfil de webcam"
              name="fotoWebcam"
              @file-updated="captureFile($event)"
            />
           
            <BaseInput
              v-model="names"
              type="text"
              label="Nombres"
              :disabled="false"
              class="new-line"
              name="nombres"
            />
            <BaseInput
              v-model="lastnames"
              type="text"
              label="Apellidos"
              :disabled="false"
              name="apellidos"
            />

            <BaseInput
              v-model="company"
              type="text"
              label="Compañia"
              :disabled="false"
              name="compania"
            />

            
            <BaseInput
              v-model="idRuc"
              type="text"
              label="Identificación o Ruc"
              :disabled="false"
            />

            <BaseInput
              v-model="iCedula"
              type="text"
              label="Cedula"
              :disabled="false"
            />

            <BaseInput
              v-model="profesional"
              type="text"
              label="Profesion"
              :disabled="false"
            />
            <BaseInput
              v-model="passport"
              type="text"
              label="Pasaporte"
              :disabled="false"
            />
            <BaseInput
              v-model="datehome"
              type="date"
              label="Fecha Inicio"
              name="fecha_inicio"
              :disabled="true"
            />
    
              
            <BaseInput
              v-model="dateend"
              type="date"
              label="Fecha Fin"
              name="fecha_fin"
              :disabled="true"
            />


            <BaseInput
              v-model="nationality"
              type="text"
              label="Nacionalidad"
              :disabled="false"
              name="nacionalidad"
            />

            <BaseInput
              v-model="civilState"
              type="text"
              label="Estado Civil"
              :disabled="false"
              name="estado_civil"
            />

            

            <BaseInput
              v-model="typeservice"
              type="text"
              label="Tipo de servicio"
              :disabled="false"
              name="tipo_servicio"
            />


            <BaseInput
              v-model="ocupation"
              type="text"
              label="Ocupacion"
              :disabled="false"
              name="ocupacion"
            />

         

                     
            <BaseInput
              v-model="country"
              type="text"
              label="Pais"
              :disabled="false"
              name="pais"
            />


            <BaseInput
              v-model="city"
              type="text"
              label="Ciudad"
              :disabled="false"
              name="ciudad"
            />


            <BaseInput
              v-model="province"
              type="text"
              label="Provincia"
              :disabled="false"
              name="provincia"
            />

            <BaseInput
              v-model="typeperson"
              type="text"
              label="Tipo de persona"
              :disabled="false"
              name="tipo_persona"
            />

            <BaseInput
              v-model="plane"
              type="text"
              label="Plan"
              :disabled="false"
              name="plan"
            />

            
            <BaseInput
              v-model="birthDate"
              type="text"
              label="Fecha de Nacimiento"
              :disabled="false"
              name="fecha_nacimiento"
            />

               
            <BaseInput
              v-model="polizaa"
              type="text"
              label="Poliza"
              :disabled="false"
              name="poliza"
            />


            <BaseInput
              v-model="certificade"
              type="text"
              label="Certificado"
              :disabled="false"
              name="certificado"
            />


            
            <BaseInput
              v-model="marcavehicule"
              type="text"
              label="Marca Vehiculo"
              :disabled="false"
              name="marca_vehiculo"
            />


            <BaseInput
              v-model="model"
              type="text"
              label="Modelo"
              :disabled="false"
              name="modelo"
            />


            <BaseInput
              v-model="year"
              type="text"
              label="Año"
              :disabled="false"
              name="anio"
            />


            <BaseInput
              v-model="collot"
              type="text"
              label="Color"
              :disabled="false"
              name="color"
            />


            <BaseInput
              v-model="placmet"
              type="text"
              label="Placa"
              :disabled="false"
              name="placa"
            />


            <BaseInput
              v-model="chekoil"
              type="text"
              label="Motor"
              :disabled="false"
              name="motor"
            />

            <BaseInput
              v-model="chas"
              type="text"
              label="Chasis"
              :disabled="false"
              name="chasis"
            />

            <BaseInput
              v-model="estable"
              type="text"
              label="Establecimientos"
              :disabled="false"
              name="establecimientos"
            />
            
            <BaseSelect v-model="gender" label="Sexo" :options="sexOptions" name="sexo" />
            <BaseSelect
              v-model="disability"
              label="Discapacidad fisica o mental"
              :options="yesNoOptions"
              name="discapacidad"
            />
            
          </div>
        </div>

        <div class="form__group">
          <h2>Contacto</h2>
          <div class="two-columns">
            <div>
              <label>Celular</label>
              <VueTelInput v-model="cellphone" mode="international"></VueTelInput>
              <!-- <BaseInput v-model="cellphone" type="text" label="Celular" name="celular" /> -->
            </div>
            <div>
              <label>Teléfono convencional</label>
              <VueTelInput v-model="phone" mode="international"></VueTelInput>
              <!-- <BaseInput v-model="phone" type="text" label="Teléfono convencional" name="telefono_convencional" /> -->
            </div>
            <BaseInput v-model="email" type="email" label="Correo" name="correo" />
           
           
           
          </div>
        </div>


      </form>
    </div>

  </main>
</template>
<script setup lang="ts">



import { VueTelInput } from "vue-tel-input";
import "vue-tel-input/dist/vue-tel-input.css";

import BaseInput from "~/components/common/inputs/base-input.vue";

import BaseFileInput from "~/components/common/inputs/file-input.vue";
import { useAuthStore } from "~/store/auth";


import { useToast } from "vue-toastification";
import BaseInputImageFromWebcam from "~/components/common/inputs/file-input-image-webcam.vue";
definePageMeta({
  title: "Socios",
  name: "Socios Page",
  components: {
    BaseInput,
    BaseFileInput,
    BaseInputImageFromWebcam,
  },
  layout: "private",
  middleware: ["auth"],
});

const authStore = useAuthStore();
const router = useRouter();

const {
  public: { baseURL },
} = useRuntimeConfig();
const BASE_URL = baseURL;

const getProfilePicture = (url: string) => `${BASE_URL}${url}`;

const generateRandomString = (num) => {
  const characters = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789";
  let result1 = Math.random().toString(36).substring(0, num);

  return result1;
};

console.log(generateRandomString(7));


const sexOptions = ref<SelectOption[]>([
  { text: "Masculino", value: "M" },
  { text: "Femenino", value: "F" },
]);
const yesNoOptions = ref([
  { text: "Si", value: true },
  { text: "No", value: false },
]);
const civilStateOptions = ref<SelectOption[]>([
  { text: "Casado", value: "casado" },
  { text: "Divorciado", value: "divorciado" },
  { text: "Viudo", value: "viudo" },
  { text: "Soltero", value: "soltero" },
]);

const file = ref<File | null>(null);
const names = ref<string>("");
const lastnames = ref<string>("");
const company = ref<string>("");
const idRuc = ref<string>("");
const iCedula = ref<string>("");
const profesional = ref<string>("");
const passport = ref<string>("");
const birthDate = ref<string>("");
const gender = ref<string>("");
const disability = ref<boolean>(false);
const nationality = ref<string>("");
const civilState = ref<string>("");
const cellphone = ref<string>("");
const phone = ref<string>("");
const email = ref<string>("");
const datehome = ref<string>("");
const typeservice = ref<string>("");
const ocupation = ref<string>("");
const dateend = ref<string>("");
const country = ref<string>("");
  const city = ref<string>("");
    const province = ref<string>("");
      const typeperson = ref<string>("");
        const typetarjet = ref<string>("");
          const plane = ref<string>("");
              const polizaa = ref<string>("");
              const certificade = ref<string>("");
                const marcavehicule = ref<string>("");
                  const model = ref<string>("");
                    const year = ref<string>("");

                    const  collot = ref<string>("");
              const  placmet = ref<string>("");
                const  chekoil = ref<string>("");
                  const   chas = ref<string>("");
                    const estable = ref<string>("");

const webCamImage = ref<File | null>(null);

const { data: dataUser } = useFetch<User>(`${BASE_URL}/users/${authStore.user?.id}`, {
  method: "GET",
  headers: {
    "Content-Type": "application/json",
    Authorization: `Bearer ${authStore.token}`,
  },
});

watch(dataUser, () => {

  names.value = dataUser.value?.datos_personales?.nombres ?? "";
  lastnames.value = dataUser.value?.datos_personales?.apellidos ?? "";
  company.value = dataUser.value?.datos_personales?.compania ?? "";
  idRuc.value = dataUser.value?.datos_personales?.cedula_ruc ?? "";
  iCedula.value = dataUser.value?.datos_personales?.cedula ?? "";
  profesional.value = dataUser.value?.datos_personales?.profesion ?? "";
  passport.value = dataUser.value?.datos_personales?.pasaporte ?? "";
  gender.value = dataUser.value?.datos_personales?.sexo ?? "";
  datehome.value = dataUser.value?.datos_personales?.fecha_inicio ?? "";
  disability.value = dataUser.value?.datos_personales?.discapacidad ?? false;
  nationality.value = dataUser.value?.datos_personales?.nacionalidad ?? "";
  civilState.value = dataUser.value?.datos_personales?.estado_civil ?? "";
  cellphone .value = dataUser.value?.datos_personales?.celular ?? "";
  phone .value = dataUser.value?.datos_personales?.telefono_convencional ?? "";
  email.value = dataUser.value?.datos_personales?.correo ?? "";
  typeservice.value = dataUser.value?.datos_personales?.tipo_de_servicio ?? "";
 ocupation.value = dataUser.value?.datos_personales?.ocupacion ?? "";
 dateend.value = dataUser.value?.datos_personales?.fecha_fin ?? "";
 country.value = dataUser.value?.datos_personales?.pais ?? "";
 city.value = dataUser.value?.datos_personales?.ciudad ?? "";
 province.value = dataUser.value?.datos_personales?.provincia ?? "";
 typeperson.value = dataUser.value?.datos_personales?.tipo_persona ?? "";
 typetarjet.value = dataUser.value?.datos_personales?.tipo_tarjeta ?? "";
 plane.value = dataUser.value?.datos_personales?.plan ?? "";
  birthDate.value = dataUser.value?.datos_personales?.fecha_nacimiento ?? "";
  polizaa.value = dataUser.value?.datos_personales?.poliza ?? "";
  certificade.value = dataUser.value?.datos_personales?.certificado ?? "";
  marcavehicule.value = dataUser.value?.datos_personales?.marca ?? "";
  model.value = dataUser.value?.datos_personales?.modelo?? "";
  year.value = dataUser.value?.datos_personales?.anio?? "";
  collot.value = dataUser.value?.datos_personales?.color?? "";
  placmet.value = dataUser.value?.datos_personales?.placa?? "";
  chekoil.value = dataUser.value?.datos_personales?.motor?? "";
  chas.value = dataUser.value?.datos_personales?.chasis?? "";
  estable.value = dataUser.value?.datos_personales?.establecimientos?? "";
});
const formPersonalData = ref<HTMLFormElement | null>(null);

const toast = useToast();

const save = async () => {
  try {
    const data: Record<string, string> = {};
    const formData = new FormData();
    const elements = [...formPersonalData.value.elements];
    // console.log(elements);
    elements.forEach(({ name, type, value, files, ...element }) => {
      if (!["submit", "file", "date"].includes(type)) {
        if (name == "") return;

        data[name] = value;
      } else if (type === "date") {
        if (value == "" || value.length === 0) return;
        data[name] = value;
      } else if (type === "file") {
        const fileList = [...files];
        fileList.forEach((file) => {
          formData.append(`files.${name}`, file, file.name);
        });
      }
    });

    if (webCamImage.value !== null) {
      formData.delete("files.foto");
      formData.append("files.foto", webCamImage.value, webCamImage.value.name);
    }

    formData.append("data", JSON.stringify(data));
    const infoUpdated = await $fetch(
      `${baseURL}/datos-personales/${dataUser.value?.datos_personales?.id}`,
      {
        method: "PUT",
        headers: {
          Authorization: `Bearer ${authStore.token}`,
        },
        body: formData,
      }
    );
    console.log(infoUpdated);
    dataUser.value.datos_personales = infoUpdated;
    toast.success("Datos actualizados correctamente");
  } catch (error) {
    console.log(error);
    toast.error("Error al actualizar los datos");
  }
};



const captureFile = (event: File) => {
  webCamImage.value = event;
  console.log("Hola");
};

</script>
<style scoped>
header {
  padding: 1rem 0;
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
  border-bottom: 1px solid var(--gray-200);
}

.header__text > h1 {
  font-size: var(--heading-2);
}

.header__photo {
  width: 3rem;
  height: 3rem;
  border-radius: 50%;
}

.home__actions > h2 {
  font-size: var(--heading-1);
}

.home__actions {
  padding: 1rem 0;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.home__buttons {
  display: flex;
  gap: 1rem;
  flex-wrap: wrap;
}

.home__link {
  color: var(--links);
}

.home__link:hover {
  color: gray; /* Color al hacer hover */
}
.form {
  padding: 1rem 0;
}

.form__group {
  padding: 2rem 0;
  border-bottom: 1px solid var(--gray-200);
  max-width: 670px;
}

.two-columns {
  display: grid;
  gap: 1rem;
  grid-template-columns: repeat(auto-fit, minmax(327px, 1fr));
}




.one-column {
  display: grid;
  gap: 1rem;
  grid-template-columns: auto;
}

label {
  display: flex;
  flex-direction: column;
  gap: 0.25rem;
}

label > input {
  height: 40px;
  padding: 0 0.5rem;
}

.new-line {
  grid-column: 1;
}

label + h3,
.one-column > h3 {
  margin-top: 1rem;
}

.form__group > h2 {
  margin-bottom: 1rem;
}

.full-column {
  grid-column: 1/-1;
}


.full-column label {
  /* Tus estilos aquí */
  color: #000;
  font-weight: 700; /* Grosor de fuente reducido */
  font-size: 2rem; /* Tamaño de fuente 1 */

}



.home_buttons {

  text-decoration: none;
  color: var(--green-400);


  align-items: center;
  justify-content: center;
  padding:1px;
  background-color: transparent;
  border-radius: 6px;

  
  border: 1px solid var(--green-500); /* Borde de 2px sólido en color verde */
}




.home_buttons:hover {
  background-color: var(--green-400);
}

.home_buttons--primary {
  display: flex;
  gap: 0.25rem;
  align-items: center;
  justify-content: center;
  padding: 0 1rem;
  color: var(--white);
  text-decoration: none;
  color: #000;
  font-weight: 500; /* Grosor de fuente reducido */
  font-size: 1rem; /* Tamaño de fuente 1 */

}

.button--secondary {


}

@media (max-width: 767px) {
  .button--secondary {
    position: fixed;
    width: 100%; /* Ocupa todo el ancho disponible */
    right: 2px;
    margin-top: 402px; 
    padding: 0 1rem;
    text-align: center; /* Centra el contenido horizontalmente */
    display: flex;
   
    z-index: 1; /* Asegúrate de que esté en un z-index superior para que esté por encima del contenido */
  }
}


.home_buttons--primary:hover {
  color: var(--white);
}

.home_buttons>img {
  width: 1.5rem;
}

.float{

position: fixed;
top: 180px;
right: 21px;
z-index: 0;


}
/* Estilos para pantallas más pequeñas (por ejemplo, menos de 768px) */
@media (max-width: 767px) {
  .home_buttons {
    justify-content: center; /* Mantén o ajusta los estilos según sea necesario para el diseño responsivo */
    padding: 8px;
    position: fixed;
  bottom: 0;
  left: 0;
  width: 100%;
  background-color: #fff; /* Puedes ajustar el color de fondo según tu diseño */
  padding: 10px; /* Espacio de relleno opcional para separar el enlace del borde inferior */
  text-align: center;
  z-index: 1; /* Asegúrate de que esté en un z-index superior para que esté por encima del contenido */
  }
}

/*breackpoint*/
@media only screen and (max-width: 600px) {
    .d-flex {
      display: flex !important;
      flex-direction: column;
      flex-wrap: wrap;
    }
    .full-column, .full-column-2 {
      width: 100% !important;
    }
    .form__group {
      max-width: 100% !important;
    }

    .one-column {
      width: 100% !important;
}
  }

  

</style>
