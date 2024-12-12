<template>
  <main>
    <header>
      <div class="header__text">
        <div class="header__description">
          <h1>Plan Contratado</h1>
          
        </div>
        <div class="header__actions">
          <nuxt-link :to="`/pagos/create`">
         
        </nuxt-link>

        </div>
      </div>
    </header>

    <div class="filters__area">
      <div class="filters__group">
        <label for="">
          Filtrar por:
          <select v-model="filterKey" name="filter">
            <option selected value="">select</option>
            <option value="day">Día</option>
            <option value="month">Mes</option>
            <option value="year">Año</option>
          </select>
        </label>

        <label for="">
          Valor del filtro:
          <input v-model="filterValue" type="text" />
        </label>
        <button class="button button--secondary" @click="applyFilter">
          <svg
            width="24"
            height="24"
            viewBox="0 0 24 24"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              d="M12 4.5V19.5M19.5 12H4.5"
              stroke="#374151"
              stroke-width="2"
              stroke-linecap="round"
              stroke-linejoin="round"
            />
          </svg>
          Agregar filtro
        </button>
      </div>
    </div>
    <div class="mt-4 mb-4">
        <span v-if="filterKey == 'day'" class="mr-4"><span class="font-bold">Day:</span> {{ filterValue }}</span>
        <span v-if="filterKey == 'month'" class="mr-4"><span class="font-bold">Month:</span> {{ filterValue }}</span>
        <span v-if="filterKey == 'year'" class="mr-4"><span class="font-bold">Year:</span> {{ filterValue }}</span>
        <span class="mr-4"><span class="font-bold">Plan Black:</span> {{ planBlack }}</span>
        <span class="mr-4"><span class="font-bold">Plan Gold:</span> {{ planGold }}</span>
        <span class="mr-4"><span class="font-bold">Plan Silver:</span> {{ planSilver }}</span>
        <span class="mr-4"><span class="font-bold">Total:</span> ${{ total }}</span>
    </div>
    <div class="home__content">
      <table v-if="config_pagos">
        <tr class="t_header">
          <th v-for="tableHeader in table_headers" :key="tableHeader.id">{{ tableHeader.name }}</th>
          <th>Action</th>
        </tr>
        <tr v-for="(data,index) in filteredData" :key="data.id">
          <td v-for="tableHeader in table_headers" :key="tableHeader.id"> 
            {{tableHeader.key == "user" ?  data[tableHeader.key] && data[tableHeader.key].username :  data[tableHeader.key] }}
          </td>
          <td>
            <div class="t_actions">
              <nuxt-link :to="`/pagos/${data.id}`">
                <svg data-v-45005775="" width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <path data-v-45005775="" d="M16.862 4.48725L19.5 7.12525M16.862 4.48725L18.549 2.79925C18.9007 2.44757 19.3777 2.25 19.875 2.25C20.3723 2.25 20.8493 2.44757 21.201 2.79925C21.5527 3.15092 21.7502 3.6279 21.7502 4.12525C21.7502 4.62259 21.5527 5.09957 21.201 5.45125L6.832 19.8202C6.30332 20.3486 5.65137 20.737 4.935 20.9502L2.25 21.7502L3.05 19.0652C3.26328 18.3489 3.65163 17.6969 4.18 17.1682L16.863 4.48725H16.862Z" stroke="#374151" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"></path>
                </svg>
              </nuxt-link>
              <button data-v-45005775="" title="Borrar" @click="remove(data.id, index)">
                <svg data-v-45005775="" width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <path data-v-45005775="" d="M14.74 8.99954L14.394 17.9995M9.606 17.9995L9.26 8.99954M19.228 5.78954C19.57 5.84154 19.91 5.89654 20.25 5.95554M19.228 5.79054L18.16 19.6725C18.1164 20.2378 17.8611 20.7657 17.445 21.1508C17.029 21.5359 16.4829 21.7497 15.916 21.7495H8.084C7.5171 21.7497 6.97102 21.5359 6.55498 21.1508C6.13894 20.7657 5.88359 20.2378 5.84 19.6725L4.772 5.78954M19.228 5.78954C18.0739 5.61506 16.9138 5.48264 15.75 5.39254M3.75 5.95454C4.09 5.89554 4.43 5.84054 4.772 5.78954M4.772 5.78954C5.92613 5.61506 7.08623 5.48264 8.25 5.39254M15.75 5.39254V4.47654C15.75 3.29654 14.84 2.31254 13.66 2.27554C12.5536 2.24018 11.4464 2.24018 10.34 2.27554C9.16 2.31254 8.25 3.29754 8.25 4.47654V5.39254M15.75 5.39254C13.2537 5.19962 10.7463 5.19962 8.25 5.39254" stroke="#374151" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"></path>
                </svg>
              </button>
            </div>
          </td>
        </tr>
      </table>
    </div>
  </main>
</template>
<script setup lang="ts">
import { POSITION, useToast } from "vue-toastification";
import { useAuthStore } from "~~/store/auth";
import { ref, onMounted, onBeforeMount } from 'vue'


definePageMeta({
  name: "PagosPage",
  layout: "private",
  middleware: ["auth"],
});
const toast = useToast();
const router = useRouter();
const route = useRoute();

const authStore = useAuthStore();
const config_pagos = ref<any>(null);
const table_headers = ref([
  {
    id: 1,
    name: "Fecha de Compra",
    key: "fecha_compra",
  },
  {
    id: 2,
    name: "Producto",
    key: "producto",
  },
  {
    id: 5,
    name: "Username",
    key: "user"
  },
  {
    id: 3,
    name: "Total",
    key: "total",
  },
  {
    id: 4,
    name: "Descuento",
    key: "descuento",
  }
]);

const {
  public: { baseURL },
} = useRuntimeConfig();

// fetch config-pagos data
const fetchData = async () => {
  const { data } = await useFetch<any[]>(`${baseURL}/config-pagos`, {
    method: "GET",
    headers: {
      "Content-Type": "application/json",
      Authorization: `Bearer ${authStore.getToken}`,
    },
  });
  if (data) config_pagos.value = data.value
  console.log(">>>> data ", data.value);
  applyFilter()
}


onMounted(() => {
  // console.log(app.$notify)

});
fetchData();

//delete a config_pagos
const remove= async (id,index)=> {
  const { data } = await useFetch<any[]>(`${baseURL}/config-pagos/${id}`, {
    method: "DELETE",
    headers: {
      "Content-Type": "application/json",
      Authorization: `Bearer ${authStore.getToken}`,
    },
  });
  if (data) config_pagos.value.splice(index, 1);
}

const filterKey = ref("");
const filterValue = ref("");
const filteredData = ref([]);
const planBlack = ref(0);
const planSilver = ref(0);
const planGold = ref(0);
const total = ref(0);

const applyFilter = () => {

  filteredData.value = [];
  planBlack.value = 0
  planSilver.value = 0
  planGold.value = 0
  total.value = 0

  console.log(">>>>> ", config_pagos.value);
  

  if (filterKey.value === 'day') {
    filteredData.value = config_pagos.value.filter((item) => {
      const date = new Date(item.fecha_compra);
      return date.getDate() === Number(filterValue.value);
    });
    filteredData.value.forEach(f_d => {
      if (f_d.producto == "Plan Gold") {
        planGold.value += 1
      } else if (f_d.producto == "Plan Black") {
        planBlack.value += 1
      } else if (f_d.producto == "Plan Silver") {
        planSilver.value += 1
      }
      total.value += f_d.total
    })
  } else if (filterKey.value === 'month') {
    filteredData.value = config_pagos.value.filter((item) => {
      const date = new Date(item.fecha_compra);
      return date.getMonth() + 1 === Number(filterValue.value);
    });
    filteredData.value.forEach(f_d => {
      if (f_d.producto == "Plan Gold") {
        planGold.value += 1
      } else if (f_d.producto == "Plan Black") {
        planBlack.value += 1
      } else if (f_d.producto == "Plan Silver") {
        planSilver.value += 1
      }
      total.value += f_d.total
    })
  } else if (filterKey.value === 'year') {
    filteredData.value = config_pagos.value.filter((item) => {
      const date = new Date(item.fecha_compra);
      return date.getFullYear() === Number(filterValue.value);
    });
    filteredData.value.forEach(f_d => {
      if (f_d.producto == "Plan Gold") {
        planGold.value += 1
      } else if (f_d.producto == "Plan Black") {
        planBlack.value += 1
      } else if (f_d.producto == "Plan Silver") {
        planSilver.value += 1
      }
      total.value += f_d.total
    })
  } else {
    filteredData.value = config_pagos.value
    filteredData.value.forEach(f_d => {
      if (f_d.producto == "Plan Gold") {
        planGold.value += 1
      } else if (f_d.producto == "Plan Black") {
        planBlack.value += 1
      } else if (f_d.producto == "Plan Silver") {
        planSilver.value += 1
      }
      total.value += f_d.total
    })
  }
  console.log(filteredData.value);
  
};

// Code by Saeed
// console.log(data);
</script>
<style scoped>
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


main {
  padding: 0 1rem 1rem 1rem;
}

.header__text>h1 {
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


.float {
display: flex;
align-items: center;
background-color: var(--green-400);
color:#ffffff;
}
.float span {
  display: flex;
  align-items: center;
  justify-content:center;
}

table {
  width: 100%;
  border-collapse: collapse;
}

table tr th {
  text-align: left;
}

tr th,
tr td {
  padding-left: .5rem;
}

tr td {
  padding: .5rem 0.5rem;
}

.t_header {
  background-color: #e7e7e7;
}

.t_actions button {
  background-color: #ffffff;
  padding: 0 0.4rem
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
</style>
