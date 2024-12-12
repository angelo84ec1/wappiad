<template>
  <main>
    <header>
      <div class="header__text">
        <div class="header__description">
          <h1>Establecimientos</h1>
        
        </div>
  
      </div>

      <div class="buttons">
        <button class="button button--secondary" @click.prevent="printPage()">
          <img src="~/assets/images/imprimir-green.png" alt="" srcset="" />
          Imprimir
        </button>
        <button
          class="button"
          :class="{
            'button--primary': usersChecked.length,
            'button--disabled': !usersChecked.length,
          }"
          @click="sendMail"
          :disabled="!usersChecked.length"
        >
          <img
            v-if="usersChecked.length"
            src="~/assets/images/notification-white.png"
            alt="mail-icon"
          />
          <img v-else src="~/assets/images/notification-gray.png" alt="mail-icon" />
          <span
            style="font-weight: 600; font-style: bold; font-size: 16px; line-height: 24px"
            >Enviar notificación</span
          >
        </button>
        <!--        <button class="button button&#45;&#45;secondary" @click="sendMail()">-->
        <!--          <img src="~/assets/images/email-green.png" alt="">Enviar estado por-->
        <!--          email-->
        <!--        </button>-->
        <button class="button button--primary" @click="goToCreate">
          <svg
            width="24"
            height="24"
            viewBox="0 0 24 24"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              d="M12 4.5V19.5M19.5 12H4.5"
              stroke="#FAFAFA"
              stroke-width="2"
              stroke-linecap="round"
              stroke-linejoin="round"
            />
          </svg>
          Agregar socio
        </button>
      </div>
    </header>


  </main>
</template>

<script setup lang="ts">
import { stringify } from "qs";
import { Dictionary } from "ts-essentials";
import { POSITION, useToast } from "vue-toastification";
import type { DatosPersonales, User } from "~/common/interfaces/user.interface";
import { useAuthStore } from "~~/store/auth";
import bottomPagination from "~~/components/common/pagination/bottom-pagination.vue";

definePageMeta({
  name: "SociosPage",
  layout: "private",
});
const {
  public: { baseURL },
} = useRuntimeConfig();
const toast = useToast();
const BASE_URL = baseURL;
const authStore = useAuthStore();
const filters = ref<Dictionary<string>>({});
const filterKey = ref("");
const filterValue = ref("");

const addFilter = () => {
  filters.value[filterKey.value] = filterValue.value;
  filterKey.value = "";
  filterValue.value = "";
  buildQuery();
  fetchData();
};

const removeFilter = (key: string) => {
  delete filters.value[key];
  filterKey.value = "";
  filterValue.value = "";
  limit.value = 10; // Added By Saeed
  buildQuery();
  fetchData();
};
const numberFields: { [key: string]: boolean } = {
  cedula: true,
};
const query = ref("");
const buildQuery = () => {
  const data: { [key: string]: string } = {};
  data._start = start.value.toString();
  data._limit = limit.value.toString();
  let i = 0;
  for (const key in filters.value) {
    if (numberFields[key]) {
      data[`_where[${i}][${key}]`] = filters.value[key];
      i++;
      continue;
    }
    data[`_where[${i}][${key}_contains]`] = filters.value[key];
    i++;
  }
  query.value = stringify(data);
};

const datos = ref<DatosPersonales[] | null>(null);
const totalData = ref<number | null>(null);
const limit = ref<number>(10);
const start = ref<number>(0);
const page = ref<number>(1);
const printData = ref<boolean>(false);
const usersChecked = ref<string[]>([]);

const changeLimit = (newLimit: number) => {
  limit.value = Number(newLimit);
  start.value = 0;
  page.value = 1;
  fetchData();
};

watch([start, limit], () => {
  fetchData();
});

const prevPage = () => {
  if (start.value < 0) start.value = 0;
  if (page.value <= 1) return;
  start.value = Number(start.value) - Number(limit.value);
  page.value = Number(page.value) - 1;
  fetchData();
};

const nextPage = () => {
  start.value = Number(limit.value) + Number(start.value);
  page.value = Number(page.value) + 1;
  fetchData();
};

const goToPage = (pageNumber: number) => {
  start.value = (Number(pageNumber) - 1) * Number(limit.value);
  page.value = Number(pageNumber);
  fetchData();
};

const fetchData = async () => {
  buildQuery();
  const { data: dataDatos } = useFetch<DatosPersonales[]>(
    `${BASE_URL}/datos-personales?${query.value}`,
    {
      method: "GET",
      headers: {
        "Content-Type": "application/json",
        Authorization: "Bearer " + authStore.token,
      },
    }
  );
  const { data: totalDatos } = useFetch<number>(`${BASE_URL}/datos-personales/count`, {
    method: "GET",
    headers: {
      "Content-Type": "application/json",
      Authorization: "Bearer " + authStore.token,
    },
  });

  watch(dataDatos, (newData) => {
    datos.value = newData;
    if (datos.value?.length < limit.value) {
      // added by Saeed
      limit.value = datos.value?.length; // added by Saeed
    } // added by Saeed
    console.log(datos);
  });

  watch(totalDatos, (newData) => {
    totalData.value = newData;
    if (totalData.value?.length < limit.value) {
      // added by Saeed
      limit.value = totalData.value?.length; // added by Saeed
    } // added by Saeed
    console.log(totalData);
  });
};

const router = useRouter();

const goToCreate = async () => {
  await router.push("/socios/crear");
};

// Added code by Saeed
const printPage = () => {
  if (typeof window === "undefined") return;
  window.print();
};


const goToUploadDocuments = () => {
  router.push("/socios/subir-documentos");
};

const checkboxHandler = (e: Event, userId: string) => {
  if (e.currentTarget?.checked) {
    usersChecked.value.push(userId);
    console.log(usersChecked.value);
  } else {
    usersChecked.value = usersChecked.value.filter((id) => id !== userId);
  }
};

const sendMail = async () => {
  const filteredUsers = datos?.value.map((data) => data.id);
  router.push({ path: "/socios/enviar", query: { users: usersChecked.value.join(",") } });
};

// Added code by Saeed

const goToEdit = async (id: string) => {
  await router.push("/socios/" + id);
};

const deleteUser = async (id: string) => {
  const { data: user } = await useFetch<User[]>(
    `${BASE_URL}/users?_datos_personales=${id}`,
    {
      method: "GET",
      headers: {
        "Content-Type": "application/json",
        Authorization: "Bearer " + authStore.token,
      },
    }
  );
  const { data: datosDeleted, error: errorDatosDeleted } = await useFetch(
    `${BASE_URL}/datos-personales/` + id,
    {
      method: "DELETE",
      headers: {
        "Content-Type": "application/json",
        Authorization: "Bearer " + authStore.token,
      },
    }
  );
  if (errorDatosDeleted.value) {
    console.log(errorDatosDeleted.value);
    toast.error("Error al eliminar el socio");
    return;
  }
  if (user.value?.length && datosDeleted.value) {
    const { data: userDeleted, error: errorUserDeleted } = await useFetch(
      `${BASE_URL}/users/` + user.value[0].id
    );
    if (errorUserDeleted.value) {
      console.log(errorUserDeleted.value);
      toast.error("Error al eliminar el socio");
      return;
    }
    if (userDeleted.value) {
      toast.success("Socio eliminado correctamente");
    }
  }
  datos.value?.splice(
    datos.value?.findIndex((user) => user.id === id),
    1
  );
};

onBeforeMount(() => {
  if (!authStore.user?.role.type.includes("admin")) {
    router.push("/personal");
    toast.error('Disculpas, usted no esta autorizado en visitar "socios" page');
  }
});

onMounted(async () => {
  await fetchData();
});

const goToSendNotification = (id: string) => {
  router.push({ path: "/socios/enviar", query: { users: id } });
};
const getProfilePicture = (url: string) => `${BASE_URL}${url}`;

// Added by Junaid
//const { data } = await useFetch<any[]>(`${BASE_URL}/pagos`, {
//method: "GET",
//headers: {
//"Content-Type": "application/json",
//Authorization: `Bearer ${authStore.getToken}`,
//},
//});
//const taxes = {
// amount: "",
//};

//if (data.value !== null) {
//console.log("amount is", data.value[0].amount);
//taxes.amount = data.value[0].amount;
//}
</script>

<style scoped>
main {
  padding: 0 1rem 1rem 1rem;
}

header {
  padding: 1rem 0;
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
  gap: 1rem;
  align-items: center;
  border-bottom: 1px solid var(--gray-200);
}

.header__description > h1 {
  font-size: var(--heading-2);
}

.header__description > img {
  width: 56px;
}

.header__text {
  flex-direction: column;
  gap: 1rem;
  flex-wrap: wrap;
  display: flex;
}

.header__description {
  display: flex;
  gap: 1rem;
  align-items: center;
}

.quote {
  max-width: 550px;
}

.filters__area {
  display: flex;
  justify-content: space-between;
}

.filters__group {
  padding: 1rem 0;
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
  align-items: flex-end;
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

.button__group > button {
  padding: 0.25rem;
  display: grid;
  place-items: center;
  background-color: transparent;
}

.button__group > button > svg {
  width: 1.5rem;
}

.button__group > button > svg > path {
  stroke: var(--gray-700);
}

.button__group > button > svg > path {
  transition: color 250ms ease-in-out;
}

.button__group > button:hover > svg > path {
  stroke: var(--green-500);
}

.button__group {
  display: flex;
  gap: 0.25rem;
}

table {
  width: 100%;
  border-spacing: 0;
  border-collapse: collapse;
  text-align: start;
  vertical-align: middle;
  table-layout: fixed;
  overflow-x: hidden;
  word-break: break-word;
}

.width--sm {
  width: 10%;
}

.width--md {
  width: 12%;
}

.width--lg {
  width: 30%;
}

td {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}

th,
td {
  padding: 0.5rem;
}

.table__header {
  text-align: left;
  background-color: var(--gray-50);
  border-bottom: 1px solid var(--gray-200);
}

.socio__photo {
  width: 48px;
  height: auto;
  border-radius: 50%;
}

@media (max-width: 1260px) {
  .button > img {
    width: 1.5rem;
  }
}

@media (max-width: 920px) {
  .header__description > img {
    width: 40px;
    height: auto;
  }

  /* Force table to not be like tables anymore */
  table,
  thead,
  tbody,
  th,
  td,
  tr {
    display: block;
  }

  /* Hide table headers (but not display: none;, for accessibility) */
  thead tr {
    position: absolute;
    top: -9999px;
    left: -9999px;
  }

  td {
    /* Behave  like a "row" */
    white-space: normal;
    border: none;
    border-bottom: 1px solid #eee;
    position: relative;
    padding-left: 35%;
  }

  td:before {
    /* Now like a table header */
    position: absolute;
    /* Top/left values mimic padding */
    top: 50%;
    left: 1rem;
    width: 25%;
    transform: translateY(-50%);
    padding-right: 10px;
    white-space: nowrap;
    font-weight: 700;
  }

  /*
	Label the data
	*/
  .checkbox-wrapper{
    padding: .5rem 0;
  }

  td:nth-of-type(1):before {
    content: "";
  }
  td:nth-of-type(2):before {
    content: "Foto";
  }

  td:nth-of-type(3):before {
    content: "Nombre";
  }

  td:nth-of-type(4):before {
    content: "Email";
  }

  td:nth-of-type(5):before {
    content: "Contrato 1";
  }

  td:nth-of-type(6):before {
    content: "Depositos";
  }

  td:nth-of-type(7):before {
    content: "Saldos";
  }

  td:nth-of-type(8):before {
    content: "Acción";
  }

  .highlight {
    background-color: var(--gray-200);
  }

  .margin-botton {
    margin-bottom: 1rem;
  }
}

@media (max-width: 430px) {
  .button__group > button > svg {
    width: 1rem;
  }
}

@media (min-width: 1500px) {
  .width--md {
    width: 14%;
  }
}

/* CHIP CSS */
.chip {
  /* Center the content */
  align-items: center;
  display: inline-flex;
  justify-content: center;

  /* Background color */
  background-color: #d1d5db;

  /* Rounded border */
  border-radius: 9999px;

  /* Spacing */
  padding: 0.25rem 0.5rem;
}

.chip__content {
  margin-right: 0.25rem;
}

.chip__button {
  /* Reset */
  background-color: transparent;
  border-color: transparent;

  /* Cursor */
  cursor: pointer;

  /* Size */
  height: 1rem;
  width: 1rem;

  /* Used to position the inner */
  position: relative;
}

.chip__button-line {
  /* Background color */
  background-color: #9ca3af;

  /* Position */
  position: absolute;

  /* Size */
  height: 1px;
  width: 100%;
}

.chip__button-line--first {
  /* Position */
  left: 0px;
  top: 50%;
  transform: translate(0%, -50%) rotate(45deg);

  /* Size */
  height: 1px;
  width: 100%;
}

.chip__button-line--second {
  /* Position */
  left: 50%;
  top: 0px;
  transform: translate(-50%, 0%) rotate(45deg);

  /* Size */
  height: 100%;
  width: 1px;
}

#print-section {
}

.checkbox-wrapper {
  display: block;
  position: relative;
  padding-left: 35px;
  margin-bottom: 12px;
  cursor: pointer;
  font-size: 22px;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.checkbox-wrapper input {
  position: absolute;
  opacity: 0;
  cursor: pointer;
  height: 0;
  width: 0;
}

.checkmark {
  position: absolute;
  top: 0;
  left: 0;
  height: 24px;
  width: 24px;
  background: #d9d9d9;
  border-radius: 6px;
}

.checkbox-wrapper:hover input ~ .checkmark {
  background: #0e7a78;
}

.checkbox-wrapper input:checked ~ .checkmark {
  background: #0e7a78;
}

.checkmark:after {
  content: "";
  position: absolute;
  display: none;
}

.checkbox-wrapper input:checked ~ .checkmark:after {
  display: block;
}

.checkbox-wrapper .checkmark:after {
  left: 9px;
  top: 5px;
  width: 5px;
  height: 10px;
  border: solid white;
  border-width: 0 3px 3px 0;
  -webkit-transform: rotate(45deg);
  -ms-transform: rotate(45deg);
  transform: rotate(45deg);
}
</style>
