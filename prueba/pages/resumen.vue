<template>
  <main>
    <header>
      <div class="header__text">
        <div class="header__description">
          <h1>Dashboard</h1>
        </div>
        <div class="header__actions">
          <button class="button button--secondary" @click.prevent="printPage()">
            <img src="~/assets/images/imprimir-green.png" alt="" srcset="" />
            Imprimir
          </button>
       
          <button
            class="button button--secondary"
            @click="sendDataToIPAddress(user?.datos_personales)"
          >
            <img src="~/assets/images/email-green.png" alt="" />Enviar Json
            Coris
          </button>
        </div>
      </div>
    </header>
    <div class="home__content">
      <div class="backdrop" v-if="showBackDrop && isBackdrop">
        <div class="message-box">
          <!-- <h1>Dummy Message</h1> -->
          <p>Favor llenar los campos pendientes</p>
          <div class="outer" @click="closeBackdrop">
            <div class="inner">
              <label>Back</label>
            </div>
          </div>
        </div>
      </div>

      <div class="socio__info">
        <div class="socio__profile">
          <img
            v-if="user?.datos_personales?.foto != null"
            :src="getProfilePicture(user?.datos_personales?.foto.url)"
            :alt="user?.datos_personales?.nombres"
            class="header__photo"
          />
          <img
            v-else
            src="~/assets/images/profile.png"
            alt="default-profile-picture"
          />

          <div>
            <h2
              class="socio__name"
              v-if="
                user?.datos_personales?.nombres &&
                user.datos_personales.apellidos
              "
            >
              {{
                `${user?.datos_personales?.nombres} ${user?.datos_personales?.apellidos}`
              }}
            </h2>
            <h2 v-else>
              {{ user?.datos_personales?.nombres ?? "" }}
            </h2>
            <ul>
             
              <li>
                <b>Correo:</b><span>{{ user?.datos_personales?.correo }}</span>
              </li>
              <li>
                <b>Identificación:</b
                ><span>{{ user?.datos_personales?.cedula_ruc }}</span>
              </li>
              <li>
                <b>Estado:</b><span>{{ user?.estado }}</span>
              </li>
            </ul>
          </div>
        </div>
        <div class="">
          <!-- <img src="~/assets/images/qrcode-generado.png" alt="" srcset="" /> -->
          <img :src="qrcode" alt="" srcset="" />
          <a href="#" @click="generatePDF" style="color: #DF2F91; font-size: 12px; text-align: center;">Descargar QR</a>
        </div>
        <div v-if="isPrint" class="socio__print_info">
         
         
        
        </div>
        <div class="socio__saldos" v-else>
          <div class="socio__saldo">
            <!-- Code by Saeed-->
            <span class="socio__saldo--positivo"
              >2 <img src="~/assets/images/socioimg.png"
            /></span>
            <p># Socios</p>
          </div>

          <div class="socio__saldo">
            <span class="socio__saldo--negativo"
              >5<img src="~/assets/images/establecimientosimg.png"
            /></span>
            <p># Establecimientos</p>
          </div>

          <div class="socio__saldo">
            <span class="socio__saldo--base"
              >10<img src="~/assets/images/contratos.png"
            /></span>
            <p># Planes Contratados</p>
          </div>
        </div>
      </div>
      <div class="cards__container">
        <div class="card">
          <h3>Datos personales</h3>
          <ul class="card__list">
            <li>
              <b>Número de Ruc:</b>&nbsp;
              <span>{{ user?.datos_personales?.cedula_ruc }}</span>
            </li>
            <li>
              <b>Número de pasaporte:</b>&nbsp;
              <span>{{ user?.datos_personales?.pasaporte }}</span>
            </li>
            <li>
              <b>Fecha de nacimiento: </b>&nbsp;
              <span>{{ user?.datos_personales?.fecha_nacimiento }}</span>
            </li>
            <li>
              <b>País:</b>&nbsp;
              <span>{{ user?.datos_personales?.pais }}</span>
            </li>
            <li>
              <b>Ciudad:</b>&nbsp;
              <span>{{ user?.datos_personales?.ciudad }}</span>
            </li>
            <li>
              <b>Dirección:</b>&nbsp;
              <span>{{ user?.datos_personales?.codigo_postal }}</span>
            </li>
            <li>
              <b>Celular:</b>&nbsp;
              <span>{{ user?.datos_personales?.celular }}</span>
            </li>
          </ul>
        </div>

        <!--<div class="card">
          <h3>Aprobaciones</h3>
          <ul class="card__list">
            <li><b>Aprobación del pago:</b>{{ "" }}</li>
            <li><b>Observaciones del pago:</b>{{ "" }}</li>
            <li><b>Fecha de contratación:</b>{{ "" }}</li>
            <li><b>Grupo anticipo:</b>{{ "" }}</li>
            <li><b>Cancelaciones:</b>{{ "" }}</li>
            <li><b>Pago anticipado:</b>{{ "" }}</li>
          </ul>
        </div> -->

        <div class="card">
          <div class="card">
            <h3>Coris</h3>
            <ul class="card__list">
              <li>
                <b>Fecha Inicio</b>&nbsp;
                <span>{{ user?.datos_personales?.fecha_inicio }}</span>
              </li>
              <li>
                <b>Fecha Fin</b>&nbsp;
                <span>{{ user?.datos_personales?.fecha_fin }}</span>
              </li>
              <li>
                <b>Tipo Persona </b>&nbsp;
                <span>{{ user?.datos_personales?.tipo_persona }}</span>
              </li>
              <li>
                <b>Tipo Tarjeta</b>&nbsp;
                <span>{{ user?.datos_personales?.tipo_tarjeta }}</span>
              </li>
              <li>
                <b>Plan</b>&nbsp;
                <span>{{ user?.datos_personales?.plan }}</span>
              </li>
              <li>
                <b>Poliza</b>&nbsp;
                <span>{{ user?.datos_personales?.poliza }}</span>
              </li>
              <li>
                <b>Certificado</b>&nbsp;
                <span>{{ user?.datos_personales?.certificado }}</span>
              </li>
              <li>
                <b>Marca</b>&nbsp;
                <span>{{ user?.datos_personales?.marca }}</span>
              </li>
              <li>
                <b>Modelo</b>&nbsp;
                <span>{{ user?.datos_personales?.modelo }}</span>
              </li>
              <li>
                <b>Año</b>&nbsp;
                <span>{{ user?.datos_personales?.anio }}</span>
              </li>
              <li>
                <b>Color</b>&nbsp;
                <span>{{ user?.datos_personales?.color }}</span>
              </li>
              <li>
                <b>Placa</b>&nbsp;
                <span>{{ user?.datos_personales?.placa }}</span>
              </li>
              <li>
                <b>Motor</b>&nbsp;
                <span>{{ user?.datos_personales?.motor }}</span>
              </li>
              <li>
                <b>Chasis</b>&nbsp;
                <span>{{ user?.datos_personales?.chasis }}</span>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>
<script setup lang="ts">
import QRCode from "qrcode";
import { jsPDF } from 'jspdf';
import { onMounted } from "vue";
import { POSITION, useToast } from "vue-toastification";
import type { User } from "~/common/interfaces/user.interface";
import { useAuthStore } from "~~/store/auth";
definePageMeta({
  name: "ResumenPage",
  layout: "private",

});
const {
  public: { baseURL },
} = useRuntimeConfig();

const getBase64Image = async (imageUrl) => {
  const response = await fetch(imageUrl);
  const blob = await response.blob();
  return new Promise((resolve, reject) => {
    const reader = new FileReader();
    reader.onloadend = () => resolve(reader.result.split(",")[1]);
    reader.onerror = reject;
    reader.readAsDataURL(blob);
  });
};

const qrcode = ref(null);
const pdfInfo = ref("");

const generatePDF = async () => {
  try {
    const pdf = new jsPDF();
    const { width, height } = pdf.internal.pageSize;

    // Load the image from the URL
    const imgData = await fetch(qrcode.value).then((res) => res.blob());
    const imgSrc = URL.createObjectURL(imgData);

    // Add image to PDF
    pdf.addImage(imgSrc, 'JPEG', 20, 20, 50, 50);

    // Add text to PDF
    pdf.text(pdfInfo.value, 20, 90);

    // Save or display the PDF
    pdf.save('document.pdf');
  } catch (error) {
    console.error("Error generating PDF:", error);
    throw error;
  }
};

const generateQRCode = async () => {
  let information = "";

  // let base64Image = "";

  // const imageUrl = "@assets/images/profile.png";

  // if (user.value?.datos_personales?.foto?.url) {
  //   base64Image = await getBase64Image(
  //     `${baseURL}${user.value?.datos_personales?.foto?.url}`
  //   );
  // } else {
  //   base64Image = await getBase64Image(imageUrl);
  // }
  // if (user.value?.datos_personales?.foto?.url)
  //   information += `${base64Image}\n`;
  information += `name: ${user.value?.datos_personales?.nombres} ${user.value?.datos_personales?.apellidos}\n`;

  if (user.value?.datos_personales?.correo)
    information += `Correo: ${user.value?.datos_personales?.correo}\n`;
  if (user.value?.datos_personales?.cedula_ruc)
    information += `Identificación: ${user.value?.datos_personales?.cedula_ruc}\n`;
  if (user.value?.estado) information += `Estado: ${user.value?.estado}\n`;

  // Generate the QR code
  const qrCodeDataUrl = `https://api.qrserver.com/v1/create-qr-code/?data=${encodeURIComponent(
    information
  )}&size=150x150`;
  // const qrCodeDataUrl = await QRCode.toDataURL(information);
  pdfInfo.value = information
  // generatePDF(information, qrCodeDataUrl);

  qrcode.value = qrCodeDataUrl;
};

const authStore = useAuthStore();
const token = authStore.getToken;
const userData = computed(() => {
  return authStore.user;
});

const getProfilePicture = (url: string) => {
  return `${baseURL}${url}`;
};

// Code By Saeed
const isPrint = ref<boolean>(false);


const isBackdrop = ref(true);

// Function to update the property
const closeBackdrop = () => {
  isBackdrop.value = false;
};

const showBackDrop = computed(() => {
  const userObject = user?.value?.datos_personales;
  if (userObject) {
    generateQRCode();
    if (
      !userObject?.fecha_inicio ||
      !userObject?.fecha_fin ||
      !userObject?.tipo_persona ||
      !userObject?.tipo_tarjeta ||
      !userObject?.plan ||
      !userObject?.poliza ||
      !userObject?.certificado ||
      !userObject?.marca ||
      !userObject?.modelo ||
      !userObject?.anio ||
      !userObject?.color ||
      !userObject?.placa ||
      !userObject?.motor ||
      !userObject?.chasis
    ) {
      return true;
    }
  } else {
    return false;
  }
});



// Code By Saeed

const { data: personal } = useFetch<User>(`${baseURL}/users/${userData.value?.id}?populate[0]=datos_personales`, {
  method: "GET",
  headers: {
    "Content-Type": "application/json",
    Authorization: `Bearer ${token}`,
  },
});

const { data: user } = useFetch<User>(`${baseURL}/users/${userData.value?.id}`, {
  method: "GET",
  headers: {
    "Content-Type": "application/json",
    Authorization: `Bearer ${token}`,
  },
});

const {data: configData } = useFetch<any[]>(`${baseURL}/config-pagos`, {
  method: "GET",
  headers: {
    "Content-Type": "application/json",
    Authorization: `Bearer ${token}`,
  },
});
//const taxes:any = userTaxes.value?.find((t:any)=> t.user === authStore.user?.id);
// if(configData) console.log(configData);

const configToGet: any = configData.value?.find((d: any) => d.user && authStore.user && d.user.id === authStore.user.id);

if (configToGet) {
  console.log(configToGet);

  const { data: taxes } = useFetch(`${baseURL}/config-pagos/${configToGet.id}`, {
    method: "GET",
    headers: {
      "Content-Type": "application/json",
      Authorization: `Bearer ${token}`,
    },
  });
} 


const { data: total } = useFetch(`${baseURL}/pagos/${userData?.value?.datos_personales}`, {
  method: "GET",
  headers: {
    "Content-Type": "application/json",
    Authorization: `Bearer ${token}`,
  },
});



// Code By Saeed
const updateDatosPersonales = () => {};
// Code By Saeed

const payment = computed(() => total.value);


const printPage = () => {
  if (typeof window === 'undefined') return;
  window.print()
}

const toast = useToast();

const sendMail = async () => {
  const { data, error } = useFetch(`${baseURL}/resumen/send-email`, {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
      Authorization: `Bearer ${token}`,
    },
  });
  if (error.value) {
    toast.error("Error al enviar el correo", { position: POSITION.BOTTOM_RIGHT });
  }
  console.log(data.value);
  if (data.value) {
    toast.success("Correo enviado, revisa tu bandeja de entrada");
  }



};
const sendDataToIPAddress = (jsonData) => {
  const ipAddress = "http://135.195.2.12.3"; // Replace with your actual IP address
  const url = ipAddress; // Replace 'your-endpoint' with the specific API endpoint you want to send data to

  const requestData = {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
    },
    body: JSON.stringify(jsonData),
  };

  console.log(">>>> json ", jsonData);

  fetch(url, requestData)
    .then((response) => {
      if (!response.ok) {
        throw new Error(`HTTP Error: ${response.status}`);
      }
      return response.json();
    })
    .then((responseData) => {
      console.log("Data sent successfully:", responseData);
    })
    .catch((error) => {
      console.error("Error sending data:", error);
    });
};
</script>
<style scoped>
main {
  padding: 0 1rem 1rem 1rem;
}

header {
  padding: 1rem 0;
  display: flex;
  gap: 1rem;
  border-bottom: 1px solid var(--gray-200);
}

.header__description > h1 {
  font-size: var(--heading-2);
}

.header__description > img {
  width: 56px;
}

.header__text > h1 {
  font-size: var(--heading-2);
}

.header__text {
  gap: 1rem;
  flex-wrap: wrap;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.header__actions {
  flex-wrap: wrap;
  display: flex;
  gap: 1rem;
}

.header__title {
  display: flex;
  gap: 1rem;
  align-items: center;
}

.header__title > img {
  width: 56px;
  height: auto;
}

.socio__name {
  font-size: var(--heading-3);
}

.socio__profile > img {
  width: 72px;
}

.socio__info {
  padding: 1rem 0;
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  gap: 1rem;
}

.socio__saldos,
.socio__profile {
  display: flex;
  gap: 1rem;
}

.socio__saldos {
  flex-wrap: wrap;
  border-radius: 9px;
  background: linear-gradient(180deg, #fbf8ff 85.42%, #0200ab 89.58%);

  box-shadow: 1px 1px 5px 2px rgba(0, 0, 0, 0.05);
}

.socio__profile {
  align-items: start;
}

.socio--activo {
  color: #22c55e;
  font-weight: 600;
}

.socio__saldo {
  position: relative;
  padding: 1rem;
  border: 1px solid var(--gray-200);
  flex: 1;
  white-space: nowrap;
}

.socio__saldo::before {
  content: "";
  top: 0;
  position: absolute;
  left: 0;
  width: 100%;
  display: block;
  height: 1rem;
}

.socio__saldo:nth-child(1):before {
  background-color: #2f1071;
}

.socio__saldo:nth-child(2):before {
  background-color: #2f1071;
}

.socio__saldo:nth-child(3):before {
  background-color: #2f1071;
}

.socio__saldo--positivo {
  color: #6430d0;
}

.socio__saldo--negativo {
  color: #6430d0;
}

.socio__saldo--base {
  color: var(--blue);
}

.socio__saldo > span {
  font-size: var(--heading-3);
  font-weight: 800;
}

.cards__container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(min(100%, 520px), 1fr));
  gap: 1rem;
}

.card {
  border: 1px solid var(--gray-200);
}

.card > h3 {
  background-color: var(--gray-200);
  padding: 1rem;
}

.card__list {
  padding: 1rem;
  font-size: 1rem;
}

@media (max-width: 1060px) {
  .button > img {
    width: 1.5rem;
  }
}

@media (max-width: 1060px) {
  .header__title > img {
    width: 40px;
    height: auto;
  }
}

.header__photo {
  width: 3rem;
  height: auto;
  border-radius: 50%;
}

/* Code By Saeed Below this line */

.socio__print_info {
  width: 50%;
}

.socio_print_info_item {
  display: flex;
  justify-content: space-between;
}

.socio_print_info_item h4 {
  width: 65%;
  display: flex;
  justify-content: flex-end;
}

.socio_print_info_item p {
  width: 35%;
  display: flex;
  justify-content: flex-end;
}

.backdrop {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5); /* Semi-transparent black background */
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000; /* Ensure it appears above other content */
}

/* Styling for the message box */
.message-box {
  background-color: #fff;
  padding: 60px;
  border-radius: 5px;
  text-align: center;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
}
.outer {
  position: relative;
  margin: auto;
  width: 70px;
  margin-top: 20px;
  cursor: pointer;
}

.inner {
  width: 50px;
  text-align: center;
}

label {
  font-size: 0.8em;
  line-height: 4em;
  text-transform: uppercase;
  /* color: #fff; */
  transition: all 0.3s ease-in;
  opacity: 0;
  cursor: pointer;
}

.inner:before,
.inner:after {
  position: absolute;
  content: "";
  height: 1px;
  width: inherit;
  background: #ffc107;
  left: 0;
  transition: all 0.3s ease-in;
}

.inner:before {
  top: 50%;
  transform: rotate(45deg);
}

.inner:after {
  bottom: 50%;
  transform: rotate(-45deg);
}

.outer:hover label {
  opacity: 1;
}

.outer:hover .inner:before,
.outer:hover .inner:after {
  transform: rotate(0);
}

.outer:hover .inner:before {
  top: 0;
}

.outer:hover .inner:after {
  bottom: 0;
}
</style>
