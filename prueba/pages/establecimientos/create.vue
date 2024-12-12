<script setup lang="ts">
import { useToast } from "vue-toastification";
import BaseInput from "~/components/common/inputs/base-input.vue";
import BaseSelect from "~/components/common/inputs/base-select.vue";
import { useAuthStore } from "~~/store/auth";
import { Pagos } from '~/models/pagos.model';
import { ConfiguracionPago } from "~~/common/interfaces/user.interface";




const {
    public: { baseURL },
} = useRuntimeConfig();
definePageMeta({
    components: {
        BaseInput,
        BaseSelect,
    },
    layout: "private",
    middleware: ["auth"],
});
const toast = useToast();
const router = useRouter();
const authStore = useAuthStore();
const aprobacion_pagos1 = ref<any>([]);
const userVal = ref<any>();
const users = ref<any>([]);
const tipo_pagos = ref<any>([]);
const moneda_pagos = ref<any>([]);
const tipo_cambios = ref<any>([]);
const grupo_anticipos = ref<any>([]);
const observacion_pagos = ref<any>([]);
const aprobacion_pagos3 = ref<any>([]);
const tipo_cuentas3 = ref<any>([]);
const banco_cooperativas3 = ref<any>([]);
const tipo_cuentas = ref<any>([]);
const aprobacion_pagos2 = ref<any>([]);
const banco_cooperativas = ref<any>([]);
const tipo_cuentas2 = ref<any>([]);
const banco_cooperativas2 = ref<any>([]);
const defaultPagos: Pagos = {
    _id: '',
    published_at: '',
    aba: '',
    swift: '',
    banco_cooperativa3: '',
    banco_cooperativa2: '',
    tipo_cuenta3: '',
    tipo_cuenta2: '',
    observacion_pago: '',
    tipo_cambio: '',
    moneda_pago: '',
    tipo_pago: '',
    aprobacion_pago3: '',
    aprobacion_pago2: '',
    banco_cooperativa: '',
    grupo_anticipo: '',
    tipo_cuenta: '',
    aprobacion_pago1: '',
    numero_cuenta_pago3: 0,
    porcentaje_cancelaciones: 0,
    cheque_no_cheque: '',
    valor_cheque: 0,
    transferencia_al_extranjero: 0,
    transferencia_desde_extranjero: 0,
    pago_al_extranjero: 0,
    pago_desde_extranjero: 0,
    comodad_cuotas: 0,
    pago_prorrateado: 0,
    saldo_despues_deposito: 0,
    comisiones: 0,
    total_debitar: 0,
    bonos_pagar: 0,
    cuentas_cobrar: 0,
    numero_transferencia: '',
    impuesto_anticipado: 0,
    retencion_fuente: 0,
    retencion_deporte: 0,
    penalisaciones_sanciones: 0,
    descuento_viajes_anuales: 0,
    retencion_impuesto_renta: 0,
    retencion_proyectos: 0,
    retencion_seguro_vida: 0,
    monto_pagar_letras: 0,
    retencion_reforestacion: 0,
    monto_pagar: 0,
    retencion_iva_ecuador: 0,
    retencion_iva_panama: 0,
    compromiso_total_adeudado: 0,
    fecha_deposito: '',
    anticipos: 0,
    conversion_divisa: '',
    numero_cuenta_pago2: '',
    numero_cuenta_pago1: '',
    createdAt: '',
    updatedAt: '',
    __v: 0,
    id: '',
};
const currentPagos = ref<any>(defaultPagos);
const pagos_cofig = ref<ConfiguracionPago[]>([]); // Initialize as an empty array

const getPagosCofig = async () => {
    const { data: dataDatos } = await useFetch<ConfiguracionPago[]>(
        `${baseURL}/config-pagos`,
        {
            method: "GET",
            headers: {
                "Content-Type": "application/json",
                Authorization: "Bearer " + authStore.token,
            },
        }
    );
    if (dataDatos.value !== null) {
        pagos_cofig.value = dataDatos.value;
    } else {
        pagos_cofig.value = [];
    }
};
getPagosCofig()

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



const getUserPagos = () => {

    const selectedUser = pagos_cofig.value.find((user: any) => user.id === userVal.value[userVal.value.length - 1].id);
    if (selectedUser) {
        currentPagos.value = selectedUser;
    } else {
        currentPagos.value = defaultPagos;
    }

};


const defaultTaxes = {
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

function deepCopy(obj: any) {
    return JSON.parse(JSON.stringify(obj));
}

let taxes = ref(deepCopy(defaultTaxes));

watch(currentPagos, () => {

    const userData: any = currentPagos.value;
    if (!userData || userData === undefined) {
        taxes.value = deepCopy(defaultTaxes);
        return
    }
    taxes.value.aprobacion_pago1 = aprobacion_pagos1.value?.find(
        (aprobacionpago1: any) => aprobacionpago1.text === userData.aprobacion_pago1
    )?.id



    taxes.value.aprobacion_pago2 = aprobacion_pagos2.value?.find(
        (aprobacionpago2: any) => aprobacionpago2.text === userData.aprobacion_pago2
    )?.id

    taxes.value.aprobacion_pago3 = aprobacion_pagos3.value?.find(
        (aprobacionpago3: any) => aprobacionpago3.text === userData.aprobacion_pago3
    )?.id


    taxes.value.tipo_cuenta = tipo_cuentas.value?.find(
        (tipo_cuenta: any) => tipo_cuenta.text === userData.tipo_cuenta)?.id

    taxes.value.banco_cooperativa = banco_cooperativas.value?.find(
        (banco_cooperativa: any) => banco_cooperativa.text === userData.banco_cooperativa)?.id


    taxes.value.tipo_cuenta2 = tipo_cuentas2.value?.find(
        (tipo_cuenta2: any) => tipo_cuenta2.text === userData.tipo_cuenta2)?.id

    taxes.value.banco_cooperativa2 = banco_cooperativas2.value?.find(
        (banco_cooperativa2: any) => banco_cooperativa2.text === userData.banco_cooperativa2)?.id


    taxes.value.tipo_cuenta3 = tipo_cuentas3.value?.find(
        (tipo_cuenta3: any) => tipo_cuenta3.text === userData.tipo_cuenta3)?.id


    taxes.value.banco_cooperativa3 = banco_cooperativas3.value?.find(
        (banco_cooperativa3: any) => banco_cooperativa3.text === userData.banco_cooperativa3)?.id

    taxes.value.tipo_pago = tipo_pagos.value?.find(
        (tipo_pago: any) => tipo_pago.text === userData.tipo_pago)?.id


    taxes.value.moneda_pago = moneda_pagos.value?.find(
        (moneda_pago: any) => moneda_pago.text === userData.moneda_pago)?.id


    taxes.value.tipo_cambio = tipo_cambios.value?.find(
        (tipo_cambio: any) => tipo_cambio.text === userData.tipo_cambio)?.id


    taxes.value.observacion_pago = observacion_pagos.value?.find(
        (observacion_pago: any) => observacion_pago.text === userData.observacion_pago)?.id


    taxes.value.grupo_anticipo = grupo_anticipos.value?.find(
        (grupo_anticipo: any) => grupo_anticipo.text === userData.grupo_anticipo)?.id

    taxes.value.numero_cuenta_pago1 = userData.numero_cuenta_pago1
        ? userData.numero_cuenta_pago1.toString()
        : "0";


    taxes.value.numero_cuenta_pago2 = userData.numero_cuenta_pago2
        ? userData.numero_cuenta_pago2.toString()
        : "0";
    taxes.value.numero_cuenta_pago3 = userData.numero_cuenta_pago3
        ? userData.numero_cuenta_pago3.toString()
        : "0";
    taxes.value.aba = userData.aba;
    taxes.value.swift = userData.swift;
    taxes.value.anticipos = userData.anticipos;
    taxes.value.fecha_deposito = userData.fecha_deposito;
    taxes.value.retencion_iva_ecuador = userData.retencion_iva_ecuador;
    taxes.value.retencion_iva_panama = userData.retencion_iva_panama;
    taxes.value.retencion_reforestacion = userData?.retencion_reforestacion;
    taxes.value.retencion_seguro_vida = userData.retencion_seguro_vida;
    taxes.value.retencion_impuesto_renta = userData.retencion_impuesto_renta;
    taxes.value.retencion_proyectos = userData.retencion_proyectos;
    taxes.value.penalisaciones_sanciones = userData.penalisaciones_sanciones;
    taxes.value.descuento_viajes_anuales = userData.descuento_viajes_anuales;
    taxes.value.impuesto_anticipado = userData.impuesto_anticipado;
    taxes.value.retencion_deporte = userData.retencion_deporte;
    taxes.value.retencion_fuente = userData.retencion_fuente
        ? userData.retencion_fuente.toString()
        : "0";
    taxes.value.monto_pagar_letras = userData.monto_pagar_letras;
    taxes.value.compromiso_total_adeudado = userData.compromiso_total_adeudado;
    taxes.value.comodad_cuotas = userData.comodad_cuotas;
    taxes.value.pago_prorrateado = userData.pago_prorrateado;
    taxes.value.pago_desde_extranjero = userData.pago_desde_extranjero;
    taxes.value.pago_al_extranjero = userData.pago_al_extranjero;
    taxes.value.transferencia_desde_extranjero =
        userData.transferencia_desde_extranjero;
    taxes.value.transferencia_al_extranjero = userData.transferencia_al_extranjero;
    taxes.value.numero_transferencia = userData.numero_transferencia;
    taxes.value.cuentas_cobrar = userData.cuentas_cobrar;
    taxes.value.total_debitar = userData.total_debitar;
    taxes.value.bonos_pagar = userData.bonos_pagar;
    taxes.value.saldo_despues_deposito = userData.saldo_despues_deposito;
    taxes.value.comisiones = userData.comisiones;
    taxes.value.valor_cheque = userData.valor_cheque;
    taxes.value.cheque_no_cheque = userData.cheque_no_cheque;
    taxes.value.porcentaje_cancelaciones = userData.porcentaje_cancelaciones;
    taxes.value.conversion_divisa = userData.conversion_divisa;
});

const onChange = () => {
    if (userVal.value.length === 0) {
        userVal.value = [];
        currentPagos.value = defaultPagos;
        return;
    }
    getUserPagos();
    const lastItem = userVal.value.pop();
    userVal.value = [lastItem];
}



const savePaymentConfig = async () => {

    const saveObject = {
        aprobacion_pago1: aprobacion_pagos1.value?.find(
            (aprobacionpago1: any) => aprobacionpago1.id === taxes.value.aprobacion_pago1
        )?.text as any,

        aprobacion_pago2: aprobacion_pagos2.value?.find(
            (aprobacionpago2: any) => aprobacionpago2.id === taxes.value.aprobacion_pago2
        )?.text as any,

        aprobacion_pago3: aprobacion_pagos3.value.find(
            (aprobacionpago3: any) => aprobacionpago3.id === taxes.value.aprobacion_pago3
        )?.text as any,

        banco_cooperativa: banco_cooperativas.value.find(
            (banco: any) => banco.id == taxes.value.banco_cooperativa
        )?.text as any,

        banco_cooperativa2: banco_cooperativas2.value.find(
            (banco2: any) => banco2.id == taxes.value.banco_cooperativa2
        )?.text as any,

        banco_cooperativa3: banco_cooperativas3.value.find(
            (banco3: any) => banco3.id == taxes.value.banco_cooperativa3
        )?.text as any,

        tipo_cuenta: tipo_cuentas.value?.find(
            (cuenta: any) => cuenta.id == taxes.value.tipo_cuenta
        )?.text as any,

        tipo_cuenta2: tipo_cuentas2.value?.find(
            (tipo2: any) => tipo2.id == taxes.value.tipo_cuenta2
        )?.text as any,

        tipo_cuenta3: tipo_cuentas3.value.find(
            (tipo3: any) => tipo3.id == taxes.value.tipo_cuenta3
        )?.text as any,

        tipo_pago: tipo_pagos.value.find(
            (tipoPago1: any) => tipoPago1.id == taxes.value.tipo_pago
        )?.text as any,

        moneda_pago: moneda_pagos.value.find(
            (MonedaPago1: any) => MonedaPago1.id == taxes.value.moneda_pago
        )?.text as any,

        tipo_cambio: tipo_cambios.value.find(
            (TipoCambio1: any) => TipoCambio1.id == taxes.value.tipo_cambio
        )?.text as any,

        observacion_pago: observacion_pagos.value.find(
            (ObservaPago1: any) => ObservaPago1.id == taxes.value.observacion_pago
        )?.text as any,

        grupo_anticipo: grupo_anticipos.value.find(
            (grupoAnticipo1: any) => grupoAnticipo1.id == taxes.value.grupo_anticipo
        )?.text as any,

        aba: taxes.value.aba,
        swift: taxes.value.swift,

        anticipos: taxes.value.anticipos ? Number(taxes.value.anticipos) ? Number(taxes.value.anticipos) : 0 : 0,
        numero_cuenta_pago1: Number(taxes.value.numero_cuenta_pago1),
        numero_cuenta_pago2: Number(taxes.value.numero_cuenta_pago2),
        numero_cuenta_pago3: Number(taxes.value.numero_cuenta_pago3),

        compromiso_total_adeudado: taxes.value.compromiso_total_adeudado ? Number(taxes.value.compromiso_total_adeudado) ? Number(taxes.value.compromiso_total_adeudado) : 0 : 0,
        fecha_deposito: taxes.value.fecha_deposito,
        retencion_iva_ecuador: Number(taxes.value.retencion_iva_ecuador) ? Number(taxes.value.retencion_iva_ecuador) : 0,
        retencion_iva_panama: Number(taxes.value.retencion_iva_panama) ? Number(taxes.value.retencion_iva_panama) : 0,
        retencion_reforestacion: Number(taxes.value.retencion_reforestacion) ? Number(taxes.value.retencion_reforestacion) : 0,
        retencion_seguro_vida: Number(taxes.value.retencion_seguro_vida) ? Number(taxes.value.retencion_seguro_vida) : 0,
        retencion_impuesto_renta: Number(taxes.value.retencion_impuesto_renta) ? Number(taxes.value.retencion_impuesto_renta) : 0,
        retencion_proyectos: Number(taxes.value.retencion_proyectos) ? Number(taxes.value.retencion_proyectos) : 0,
        penalisaciones_sanciones: Number(taxes.value.penalisaciones_sanciones) ? Number(taxes.value.penalisaciones_sanciones) : 0,
        descuento_viajes_anuales: Number(taxes.value.descuento_viajes_anuales) ? Number(taxes.value.descuento_viajes_anuales) : 0,
        impuesto_anticipado: Number(taxes.value.impuesto_anticipado) ? Number(taxes.value.impuesto_anticipado) : 0,
        retencion_deporte: Number(taxes.value.retencion_deporte) ?? 0,
        retencion_fuente: Number(taxes.value.retencion_fuente) ? Number(taxes.value.retencion_fuente) : 0,
        monto_pagar: Number(taxes.value.monto_pagar) ? Number(taxes.value.monto_pagar) : 0,
        monto_pagar_letras: Number(taxes.value.monto_pagar_letras) ? Number(taxes.value.monto_pagar_letras) : 0,
        numero_transferencia: taxes.value.numero_transferencia,
        cuentas_cobrar: taxes.value.cuentas_cobrar,
        total_debitar: Number(taxes.value.total_debitar) ? Number(taxes.value.total_debitar) : 0,
        bonos_pagar: Number(taxes.value.bonos_pagar) ? Number(taxes.value.bonos_pagar) : 0,
        saldo_despues_deposito: Number(taxes.value.saldo_despues_deposito) ? Number(taxes.value.saldo_despues_deposito) : 0,
        comisiones: Number(taxes.value.comisiones) ? Number(taxes.value.comisiones) : 0,
        comodad_cuotas: Number(taxes.value.comodad_cuotas) ? Number(taxes.value.comodad_cuotas) : 0,
        pago_prorrateado: Number(taxes.value.pago_prorrateado) ? Number(taxes.value.pago_prorrateado) : 0,
        pago_desde_extranjero: Number(taxes.value.pago_desde_extranjero) ? Number(taxes.value.pago_desde_extranjero) : 0,
        pago_al_extranjero: Number(taxes.value.pago_al_extranjero) ? Number(taxes.value.pago_al_extranjero) : 0,
        transferencia_desde_extranjero:
            Number(taxes.value.transferencia_desde_extranjero) ? Number(taxes.value.transferencia_desde_extranjero) : 0,
        transferencia_al_extranjero:
            Number(taxes.value.transferencia_al_extranjero) ? Number(taxes.value.transferencia_al_extranjero) : 0,
        valor_cheque: Number(taxes.value.valor_cheque) ? Number(taxes.value.valor_cheque) : 0,
        cheque_no_cheque: Number(taxes.value.cheque_no_cheque) ? Number(taxes.value.cheque_no_cheque) : 0,
        porcentaje_cancelaciones: Number(taxes.value.porcentaje_cancelaciones) ? Number(taxes.value.porcentaje_cancelaciones) : 0,
        conversion_divisa: taxes.value.conversion_divisa,
    };
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
    if (updatedData.value) {
        toast.success("pago guardado exitosamente!");
        router.push('/pagos');
        return;
    }

    if (updateError) {
        toast.error("el pago no se pudo guardar");
        return;
    }

}




onBeforeMount(() => {
    if (!authStore.user?.role.type.includes("admin") && !authStore.user?.role.type.includes("digitador")) {
        router.push("/personal");
        toast.error('Disculpas, usted no esta autorizado en visitar "socios" page');
    }
});



// Code by Ammar Ahmed
</script>
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

                        <!-- <div v-if="pagos_cofig"
                            class="card flex justify-content-center">
                            
                        </div> -->

                        <div>
                            <label for="users">
                                <span style="font-weight: 600">Users</span>
                                <!-- <select class="custom-select"
                                    id="$attrs['for']"
                                    name="name"
                                    @change="getUserPagos"
                                    v-model="userVal">
                                    <option v-for="(option, idx) in pagos_cofig"
                                        :key="idx"
                                        :value="option.id">
                                        {{ option.numero_cuenta_pago1 }}
                                    </option>
                                </select> -->

                                <MultiSelect v-model="userVal"
                                    :options="pagos_cofig"
                                    optionLabel="numero_cuenta_pago1"
                                    placeholder="seleccionar cuenta"
                                    :maxSelectedLabels="1"
                                    @change="onChange()"
                                    filter
                                    class="w-full md:w-20rem" />
                            </label>

                        </div>


                        <h2 class="full-column margin-top-sm">Cuenta 1</h2>

                        <BaseSelect v-model="taxes.aprobacion_pago1"
                            label="Aprobación Pago1"
                            :options="aprobacion_pagos1" />

                        <BaseSelect v-model="taxes.tipo_cuenta"
                            label="Tipo Cuenta 1"
                            :options="tipo_cuentas" />

                        <BaseInput v-model="taxes.numero_cuenta_pago1"
                            label="Número de Cuenta 1"
                            type="text"
                            :disabled="false" />

                        <BaseSelect v-model="taxes.banco_cooperativa"
                            label="Banco/Cooperativa"
                            :options="banco_cooperativas" />
                        <h2 class="full-column margin-top-sm">Cuenta 2</h2>

                        <BaseSelect v-model="taxes.aprobacion_pago2"
                            label="Aprobación Pago2"
                            :options="aprobacion_pagos2" />


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

                        <h2 class="full-column margin-top-sm">Cuenta 3</h2>

                        <BaseSelect v-model="taxes.aprobacion_pago3"
                            label="Aprobación Pago3"
                            :options="aprobacion_pagos3" />
                        <BaseSelect v-model="taxes.tipo_cuenta3"
                            label="Tipo Cuenta 3"
                            :options="tipo_cuentas3" />

                        <BaseInput v-model="taxes.numero_cuenta_pago3"
                            label="Número de Cuenta 3"
                            type="text"
                            :disabled="false" />
                        <BaseSelect v-model="taxes.banco_cooperativa3"
                            label="Banco/Cooperativa 3"
                            :options="banco_cooperativas3" />

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

<style scoped>
:deep(.p-multiselect) {
    color: var(--gray-800);
    background-color: var(--white);
    border: 1px solid var(--gray-500);
}

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

label {
    display: flex;
    flex-direction: column;
    gap: 0.25rem;
}
</style>
  