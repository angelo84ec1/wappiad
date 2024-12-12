<template>
  <main style="background-color: #f1f8f8">
    <header>
      <div class="header__text">
        <div class="header__title">
          <h1>Pagos</h1>
          <img src="~/assets/images/carga-documentos.png"
            alt="" />
        </div>
        <div class="header__actions">
          <button class="button button--secondary float"
            @click.prevent="savePaymentConfig">
            <img src="~/assets/images/save-green.png"
              alt="" /> Guardar
          </button>
        </div>
      </div>
    </header>
    <div class="home__content">
      <form class="form">
        <div class="form__group">
          <div class="two-columns">
            <h2 class="full-column margin-top-sm">
              Seleccione el ID del socio
            </h2>

            <BaseSelect v-model="taxes.user"
              label="User"
              :options="users"
              :disabled="false" />



            <h2 class="full-column margin-top-sm">Cuenta 1</h2>
            <!-- <BaseInput
              v-model="taxes.aprobacion_pago1"
              label="Aprobación Pago"
              type="text"
              :disabled="true"
            /> -->
            <BaseSelect v-model="taxes.aprobacion_pago1"
              label="Aprobación Pago1"
              :options="aprobacion_pagos1" />

            <BaseSelect v-model="taxes.tipo_cuenta"
              label="Tipo Cuenta 1"
              :options="tipo_cuentas" />
            <!-- <BaseInput
              v-model="taxes.Tipo_cuenta"
              label="Tipo de Cuenta"
              type="text"
              :disabled="true"
            /> -->
            <BaseInput v-model="taxes.numero_cuenta_pago1"
              label="Número de Cuenta 1"
              type="text"
              :disabled="false" />
            <!--<BaseInput
              v-model="taxes.Banco_cooperativa"
              label="Banco Cooperativa"
              type="text"
              :disabled="true"
            /> -->

            <BaseSelect v-model="taxes.banco_cooperativa"
              label="Banco/Cooperativa"
              :options="banco_cooperativas" />
            <h2 class="full-column margin-top-sm">Cuenta 2</h2>
            <!-- <BaseInput
              v-model="taxes.aprobacion_pago2"
              label="Aprobación Pago 2"
              type="text"
              :disabled="false"
            /> -->

            <BaseSelect v-model="taxes.aprobacion_pago2"
              label="Aprobación Pago2"
              :options="aprobacion_pagos2" />

            <!-- <BaseInput
              v-model="taxes.numero_cuenta_pago2"
              label="Tipo de Cuenta 2"
              type="text"
              :disabled="false"
            />  -->

            <BaseSelect v-model="taxes.tipo_cuenta2"
              label="Tipo Cuenta 2"
              :options="tipo_cuentas2" />
            <BaseInput v-model="taxes.numero_cuenta_pago2"
              label="Número de Cuenta 2"
              type="text"
              :disabled="false" />

            <BaseSelect v-model="taxes.banco_cooperativa2"
              label="Banco/Cooperativa 2"
              :options="banco_cooperativas2" />
            <!-- <BaseInput
              v-model="taxes.Banco_cooperativa2"
              label="Banco Cooperativa 2"
              type="text"
              :disabled="true"
            /> -->
            <h2 class="full-column margin-top-sm">Cuenta 3</h2>
            <!--<BaseInput
              v-model="taxes.aprobacion_pago3"
              label="Aprobación Pago 3"
              type="text"
              :disabled="false"
            /> -->
            <BaseSelect v-model="taxes.aprobacion_pago3"
              label="Aprobación Pago3"
              :options="aprobacion_pagos3" />
            <BaseSelect v-model="taxes.tipo_cuenta3"
              label="Tipo Cuenta 3"
              :options="tipo_cuentas3" />
            <!-- <BaseInput
              v-model="typeAccount3"
              label="Tipo de Cuenta 3"
              type="text"
              :disabled="true"
            /> -->
            <BaseInput v-model="taxes.numero_cuenta_pago3"
              label="Número de Cuenta 3"
              type="text"
              :disabled="false" />
            <BaseSelect v-model="taxes.banco_cooperativa3"
              label="Banco/Cooperativa 3"
              :options="banco_cooperativas3" />
            <!-- 
            <BaseInput
              v-model="banco_cooperativa3"
              label="Banco Cooperativa 3"
              type="text"
              :disabled="true"
            /> -->
            <h2 class="full-column margin-top-sm">Pago al extranjero</h2>
            <BaseInput v-model="taxes.aba"
              label="ABA"
              type="text"
              placeholder="00000000" />
            <BaseInput v-model="taxes.swift"
              label="SWIFT"
              type="text"
              placeholder="00000000" />
            <BaseSelect v-model="taxes.tipo_pago"
              label="Tipo de pago"
              :options="tipo_pagos" />

            <!-- <BaseSelect v-model="taxes.tipoPago" label="Tipo de pago" /> -->
            <BaseSelect v-model="taxes.moneda_pago"
              label="Moneda Pago"
              :options="moneda_pagos" />
            <BaseSelect v-model="taxes.tipo_cambio"
              label="Tipo Cambio"
              :options="tipo_cambios" />
            <BaseInput v-model="taxes.conversion_divisa"
              label="Conversion de divisa"
              type="text" />
            <BaseSelect v-model="taxes.observacion_pago"
              label="Observación de Pago"
              :options="observacion_pagos" />
            <BaseSelect v-model="taxes.grupo_anticipo"
              label="Grupo Anticipo"
              :options="grupo_anticipos" />
            <!-- <BaseSelect v-model="grupoAnticipo" label="Grupo anticipo" />-->
            <BaseInput v-model="taxes.anticipos"
              label="Anticipos"
              placeholder="$0.00"
              :disabled="false" />

            <BaseInput v-model="taxes.compromiso_total_adeudado"
              label="Compromiso total adeudado"
              placeholder="$0.00"
              :disabled="false" />
            <BaseInput v-model="taxes.fecha_deposito"
              label="Fecha de deposito"
              type="date"
              placeholder="$0.00" />
            <BaseInput v-model="taxes.retencion_iva_ecuador"
              label="Retencion IVA Ecuador"
              type="text"
              placeholder="%" />
            <BaseInput v-model="taxes.retencion_iva_panama"
              label="Retencion IVA Panama"
              type="number"
              placeholder="%" />
            <BaseInput v-model="taxes.retencion_reforestacion"
              label="Retencion reforestacion"
              type="text"
              placeholder="%" />
            <BaseInput v-model="taxes.retencion_seguro_vida"
              label="Retencion seguro de vida"
              type="text"
              placeholder="%" />
            <BaseInput v-model="taxes.retencion_impuesto_renta"
              label="Retencion impuesto a la renta"
              type="text"
              placeholder="%" />
            <BaseInput v-model="taxes.retencion_proyectos"
              label="Retencion a proyectos"
              type="text"
              placeholder="%" />
            <BaseInput v-model="taxes.penalisaciones_sanciones"
              label="Penalisaciones sanciones"
              type="text"
              placeholder="%" />
            <BaseInput v-model="taxes.descuento_viajes_anuales"
              label="Descuento viajes anuales"
              type="text"
              placeholder="%" />
            <BaseInput v-model="taxes.impuesto_anticipado"
              label="Impuesto anticipado"
              type="text"
              placeholder="%" />
            <BaseInput v-model="taxes.retencion_deporte"
              label="Retencion al deporte"
              type="text"
              placeholder="%" />

            <BaseInput v-model="taxes.retencion_fuente"
              label="Retencion de la Fuente"
              type="text"
              placeholder="%" />
            <!-- <BaseInput v-model="taxes.monto_pagar"
              label="Monto a pagar"
              type="text"
              placeholder="$0.00" /> -->
            <BaseInput v-model="taxes.monto_pagar_letras"
              label="Monto a pagar en letras"
              type="text"
              placeholder="$0.00" />
            <BaseInput v-model="taxes.numero_transferencia"
              label="Numero de transferencia"
              type="text" />
            <BaseInput v-model="taxes.cuentas_cobrar"
              label="Cuentas Cobrar"
              type="text" />
            <BaseInput v-model="taxes.total_debitar"
              label="Total a debitar"
              type="text"
              placeholder="$0.00" />
            <BaseInput v-model="taxes.bonos_pagar"
              label="Bonos por pagar"
              type="text"
              placeholder="$0.00" />
            <BaseInput v-model="taxes.saldo_despues_deposito"
              label="Saldo despues del deposito"
              type="text"
              placeholder="$0.00" />
            <BaseInput v-model="taxes.comisiones"
              label="Comisiones"
              type="text"
              placeholder="$0.00" />
            <BaseInput v-model="taxes.comodad_cuotas"
              label="Comodas cuotas"
              type="text"
              placeholder="$0.00" />
            <BaseInput v-model="taxes.pago_prorrateado"
              label="Pago prorrateado"
              type="text"
              placeholder="$0.00" />
            <BaseInput v-model="taxes.transferencia_desde_extranjero"
              label="Transferencia desde el extranjero"
              type="text"
              placeholder="$0.00" />
            <BaseInput v-model="taxes.pago_desde_extranjero"
              label="Pago desde extranjero"
              type="text"
              placeholder="$0.00" />
            <BaseInput v-model="taxes.pago_al_extranjero"
              label="Pago al Extranjero"
              type="text"
              placeholder="$0.00" />

            <BaseInput v-model="taxes.transferencia_al_extranjero"
              label="Transferencia al extranjero"
              type="text"
              placeholder="$0.00" />
            <BaseInput v-model="taxes.valor_cheque"
              label="Valor de cheque"
              type="text"
              placeholder="$0.00" />
            <BaseInput v-model="taxes.cheque_no_cheque"
              label="Cheque(s) Nro cheque"
              type="text" />
            <BaseInput v-model="taxes.porcentaje_cancelaciones"
              label="Porcentaje Cancelaciones"
              type="text" />
          </div>
        </div>
      </form>
    </div>
  </main>
</template>
<script setup lang="ts">
import { useToast } from "vue-toastification";
import BaseInput from "~/components/common/inputs/base-input.vue";


import BaseSelect from "~/components/common/inputs/base-select.vue";
import { useAuthStore } from "~~/store/auth";
import { ref } from "vue";

definePageMeta({
  // name: "PagosPage",
  components: {
    BaseInput,
    BaseSelect,
  },
  layout: "private",
  middleware: ["auth"],
});
const toast = useToast();
const router = useRouter();
const route = useRoute();

const authStore = useAuthStore();

//const authStore = useAuthStore();

//definePageMeta({
//name: "PagosPage",
//components: {
//BaseInput,
//BaseSelect,
//},
//layout: "private",
//middleware: ["auth"],
//});
// const store = useStore()
// const userData = computed(() => {
//   return store.getters.loggedInUser
// })

//const datos = ref<DatosPersonales[] | null>(null);

// const {app} = useContext()

onMounted(() => {
  // // console.log(app.$notify)
});

const {
  public: { baseURL },
} = useRuntimeConfig();

// console.log(route);
const config_pagos = ref<any>(null);

if (route.params.id != "create") {
  const { data } = await useFetch<any[]>(
    `${baseURL}/config-pagos/${route.params.id}`,
    {
      method: "GET",
      headers: {
        "Content-Type": "application/json",
        Authorization: `Bearer ${authStore.getToken}`,
      },
    }
  );
  console.log("????????? ", data.value);

  config_pagos.value = data.value;
  //get selected user
  //   const {data} = await useFetch<any[]>(`${baseURL}/users/`, {
  //   method: "GET",
  //   headers: {
  //     "Content-Type": "application/json",
  //     Authorization: `Bearer ${authStore.getToken}`,
  //   },
  // });
}


const users = ref<any>([]);
const { data } = await useFetch<any[]>(`${baseURL}/users`, {
  method: "GET",
  headers: {
    "Content-Type": "application/json",
    Authorization: `Bearer ${authStore.getToken}`,
  },
});
users.value = data.value;
users.value.map((user: any) => {
  user.text = user.username;
  user.value = user._id;
});
console.log(users.value);



const aprobacion_pagos1 = ref<any>([]);

const getAprobacionPagos = async () => {
  const { data } = await useFetch<any[]>(`${baseURL}/observacion-pagos`, {
    method: "GET",
    headers: {
      "Content-Type": "application/json",
      Authorization: `Bearer ${authStore.getToken}`,
    },
  });
  aprobacion_pagos1.value = data.value;
  aprobacion_pagos1.value.map((aprobacion_pago1: any) => {
    aprobacion_pago1.text = aprobacion_pago1.Nombre;
    aprobacion_pago1.value = aprobacion_pago1._id;
  });
};

const tipo_pagos = ref<any>([]);
const getTipoPago = async () => {
  const { data } = await useFetch<any[]>(`${baseURL}/tipo-pagos`, {
    method: "GET",
    headers: {
      "Content-Type": "application/json",
      Authorization: `Bearer ${authStore.getToken}`,
    },
  });
  tipo_pagos.value = data.value;
  tipo_pagos.value.map((tipo_pago: any) => {
    tipo_pago.text = tipo_pago.TipoPago;
    tipo_pago.value = tipo_pago._id;
  });
};



const moneda_pagos = ref<any>([]);
const getmonedaPago = async () => {
  const { data } = await useFetch<any[]>(`${baseURL}/moneda-pagos`, {
    method: "GET",
    headers: {
      "Content-Type": "application/json",
      Authorization: `Bearer ${authStore.getToken}`,
    },
  });
  moneda_pagos.value = data.value;
  moneda_pagos.value.map((moneda_pago: any) => {
    moneda_pago.text = moneda_pago.Nombre;
    moneda_pago.value = moneda_pago._id;
  });
};


const tipo_cambios = ref<any>([]);
const getTipoCambio = async () => {
  const { data } = await useFetch<any[]>(`${baseURL}/tipo-cambios`, {
    method: "GET",
    headers: {
      "Content-Type": "application/json",
      Authorization: `Bearer ${authStore.getToken}`,
    },
  });
  tipo_cambios.value = data.value;
  tipo_cambios.value.map((tipo_cambio: any) => {
    tipo_cambio.text = tipo_cambio.Nombre;
    tipo_cambio.value = tipo_cambio._id;
  });
};



const grupo_anticipos = ref<any>([]);
const getGrupoAnticipos = async () => {
  const { data } = await useFetch<any[]>(`${baseURL}/grupo-anticipos`, {
    method: "GET",
    headers: {
      "Content-Type": "application/json",
      Authorization: `Bearer ${authStore.getToken}`,
    },
  });
  grupo_anticipos.value = data.value;
  grupo_anticipos.value.map((grupo_anticipo: any) => {
    grupo_anticipo.text = grupo_anticipo.Nombre;
    grupo_anticipo.value = grupo_anticipo._id;
  });
};




const observacion_pagos = ref<any>([]);
const getObservacionPagos = async () => {
  const { data } = await useFetch<any[]>(`${baseURL}/observacion-pagos`, {
    method: "GET",
    headers: {
      "Content-Type": "application/json",
      Authorization: `Bearer ${authStore.getToken}`,
    },
  });
  observacion_pagos.value = data.value;
  observacion_pagos.value.map((observacion_pago: any) => {
    observacion_pago.text = observacion_pago.Nombre;
    observacion_pago.value = observacion_pago._id;
  });
};
const aprobacion_pagos3 = ref<any>([]);
const getAprobacionPagos3 = async () => {
  const { data } = await useFetch<any[]>(`${baseURL}/observacion-pagos`, {
    method: "GET",
    headers: {
      "Content-Type": "application/json",
      Authorization: `Bearer ${authStore.getToken}`,
    },
  });
  aprobacion_pagos3.value = data.value;
  aprobacion_pagos3.value.map((aprobacion_pago3: any) => {
    aprobacion_pago3.text = aprobacion_pago3.Nombre;
    aprobacion_pago3.value = aprobacion_pago3._id;
  });
};

const tipo_cuentas3 = ref<any>([]);
const getTipocuentas3 = async () => {
  const { data } = await useFetch<any[]>(`${baseURL}/tipo-cuentas`, {
    method: "GET",
    headers: {
      "Content-Type": "application/json",
      Authorization: `Bearer ${authStore.getToken}`,
    },
  });
  tipo_cuentas3.value = data.value;
  tipo_cuentas3.value.map((tipo_cuenta3: any) => {
    tipo_cuenta3.text = tipo_cuenta3.Tipo;
    tipo_cuenta3.value = tipo_cuenta3._id;
  });
};

const banco_cooperativas3 = ref<any>([]);
const getBancos3 = async () => {
  const { data } = await useFetch<any[]>(`${baseURL}/bancos`, {
    method: "GET",
    headers: {
      "Content-Type": "application/json",
      Authorization: `Bearer ${authStore.getToken}`,
    },
  });
  banco_cooperativas3.value = data.value;
  banco_cooperativas3.value.map((banco_cooperativa3: any) => {
    banco_cooperativa3.text = banco_cooperativa3.Nombre;
    banco_cooperativa3.value = banco_cooperativa3._id;
  });
};

const tipo_cuentas = ref<any>([]);
const getTipocuentas = async () => {
  const { data } = await useFetch<any[]>(`${baseURL}/tipo-cuentas`, {
    method: "GET",
    headers: {
      "Content-Type": "application/json",
      Authorization: `Bearer ${authStore.getToken}`,
    },
  });
  tipo_cuentas.value = data.value;
  tipo_cuentas.value.map((tipo_cuenta: any) => {
    tipo_cuenta.text = tipo_cuenta.Tipo;
    tipo_cuenta.value = tipo_cuenta._id;
  });
};

const aprobacion_pagos2 = ref<any>([]);
const getAprobacionPagos2 = async () => {
  const { data } = await useFetch<any[]>(`${baseURL}/observacion-pagos`, {
    method: "GET",
    headers: {
      "Content-Type": "application/json",
      Authorization: `Bearer ${authStore.getToken}`,
    },
  });
  aprobacion_pagos2.value = data.value;
  aprobacion_pagos2.value.map((aprobacion_pago2: any) => {
    aprobacion_pago2.text = aprobacion_pago2.Nombre;
    aprobacion_pago2.value = aprobacion_pago2._id;
  });
};

const banco_cooperativas = ref<any>([]);
const getBancos = async () => {
  const { data } = await useFetch<any[]>(`${baseURL}/bancos`, {
    method: "GET",
    headers: {
      "Content-Type": "application/json",
      Authorization: `Bearer ${authStore.getToken}`,
    },
  });
  banco_cooperativas.value = data.value;
  banco_cooperativas.value.map((banco_cooperativa: any) => {
    banco_cooperativa.text = banco_cooperativa.Nombre;
    banco_cooperativa.value = banco_cooperativa._id;
  });
};

const tipo_cuentas2 = ref<any>([]);
const getTipocuentas2 = async () => {
  const { data } = await useFetch<any[]>(`${baseURL}/tipo-cuentas`, {
    method: "GET",
    headers: {
      "Content-Type": "application/json",
      Authorization: `Bearer ${authStore.getToken}`,
    },
  });
  tipo_cuentas2.value = data.value;
  tipo_cuentas2.value.map((tipo_cuenta2: any) => {
    tipo_cuenta2.text = tipo_cuenta2.Tipo;
    tipo_cuenta2.value = tipo_cuenta2._id;
  });
};

const banco_cooperativas2 = ref<any>([]);
const getBancos2 = async () => {
  const { data } = await useFetch<any[]>(`${baseURL}/bancos`, {
    method: "GET",
    headers: {
      "Content-Type": "application/json",
      Authorization: `Bearer ${authStore.getToken}`,
    },
  });
  banco_cooperativas2.value = data.value;
  banco_cooperativas2.value.map((banco_cooperativa2: any) => {
    banco_cooperativa2.text = banco_cooperativa2.Nombre;
    banco_cooperativa2.value = banco_cooperativa2._id;
  });
};


getBancos2();
getTipocuentas2();
getBancos();
getAprobacionPagos2();
getTipocuentas3();
getAprobacionPagos();
getTipoPago();
getmonedaPago();
getTipoCambio();
getGrupoAnticipos();
getObservacionPagos();
getAprobacionPagos3();
getBancos3();
getTipocuentas();

const taxes = {
  aprobacion_pago1: "",
  aprobacion_pago2: "",
  aprobacion_pago3: "",
  numero_cuenta_pago1: "",
  tipo_cuenta: "",
  banco_cooperativa: "",
  fecha_deposito: "",
  banco_cooperativa2: "",
  banco_cooperativa3: "",
  numero_cuenta_pago2: "",
  numero_cuenta_pago3: "",
  aba: "",
  swift: "",
  tipo_pago: "",
  anticipos: "",
  compromiso_total_adeudado: "",
  retencion_iva_ecuador: "",
  retencion_iva_panama: "",
  retencion_reforestacion: "",
  retencion_seguro_vida: "",
  retencion_impuesto_renta: "",
  retencion_proyectos: "",
  penalisaciones_sanciones: "",
  descuento_viajes_anuales: "",
  impuesto_anticipado: "",
  retencion_deporte: "",
  retencion_fuente: "",
  monto_pagar_letras: "",
  numero_transferencia: "",
  cuentas_cobrar: "",
  total_debitar: "",
  bonos_pagar: "",
  saldo_despues_deposito: "",
  comisiones: "",
  comodad_cuotas: "",
  pago_prorrateado: "",
  transferencia_desde_extranjero: "",
  transferencia_al_extranjero: "",
  pago_desde_extranjero: "",
  pago_al_extranjero: "",
  valor_cheque: "",
  cheque_no_cheque: "",
  porcentaje_cancelaciones: "",
  tipo_cuenta2: "",
  tipo_cuenta3: "",
  tipo_cambio: "",
  moneda_pago: "",
  observacion_pago: "",
  grupo_anticipo: "",
  conversion_divisa: "",
  user: "",
};

onBeforeMount(() => {
  if (!authStore.user?.role.type.includes("admin")) {
    router.push("/personal");
    toast.error('Disculpas, usted no esta autorizado en visitar "Pagos" page');
  }
});

// Code by Saeed
const hyphenateNumDeCuenta = (numDeCuenta: string | number) => {
  if (!numDeCuenta) return numDeCuenta;
  if (typeof numDeCuenta === "number") {
    numDeCuenta = numDeCuenta.toString();
  }
  numDeCuenta =
    numDeCuenta.slice(0, numDeCuenta.length - 2) +
    "-" +
    numDeCuenta[numDeCuenta.length - 1];
  if (numDeCuenta.includes("undefined")) return "";
  return numDeCuenta;
};


if (config_pagos.value !== null) {
  // // console.log("pagos1", config_pagos[0].id);
  // // console.log("pagos2", config_pagos[1].id);
  // // console.log("userID", authStore.user?.id);
  // const userData:any = config_pagos.value.find(d => d.user.id === authStore.user?.id);

  const userData: any = config_pagos.value;
  watchEffect(() => {
    // Your statement or code block to run whenever 'myRef' value changes
    taxes.aprobacion_pago1 = aprobacion_pagos1.value?.find(
      (aprobacionpago1: any) => aprobacionpago1.text === userData.aprobacion_pago1
    )?.id

    // taxes.aprobacion_pago1 = userData.aprobacion_pago1
    //   ? userData.aprobacion_pago1
    //   : "0";

    taxes.aprobacion_pago2 = aprobacion_pagos2.value?.find(
      (aprobacionpago2: any) => aprobacionpago2.text === userData.aprobacion_pago2
    )?.id

    taxes.aprobacion_pago3 = aprobacion_pagos3.value?.find(
      (aprobacionpago3: any) => aprobacionpago3.text === userData.aprobacion_pago3
    )?.id


    taxes.tipo_cuenta = tipo_cuentas.value?.find(
      (tipo_cuenta: any) => tipo_cuenta.text === userData.tipo_cuenta)?.id

    taxes.banco_cooperativa = banco_cooperativas.value?.find(
      (banco_cooperativa: any) => banco_cooperativa.text === userData.banco_cooperativa)?.id

    //taxes.tipo_cuenta2 = userData.tipo_cuenta2;

    taxes.tipo_cuenta2 = tipo_cuentas2.value?.find(
      (tipo_cuenta2: any) => tipo_cuenta2.text === userData.tipo_cuenta2)?.id

    taxes.banco_cooperativa2 = banco_cooperativas2.value?.find(
      (banco_cooperativa2: any) => banco_cooperativa2.text === userData.banco_cooperativa2)?.id

    //taxes.tipo_cuenta3 = userData.tipo_cuenta3;

    taxes.tipo_cuenta3 = tipo_cuentas3.value?.find(
      (tipo_cuenta3: any) => tipo_cuenta3.text === userData.tipo_cuenta3)?.id


    taxes.banco_cooperativa3 = banco_cooperativas3.value?.find(
      (banco_cooperativa3: any) => banco_cooperativa3.text === userData.banco_cooperativa3)?.id

    taxes.tipo_pago = tipo_pagos.value?.find(
      (tipo_pago: any) => tipo_pago.text === userData.tipo_pago)?.id


    taxes.moneda_pago = moneda_pagos.value?.find(
      (moneda_pago: any) => moneda_pago.text === userData.moneda_pago)?.id


    taxes.tipo_cambio = tipo_cambios.value?.find(
      (tipo_cambio: any) => tipo_cambio.text === userData.tipo_cambio)?.id


    taxes.observacion_pago = observacion_pagos.value?.find(
      (observacion_pago: any) => observacion_pago.text === userData.observacion_pago)?.id


    taxes.grupo_anticipo = grupo_anticipos.value?.find(
      (grupo_anticipo: any) => grupo_anticipo.text === userData.grupo_anticipo)?.id

    taxes.numero_cuenta_pago1 = userData.numero_cuenta_pago1
      ? userData.numero_cuenta_pago1.toString()
      : "0";


    taxes.numero_cuenta_pago2 = userData.numero_cuenta_pago2
      ? userData.numero_cuenta_pago2.toString()
      : "0";
    taxes.numero_cuenta_pago3 = userData.numero_cuenta_pago3
      ? userData.numero_cuenta_pago3.toString()
      : "0";
    taxes.aba = userData.aba;
    taxes.swift = userData.swift;
    taxes.anticipos = userData.anticipos;
    taxes.fecha_deposito = userData.fecha_deposito;
    taxes.retencion_iva_ecuador = userData.retencion_iva_ecuador; // changes by zee
    taxes.retencion_iva_panama = userData.retencion_iva_panama;
    taxes.retencion_reforestacion = userData?.retencion_reforestacion;
    taxes.retencion_seguro_vida = userData.retencion_seguro_vida;
    taxes.retencion_impuesto_renta = userData.retencion_impuesto_renta;
    taxes.retencion_proyectos = userData.retencion_proyectos;
    taxes.penalisaciones_sanciones = userData.penalisaciones_sanciones;
    taxes.descuento_viajes_anuales = userData.descuento_viajes_anuales;
    taxes.impuesto_anticipado = userData.impuesto_anticipado;
    taxes.retencion_deporte = userData.retencion_deporte;
    // taxes.retencion_fuente = userData.retencion_fuente;
    taxes.retencion_fuente = userData.retencion_fuente
      ? userData.retencion_fuente.toString()
      : "0";
    taxes.monto_pagar_letras = userData.monto_pagar_letras;
    taxes.compromiso_total_adeudado = userData.compromiso_total_adeudado;
    // taxes.monto_pagar = userData.monto_pagar;
    taxes.comodad_cuotas = userData.comodad_cuotas;
    taxes.pago_prorrateado = userData.pago_prorrateado;
    taxes.pago_desde_extranjero = userData.pago_desde_extranjero;
    taxes.pago_al_extranjero = userData.pago_al_extranjero;
    taxes.transferencia_desde_extranjero =
      userData.transferencia_desde_extranjero;
    taxes.transferencia_al_extranjero = userData.transferencia_al_extranjero;
    taxes.numero_transferencia = userData.numero_transferencia;
    taxes.cuentas_cobrar = userData.cuentas_cobrar;
    taxes.total_debitar = userData.total_debitar;
    taxes.bonos_pagar = userData.bonos_pagar;
    taxes.saldo_despues_deposito = userData.saldo_despues_deposito;
    taxes.comisiones = userData.comisiones;
    taxes.valor_cheque = userData.valor_cheque;
    taxes.cheque_no_cheque = userData.cheque_no_cheque;
    taxes.porcentaje_cancelaciones = userData.porcentaje_cancelaciones;
    taxes.conversion_divisa = userData.conversion_divisa;
    //taxes.user = userData.user.id;
  });
}

// const savePaymentConfig = async () => {
// 	// changes by zee : there were typos in few of the arrays listed below, i fixed it.

// 	// console.log(">>>> ", tipo_cuentas2.value.find(
// 			(tipo2) => tipo2.id == taxes.tipo_cuenta2
// 		));
// 	return

// 	const saveObject = {
// 		// aprobacion_pago1: aprobacion_pagos1.value.find(
// 		// (aprobacionpago1) => aprobacionpago1.id === taxes.aprobacion_pago1.id
// 		// ),

//     // aprobacion_pago1: taxes.aprobacion_pago1,
// 		aprobacion_pagos1: "Estudio",
// 		// aprobacion_pago2: aprobacion_pagos2.value.find(
// 		// 	(aprobacionpago2) => aprobacionpago2.id === taxes.aprobacion_pago2.id
// 		// ),
// 		// aprobacion_pago2: aprobacion_pagos2.value.find(
// 		// 	(aprobacionpago2) => aprobacionpago2.id === taxes.aprobacion_pago2
// 		// ).text,
// 		aprobacion_pago2: "Estudio",
// 		// aprobacion_pago3: aprobacion_pagos3.value.find(
// 		// 	(aprobacionpago3) => aprobacionpago3.id === taxes.aprobacion_pago3.id
// 		// ),
// 		// aprobacion_pago3: aprobacion_pagos3.value.find(
// 		// 	(aprobacionpago3) => aprobacionpago3.id === taxes.aprobacion_pago3
// 		// ).text,
// 		aprobacion_pago3: "Rechazado",
// 		// Tipo_cuenta: taxes.Tipo_cuenta,
// 		// numero_cuenta_pago1: numeroCuentaPago1,
// 		// banco_cooperativa: banco_cooperativas.value.find(
// 		// 	(banco) => banco.id == taxes.banco_cooperativa
// 		// )?.text,
// 		banco_cooperativa: "Pichincha",
// 		banco_cooperativa2: banco_cooperativas2.value?.find(
// 			(banco2) => banco2.id == taxes.banco_cooperativa2
// 		)?.text,
// 		banco_cooperativa3: banco_cooperativas3.value?.find(
// 			(banco3) => banco3.id == taxes.banco_cooperativa3
// 		)?.text,
// 		//banco_cooperativa3:0,
// 		tipo_cuenta: tipo_cuentas.value?.find(
// 			(cuenta) => cuenta.id === taxes.tipo_cuenta // added .id to taxes.tipo_cuenta
// 		)?.text,
// 		tipo_cuenta2: tipo_cuentas2.value.find(
// 			(tipo2) => tipo2.id == taxes.tipo_cuenta2
// 		).text,
// 		tipo_cuenta3: tipo_cuentas3.value.find(
// 			(tipo3) => tipo3.id == taxes.tipo_cuenta3
// 		).text,
// 		tipo_pago: tipo_pagos.value.find(
// 			(tipoPago1) => tipoPago1.id == taxes.tipo_pago.id
// 		),
// 		moneda_pago: moneda_pagos.value.find(
// 			(MonedaPago1) => MonedaPago1.id == taxes.moneda_pago.id
// 		),
// 		tipo_cambio: tipo_cambios.value.find(
// 			(TipoCambio1) => TipoCambio1.id == taxes.tipo_cambio.id
// 		),
// 		observacion_pago: observacion_pagos.value.find(
// 			(ObservaPago1) => ObservaPago1.id == taxes.observacion_pago.id
// 		),
// 		grupo_anticipo: grupo_anticipos.value.find(
// 			(grupoAnticipo1) => grupoAnticipo1.id == taxes.grupo_anticipo
// 		),
// 		// aprobacion_pago2: taxes.aprobacion_pago2,
// 		// Numero_cuenta_pago2: taxes.Numero_cuenta_pago2,

// 		// aprobacion_pago3: taxes.aprobacion_pago3,
// 		// type_account3: typeAccount3.value,
// 		// account_number3: numeroCuentaPago3,
// 		// bankCooperativa3: bankCooperativa3.value,
// 		Aba: taxes.Aba,
// 		Swift: taxes.Swift,

// 		anticipos: Number(taxes.anticipos) ?? 0,
// 		numero_cuenta_pago1:taxes.numero_cuenta_pago1,
// 		numero_cuenta_pago2: Number(taxes.numero_cuenta_pago2),
// 		numero_cuenta_pago3: Number(taxes.numero_cuenta_pago3),
// 		//moneda_pago: monedaPago.value ? monedaPago.value : "USD",
// 		tipo_cambio: tipo_cambios.value ? tipo_cambios.value?.Nombre : "Dolar",
// 		//observacion_pago: observacionPago.value ? observacionPago.value : "Urgente",
// 		//grupo_anticipo: grupoAnticipo.value,
// 		// anticipos: Number(anticipos.value),
// 		pagoAnticipado: taxes.pagoAnticipado,
// 		compromiso_total_adeudado: Number(taxes.compromiso_total_adeudado) ?? 0,
// 		fecha_deposito: taxes.fecha_deposito?.value, // changes by zee
// 		retencion_iva_ecuador: Number(taxes.retencion_iva_ecuador?.value) ?? 0, // changes by zee
// 		retencion_iva_panama: Number(taxes.retencion_iva_panama?.value) ?? 0, // taxes word was missing (here and below fields)
// 		retencion_reforestacion: Number(taxes?.retencion_reforestacion?.value ? taxes?.retencion_reforestacion?.value : '0') ?? 0,
// 		retencion_seguro_vida: Number(taxes?.retencion_seguro_vida?.value ? taxes.retencion_seguro_vida.value : '0') ?? 0,
// 		retencion_impuesto_renta: Number(taxes.retencion_impuesto_renta.value) ?? 0,
// 		retencion_proyectos: Number(taxes.retencion_proyectos.value) ?? 0,
// 		penalisaciones_sanciones: Number(taxes.penalisaciones_sanciones.value) ?? 0,
// 		descuento_viajes_anuales: Number(taxes.descuento_viajes_anuales.value) ?? 0,
// 		impuesto_anticipado: Number(taxes.impuesto_anticipado.value) ?? 0,
// 		retencion_deporte: Number(taxes.retencion_deporte.value) ?? 0,
//     //retencion_fuente: Number(taxes.retencion_fuente.value) ?? 0,
//     retencion_fuente: Number(taxes.retencion_fuente),
// 		monto_pagar: Number(taxes.monto_pagar?.value) ?? 0,
// 		monto_pagar_letras: Number(taxes.monto_pagar_letras.value) ?? 0,
// 		numero_transferencia: taxes.numero_transferencia.value,
//     numero_cuentas_cobrar: taxes.cuentas_cobrar.value,
// 		total_debitar: Number(taxes.total_debitar.value) ?? 0,
// 		bonos_pagar: Number(taxes.bonos_pagar.value) ?? 0,
// 		saldo_despues_deposito: Number(taxes.saldo_despues_deposito.value) ?? 0,
// 		comisiones: Number(taxes.comisiones.value) ?? 0,
// 		comodad_cuotas: Number(taxes.comodad_cuotas.value) ?? 0,
// 		pago_prorrateado: Number(taxes.pago_prorrateado.value) ?? 0,
// 		pago_desde_extranjero: Number(taxes.pago_desde_extranjero.value) ?? 0,
//     pago_al_extranjero: Number(taxes.pago_al_extranjero.value) ?? 0,
// 		transferencia_desde_extranjero:
// 			Number(taxes.transferencia_desde_extranjero.value) ?? 0,
// 		transferencia_al_extranjero:
// 			Number(taxes.transferencia_al_extranjero.value) ?? 0,
// 		valor_cheque: Number(taxes.valor_cheque.value) ?? 0,
// 		cheque_no_cheque: Number(taxes.cheque_no_cheque.value) ?? 0,
//     porcentaje_cancelaciones: Number(taxes.porcentaje_cancelaciones.value) ?? 0,
// 		conversion_divisa: Number(taxes.conversion_divisa.value) ?? 0, // till here we were missing taxes keyword
// 		user: users.value.find((user) => user.id == taxes.user),
// 	};

// 	const configToUpdate = config_pagos.value;
// 	// // console.log(existingUser);
// 	// console.log("data", saveObject);
// 	if (route.params.id != "create") {
// 		const {data: updatedData, error: updateError} = await useFetch<any[]>(
// 			`${baseURL}/config-pagos/${configToUpdate.id}`,
// 			{
// 				method: "PUT",
// 				headers: {
// 					"Content-Type": "application/json",
// 					Authorization: `Bearer ${authStore.getToken}`,
// 				},
// 				body: JSON.stringify(saveObject),
// 			}
// 		);
// 		// console.log("updated data ::", updatedData);
// 		// console.log(updateError);
// 	} else {
// 		const {data: updatedData, error: updateError} = await useFetch<any[]>(
// 			`${baseURL}/config-pagos`,
// 			{
// 				method: "POST",
// 				headers: {
// 					"Content-Type": "application/json",
// 					Authorization: `Bearer ${authStore.getToken}`,
// 				},
// 				body: JSON.stringify(saveObject),
// 			}
// 		);
// 	}
// };

const savePaymentConfig = async () => {
  // changes by zee : there were typos in few of the arrays listed below, i fixed it.

  // // console.log(">>>>>> ", tipo_cambios.value.find(
  //     (TipoCambio1) => TipoCambio1.id == taxes.tipo_cambio
  //   )?.text);
  // return
  // i want to see console value but no console is showing up
  // does tha depend on the internet browser?
  // console is showing correcly on my local, why it's not showing up on your machine?
  //  give me a minut, i'm fixing this issue in my local machine
  // ok
  // i figured it out. to fix this issue you need to modify your backend
  // and what should be changed?
  // that issue is that backend is taking these input field values in text like, "Urgente" but we need to store their id's
  // i could make a quick fix if you prefer
  // thank you very much for the quick solution. let me check first if it will work or not
  //ok // you can close the connection if you want, i will continue from my side
  // no problem send me the script when you have it please . ok
  // another select module works fine whit the same backend indicated
  const saveObject = {


    aprobacion_pago1: aprobacion_pagos1.value?.find(
      (aprobacionpago1: any) => aprobacionpago1.id === taxes.aprobacion_pago1
    )?.text,
    // aprobacion_pago1: "Estudio",

    // aprobacion_pago1: Number(taxes.aprobacion_pago1),
    // aprobacion_pago2: aprobacion_pagos2.value.find(
    //   (aprobacionpago2) => aprobacionpago2.id === taxes.aprobacion_pago2.id
    // ),
    aprobacion_pago2: aprobacion_pagos2.value?.find(
      (aprobacionpago2: any) => aprobacionpago2.id === taxes.aprobacion_pago2
    )?.text,
    // aprobacion_pago2: "Rechazado",
    aprobacion_pago3: aprobacion_pagos3.value.find(
      (aprobacionpago3: any) => aprobacionpago3.id === taxes.aprobacion_pago3
    )?.text,
    // aprobacion_pago3: "Rechazado",
    // Tipo_cuenta: taxes.Tipo_cuenta,
    // numero_cuenta_pago1: numeroCuentaPago1,

    banco_cooperativa: banco_cooperativas.value.find(
      (banco: any) => banco.id == taxes.banco_cooperativa
    )?.text,
    // banco_cooperativa: "Pichincha",
    banco_cooperativa2: banco_cooperativas2.value.find(
      (banco2: any) => banco2.id == taxes.banco_cooperativa2
    )?.text,
    banco_cooperativa3: banco_cooperativas3.value.find(
      (banco3: any) => banco3.id == taxes.banco_cooperativa3
    )?.text,
    //banco_cooperativa3:0,
    tipo_cuenta: tipo_cuentas.value?.find(
      (cuenta: any) => cuenta.id == taxes.tipo_cuenta // added .id to taxes.tipo_cuenta
    )?.text,
    tipo_cuenta2: tipo_cuentas2.value?.find(
      (tipo2: any) => tipo2.id == taxes.tipo_cuenta2
    )?.text,
    tipo_cuenta3: tipo_cuentas3.value.find(
      (tipo3: any) => tipo3.id == taxes.tipo_cuenta3
    )?.text,
    tipo_pago: tipo_pagos.value.find(
      (tipoPago1: any) => tipoPago1.id == taxes.tipo_pago
    )?.text,
    moneda_pago: moneda_pagos.value.find(
      (MonedaPago1: any) => MonedaPago1.id == taxes.moneda_pago
    )?.text,
    tipo_cambio: tipo_cambios.value.find(
      (TipoCambio1: any) => TipoCambio1.id == taxes.tipo_cambio
    )?.text,
    // tipo_cambio: "Dolar",
    observacion_pago: observacion_pagos.value.find(
      (ObservaPago1: any) => ObservaPago1.id == taxes.observacion_pago
    )?.text,
    // observacion_pago: "Urgente",
    grupo_anticipo: grupo_anticipos.value.find(
      (grupoAnticipo1: any) => grupoAnticipo1.id == taxes.grupo_anticipo
    )?.text,
    // aprobacion_pago2: taxes.aprobacion_pago2,
    // Numero_cuenta_pago2: taxes.Numero_cuenta_pago2,

    // aprobacion_pago3: taxes.aprobacion_pago3,
    // type_account3: typeAccount3.value,
    // account_number3: numeroCuentaPago3,
    // bankCooperativa3: bankCooperativa3.value,
    aba: taxes.aba,
    swift: taxes.swift,

    anticipos: taxes.anticipos ? Number(taxes.anticipos) ? Number(taxes.anticipos) : 0 : 0,
    numero_cuenta_pago1: Number(taxes.numero_cuenta_pago1),
    numero_cuenta_pago2: Number(taxes.numero_cuenta_pago2),
    numero_cuenta_pago3: Number(taxes.numero_cuenta_pago3),
    //moneda_pago: monedaPago.value ? monedaPago.value : "USD",
    // tipo_cambio: tipo_cambios.value ? tipo_cambios.value?.Nombre : "Dolar",
    //observacion_pago: observacionPago.value ? observacionPago.value : "Urgente",
    //grupo_anticipo: grupoAnticipo.value,
    // anticipos: Number(anticipos.value),
    // pagoAnticipado: taxes.pagoAnticipado,
    compromiso_total_adeudado: taxes.compromiso_total_adeudado ? Number(taxes.compromiso_total_adeudado) ? Number(taxes.compromiso_total_adeudado) : 0 : 0,
    fecha_deposito: taxes.fecha_deposito, // changes by zee
    retencion_iva_ecuador: Number(taxes.retencion_iva_ecuador) ? Number(taxes.retencion_iva_ecuador) : 0, // changes by zee
    retencion_iva_panama: Number(taxes.retencion_iva_panama) ? Number(taxes.retencion_iva_panama) : 0, // taxes word was missing (here and below fields)

    retencion_reforestacion: Number(taxes.retencion_reforestacion) ? Number(taxes.retencion_reforestacion) : 0,
    retencion_seguro_vida: Number(taxes.retencion_seguro_vida) ? Number(taxes.retencion_seguro_vida) : 0,

    retencion_impuesto_renta: Number(taxes.retencion_impuesto_renta) ? Number(taxes.retencion_impuesto_renta) : 0,
    retencion_proyectos: Number(taxes.retencion_proyectos) ? Number(taxes.retencion_proyectos) : 0,
    penalisaciones_sanciones: Number(taxes.penalisaciones_sanciones) ? Number(taxes.penalisaciones_sanciones) : 0,
    descuento_viajes_anuales: Number(taxes.descuento_viajes_anuales) ? Number(taxes.descuento_viajes_anuales) : 0,
    impuesto_anticipado: Number(taxes.impuesto_anticipado) ? Number(taxes.impuesto_anticipado) : 0,
    retencion_deporte: Number(taxes.retencion_deporte) ?? 0,
    //retencion_fuente: Number(taxes.retencion_fuente.value) ?? 0,
    retencion_fuente: Number(taxes.retencion_fuente) ? Number(taxes.retencion_fuente) : 0,
    // monto_pagar: Number(taxes.monto_pagar) ? Number(taxes.monto_pagar) : 0,
    monto_pagar_letras: Number(taxes.monto_pagar_letras) ? Number(taxes.monto_pagar_letras) : 0,
    numero_transferencia: taxes.numero_transferencia,
    cuentas_cobrar: taxes.cuentas_cobrar,
    total_debitar: Number(taxes.total_debitar) ? Number(taxes.total_debitar) : 0,
    bonos_pagar: Number(taxes.bonos_pagar) ? Number(taxes.bonos_pagar) : 0,
    saldo_despues_deposito: Number(taxes.saldo_despues_deposito) ? Number(taxes.saldo_despues_deposito) : 0,
    comisiones: Number(taxes.comisiones) ? Number(taxes.comisiones) : 0,
    comodad_cuotas: Number(taxes.comodad_cuotas) ? Number(taxes.comodad_cuotas) : 0,
    pago_prorrateado: Number(taxes.pago_prorrateado) ? Number(taxes.pago_prorrateado) : 0,
    pago_desde_extranjero: Number(taxes.pago_desde_extranjero) ? Number(taxes.pago_desde_extranjero) : 0,
    pago_al_extranjero: Number(taxes.pago_al_extranjero) ? Number(taxes.pago_al_extranjero) : 0,
    transferencia_desde_extranjero:
      Number(taxes.transferencia_desde_extranjero) ? Number(taxes.transferencia_desde_extranjero) : 0,
    transferencia_al_extranjero:
      Number(taxes.transferencia_al_extranjero) ? Number(taxes.transferencia_al_extranjero) : 0,
    valor_cheque: Number(taxes.valor_cheque) ? Number(taxes.valor_cheque) : 0,
    cheque_no_cheque: Number(taxes.cheque_no_cheque) ? Number(taxes.cheque_no_cheque) : 0,
    porcentaje_cancelaciones: Number(taxes.porcentaje_cancelaciones) ? Number(taxes.porcentaje_cancelaciones) : 0,
    conversion_divisa: taxes.conversion_divisa, // till here we were missing taxes keyword
    //user: users.value.find((user) => user.id == taxes.user),



  };

  const configToUpdate = config_pagos.value;
  // // console.log(existingUser);
  // console.log("data", saveObject);
  if (route.params.id != "create") {
    const { data: updatedData, error: updateError } = await useFetch<any[]>(
      `${baseURL}/config-pagos/${configToUpdate.id}`,
      {
        method: "PUT",
        headers: {
          "Content-Type": "application/json",
          Authorization: `Bearer ${authStore.getToken}`,
        },
        body: JSON.stringify(saveObject),
      }
    );
    // console.log("updated data ::", updatedData);
    // console.log(updateError);

    if (updateError) {
      // console.log(updateError);
      toast("Información Actualizada");
    } else {
      toast("Error al Actualizar");
    }
  } else {
    const { data: updatedData, error: updateError } = await useFetch<any[]>(
      `${baseURL}/config-pagos`,
      {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
          Authorization: `Bearer ${authStore.getToken}`,
        },
        body: JSON.stringify(saveObject),
      }
    );


  }




};





onBeforeMount(() => {
  if (!authStore.user?.role.type.includes("admin") && !authStore.user?.role.type.includes("digitador")) {
    router.push("/personal");
    toast.error('Disculpas, usted no esta autorizado en visitar "socios" page');
  }
});


// Code by Saeed
// // console.log(data);
</script>
<style scoped>
header {
  padding: 1rem 0;
  display: flex;
  gap: 1rem;
  border-bottom: 1px solid var(--gray-200);
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

.float {
  position: fixed;
  top: 100px;
  right: 30px;
}

.form {
  max-width: 670px;
}

.two-columns {
  display: grid;
  gap: 1rem;
  grid-template-columns: repeat(auto-fit, minmax(min(100%, 326px), 1fr));
}

.full-column {
  grid-column: 1/-1;
}

.margin-top-sm {
  margin-top: 1rem;
}
</style>
