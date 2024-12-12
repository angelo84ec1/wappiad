<template>
  <main style="background-color: #f1f8f8">
    <header>
      <div class="home__actions">
        <h2>Editar socio</h2>
      </div>
    </header>
    <div class="home__content">
      <div class="home__actions">
        <h3>Sobre el socio</h3>
        <div class="home__buttons">
          <button class="button button--secondary float" @click.prevent="save()">
            <img src="~/assets/images/save-green.png" alt="" /> Guardar cambios
          </button>
         
        </div>
      </div>
      <form ref="formPersonalData" class="form">
        <div class="form__group">
          <div class="two-columns d-flex">
            <BaseFileInput
              v-model="formEdit.foto"
              :v="vuelidate"
              class="full-column"
              label="Foto de perfil"
              name="foto"
              @update:modelValue="formEdit.foto = $event"
            />
            <BaseSelect
              v-model="formEdit.status"
              :v="vuelidate.status"
              name="status"
              class="full-column"
              type="text"
              label="Status"
              placeholder="Activo"
              :options="statusOptions"
            />
            <BaseInput
              v-model="formEdit.nombres"
              :v="vuelidate.nombres"
              type="text"
              label="Nombres"
              placeholder="Luis"
              class="new-line"
              name="nombres"
            />
            <BaseInput
              v-model="formEdit.apellidos"
              :v="vuelidate.apellidos"
              type="text"
              label="Apellidos"
              placeholder="Vasquez"
              name="apellidos"
            />
            <BaseInput
              v-model="formEdit.compania"
              name="compania"
              :v="vuelidate.compania"
              type="text"
              label="Compañia"
            />
           
            <BaseInput
              v-model="formEdit.cedula_ruc"
              name="cedula_ruc"
              :v="vuelidate.cedula_ruc"
              type="text"
              label="Identificación o Ruc"
            />
            <BaseInput
              v-model="formEdit.cedula"
              name="cedula"
              :v="vuelidate.cedula"
              type="text"
              label="Cedula"
            />
            <BaseInput
              v-model="formEdit.pasaporte"
              name="pasaporte"
              :v="vuelidate.pasaporte"
              type="text"
              label="Pasaporte"
            />
            <BaseInput
              v-model="formEdit.fecha_nacimiento"
              :v="vuelidate.fecha_nacimiento"
              type="date"
              label="Nacimiento"
              name="fecha_nacimiento"
            />
            <BaseSelect
              v-model="formEdit.sexo"
              :v="vuelidate.sexo"
              label="Sexo"
              :options="sexOptions"
              name="sexo"
            />
            <BaseSelect
              v-model="formEdit.discapacidad"
              :v="vuelidate.discapacidad"
              label="Discapacidad fisica o mental"
              :options="yesNoOptions"
              name="discapacidad"
            />
            
            <BaseSelect
              v-model="formEdit.tipo_sangre"
              :v="vuelidate.tipo_sangre"
              label="Tipo de sangre"
              :options="bloodOptions"
              name="tipo_sangre"
            />
            <BaseSelect
              v-model="formEdit.nacionalidad"
              :v="vuelidate.nacionalidad"
              label="Nacionalidad"
              :options="nationalityOptions"
              name="nacionalidad"
            />
            <BaseSelect
              v-model="formEdit.estado_civil"
              :v="vuelidate.estado_civil"
              label="Estado civil"
              :options="civilStateOptions"
              name="estado_civil"
            />
           
          </div>
        </div>

        <div class="form__group">
          <h2>Contacto</h2>
          <div class="two-columns d-flex">
            <BaseInput
              v-model="formEdit.celular"
              :v="vuelidate.celular"
              type="text"
              label="Celular"
              name="celular"
            />
            <BaseInput
              v-model="formEdit.telefono_convencional"
              :v="vuelidate.telefono_convencional"
              type="text"
              label="Teléfono convencional"
              name="telefono_convencional"
            />
            <BaseInput
              v-model="formEdit.correo"
              :v="vuelidate.correo"
              type="email"
              label="Correo"
              name="correo"
            />
            <BaseInput
              v-model="formEdit.correo_alternativo"
              :v="vuelidate.correo_alternativo"
              type="email"
              label="Correo alternativo"
              name="correo_alternativo"
            />
           
           
          </div>
        </div>

        <div class="form__group">
          <h2>Datos avanzados</h2>
          <div class="one-column d-flex">
            
          
            
           
            <BaseInput
              v-model="formEdit.fecha_de_ingreso_a_la_organizacion"
              :v="vuelidate.fecha_de_ingreso_a_la_organizacion"
              name="fecha_de_ingreso_a_la_organizacion"
              type="date"
              class="full-column-2"
              label="Fecha de Ingreso a la Organización"
            />
            <BaseSelect
              v-model="formEdit.pais"
              :v="vuelidate.pais"
              name="pais"
              class="full-column-2"
              label="Pais"
              :options="paisOptions"
            />
            <BaseSelect
              v-model="formEdit.ciudad"
              :v="vuelidate.ciudad"
              name="ciudad"
              class="full-column-2"
              label="Ciudad"
              :options="ciudadOptions"
            />
            
            <BaseSelect
              v-model="formEdit.provincia"
              :v="vuelidate.provincia"
              name="provincia"
              class="full-column-2"
              label="Provincia"
              :options="provinciaOptions"
            />
            <!-- <BaseInput
              v-model="formEdit.departamento"
              :v="vuelidate.departamento"
              name="departamento"
              class="full-column-2"
              label="Departamento"
            /> -->
           

            <!--<BaseInput
              v-model="formEdit.canton"
              :v="vuelidate.canton"
              name="canton"
              class="full-column-2"
              label="Cantón"
            /> -->
            <BaseSelect
            v-model="formEdit.canton"
              :v="vuelidate.canton"
              name="canton"
              class="full-column-2"
              label="Cantón"
              :options="cantonOptions"
            />
            
            
          </div>
        </div>

        <div class="form__group">
          <h2>Número de Socios</h2>
          <div class="two-columns d-flex">
            <BaseInput
              v-model="formEdit.valor_del_contrato"
              name="valor_del_contrato"
              :v="vuelidate.valor_del_contrato"
              type="text"
              class="full-column-2"
              label="Valor del contrato"
            />
            <BaseInput
              v-model="formEdit.valor_adendum"
              name="valor_adendum"
              :v="vuelidate.valor_adendum"
              type="text"
              class="full-column-2"
              label="Valor Adendum"
            />
           
            
           
            
            
            
            
          
          </div>
        </div>


      </form>
    </div>
    <scroll-top />
  </main>
</template>
<script setup lang="ts">
import { useVuelidate } from "@vuelidate/core";
import { required, email, decimal, helpers, numeric } from "@vuelidate/validators";
import { StatusRegistry } from "~/common/enums/status.enum";
import { SelectOption } from "~/common/interfaces/select-option.interface";
import BaseInput from "~/components/common/inputs/base-input.vue";
import BaseSelect from "~/components/common/inputs/base-select.vue";
import BaseFileInput from "~/components/common/inputs/file-input.vue";
import ScrollTop from "~/components/common/buttons/scroll-top.vue";
import { DatosPersonales } from "~/common/interfaces/user.interface";
import { useAuthStore } from "~~/store/auth";
import { useToast } from "vue-toastification";
import { CargaCivil} from "~~/common/interfaces/options.interface";


definePageMeta({
  name: "EditSociosPage",
  components: {
    BaseInput,
    BaseFileInput,
    BaseSelect,
    ScrollTop,

  },
  layout: "private",
});

const router = useRouter();
const { params } = useRoute();

const idDatos = computed(() => params.id);
const {
  public: { baseURL },
} = useRuntimeConfig();
const authStore = useAuthStore();

const { data: user } = useAsyncData<DatosPersonales>(
  "datos-personales",
  () =>
    $fetch(`${baseURL}/datos-personales/${idDatos.value}`, {
      method: "GET",
      headers: {
        "Content-Type": "application/json",
        Authorization: `Bearer ${authStore.token}`,
      },
    }),
  { watch: [idDatos] }
);
watch(user, (value) => {
  for (const key in value) {
    formEdit[key] = value[key];
  }
});



const statusOptions = ref<SelectOption[]>([
  { text: "Activo", value: "true" },
  { text: "Inactivo", value: "false" },
]);
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

const formEdit = reactive({
  status: "",
  foto: null,
  nombres: "",
  apellidos: "",
  compania: "",
  categoria: "",
  cedula_ruc: "",
  cedula: "",
  pasaporte: "",
  fecha_nacimiento: "",
  sexo: "",
  discapacidad: "",
  jubilacion: "",
  tipo_sangre: "",
  nacionalidad: "",
  estado_civil: "",
  carga_civil: "",
  celular: "",
  telefono_convencional: "",
  correo: "",
  correo_alternativo: "",
  coordinador: "",
  cedula_coordinador: "",
  tipo_de_proyecto: "",
  tipo_de_servicio: "",
  ocupacion: "",
  profesion: "",
  fecha_de_ingreso_a_la_organizacion: "",
  pais: "",
  ciudad: "",
  corregimiento: "",
  provincia: "",
  departamento: "",
  canton: "",
  domicilio1: "",
  domicilio2: "",
  casa: "",
  pasaje: "",
  codigo_postal: "",
  valor_del_contrato: "",
  valor_adendum: "",
  valor_cheque: "",
  acta_de_adelanto: "",
  acta_de_finiquito: "",
  acta_compromiso_pago: "",
  contrato_privado_gestion_intermediacion: "",
  pagare: "",
  valor_letra_de_cambio: "",
  bono_eficiencia_cumplimiento: "",
  convenio_compensacion: "",
  certificado_garantia_depositos: "",
  numero_contrato: "",
  declaracion_jurada: "",
  numero_cuenta: "",
  banco_cooperativa: "",
  tipo_cuenta: "",
  numero_cuenta2: "",
  banco_cooperativa2: "",
  tipo_cuenta2: "",
  numero_cuenta3: "",
  banco_cooperativa3: "",
  tipo_cuenta3: "",
  beneficiario1: "",
  cedula_beneficiario1: "",
  pasaporte_beneficiario1: "",
  nacimiento_beneficiario1: "",
  nacionalidad_beneficiario1: "",
  sexo_beneficiario1: "",
  parentezco_beneficiario1: "",
  edad_beneficiario1: "",
  celular_beneficiario1: "",
  telefono_convencional_beneficiario1: "",
  email_beneficiario1: "",
  domicilio_beneficiario1: "",
  beneficiario2: "",
  cedula_beneficiario2: "",
  pasaporte_beneficiario2: "",
  nacimiento_beneficiario2: "",
  nacionalidad_beneficiario2: "",
  sexo_beneficiario2: "",
  parentezco_beneficiario2: "",
  edad_beneficiario2: "",
  celular_beneficiario2: "",
  telefono_convencional_beneficiario2: "",
  email_beneficiario2: "",
  domicilio_beneficiario2: "",
  beneficiario3: "",
  cedula_beneficiario3: "",
  pasaporte_beneficiario3: "",
  nacimiento_beneficiario3: "",
  nacionalidad_beneficiario3: "",
  sexo_beneficiario3: "",
  parentezco_beneficiario3: "",
  edad_beneficiario3: "",
  celular_beneficiario3: "",
  telefono_convencional_beneficiario3: "",
  email_beneficiario3: "",
  domicilio_beneficiario3: "",
});

const rules = {
  status: { required: helpers.withMessage("Este campo no puede estar vacio", required) },
  foto: {},
  nombres: { required: helpers.withMessage("Este campo no puede estar vacio", required) },
  apellidos: {
    required: helpers.withMessage("Este campo no puede estar vacio", required),
  },
  compania: {
    required: helpers.withMessage("Este campo no puede estar vacio", required),
  },
  categoria: {
    required: helpers.withMessage("Este campo no puede estar vacio", required),
  },
  cedula_ruc: {
    required: helpers.withMessage("Este campo no puede estar vacio", required),
  },
  cedula: { required: helpers.withMessage("Este campo no puede estar vacio", required) },
  pasaporte: {
    required: helpers.withMessage("Este campo no puede estar vacio", required),
  },
  fecha_nacimiento: {},
  sexo: {},
  discapacidad: {
    required: helpers.withMessage("Este campo no puede estar vacio", required),
  },
  jubilacion: {
    required: helpers.withMessage("Este campo no puede estar vacio", required),
  },
  tipo_sangre: {},
  nacionalidad: {},
  estado_civil: {},
  carga_civil: {},
  celular: { numeric: helpers.withMessage("Este campo solo acepta numeros", numeric) },
  telefono_convencional: {
    numeric: helpers.withMessage("Este campo solo acepta numeros", numeric),
  },
  correo: {
    required: helpers.withMessage("Este campo no puede estar vacio", required),
    email: helpers.withMessage("Debe ser un email valido", email),
  },
  correo_alternativo: { email },
  coordinador: {
    required: helpers.withMessage("Este campo no puede estar vacio", required),
  },
  cedula_coordinador: {
    required: helpers.withMessage("Este campo no puede estar vacio", required),
  },
  tipo_de_proyecto: {},
  tipo_de_servicio: {},
  ocupacion: {},
  profesion: {},
  fecha_de_ingreso_a_la_organizacion: {},
  pais: {},
  ciudad: {},
  corregimiento: {},
  provincia: {},
  departamento: {},
  canton: {},
  domicilio1: {},
  domicilio2: {},
  casa: {},
  pasaje: {},
  codigo_postal: {},
  valor_del_contrato: {
    required: helpers.withMessage("Este campo no puede estar vacio", required),
    decimal: helpers.withMessage("Debe de ser un decimal", decimal),
  },
  valor_adendum: {
    required: helpers.withMessage("Este campo no puede estar vacio", required),
    decimal: helpers.withMessage("Debe de ser un decimal", decimal),
  },
  valor_cheque: {
    required: helpers.withMessage("Este campo no puede estar vacio", required),
    decimal: helpers.withMessage("Debe de ser un decimal", decimal),
  },
  acta_de_adelanto: {
    required: helpers.withMessage("Este campo no puede estar vacio", required),
    decimal: helpers.withMessage("Debe de ser un decimal", decimal),
  },
  acta_de_finiquito: {
    required: helpers.withMessage("Este campo no puede estar vacio", required),
    decimal: helpers.withMessage("Debe de ser un decimal", decimal),
  },
  acta_compromiso_pago: {
    required: helpers.withMessage("Este campo no puede estar vacio", required),
    decimal: helpers.withMessage("Debe de ser un decimal", decimal),
  },
  contrato_privado_gestion_intermediacion: {
    required: helpers.withMessage("Este campo no puede estar vacio", required),
    decimal: helpers.withMessage("Debe de ser un decimal", decimal),
  },
  pagare: {
    required: helpers.withMessage("Este campo no puede estar vacio", required),
    decimal,
  },
  valor_letra_de_cambio: {
    required: helpers.withMessage("Este campo no puede estar vacio", required),
    decimal: helpers.withMessage("Debe de ser un decimal", decimal),
  },
  bono_eficiencia_cumplimiento: {
    required: helpers.withMessage("Este campo no puede estar vacio", required),
    decimal: helpers.withMessage("Debe de ser un decimal", decimal),
  },
  convenio_compensacion: {
    required: helpers.withMessage("Este campo no puede estar vacio", required),
    decimal: helpers.withMessage("Debe de ser un decimal", decimal),
  },
  certificado_garantia_depositos: {
    required: helpers.withMessage("Este campo no puede estar vacio", required),
    decimal: helpers.withMessage("Debe de ser un decimal", decimal),
  },
  numero_contrato: {},
  declaracion_jurada: {},
  numero_cuenta: {},
  banco_cooperativa: {},
  tipo_cuenta: {},
  numero_cuenta2: {},
  banco_cooperativa2: {},
  tipo_cuenta2: {},
  numero_cuenta3: {},
  banco_cooperativa3: {},
  tipo_cuenta3: {},
  beneficiario1: {},
  cedula_beneficiario1: {},
  pasaporte_beneficiario1: {},
  nacimiento_beneficiario1: {},
  nacionalidad_beneficiario1: {},
  sexo_beneficiario1: {},
  parentezco_beneficiario1: {},
  edad_beneficiario1: {},
  celular_beneficiario1: {},
  telefono_convencional_beneficiario1: {},
  email_beneficiario1: { email },
  domicilio_beneficiario1: {},
  beneficiario2: {},
  cedula_beneficiario2: {},
  pasaporte_beneficiario2: {},
  nacimiento_beneficiario2: {},
  nacionalidad_beneficiario2: {},
  sexo_beneficiario2: {},
  parentezco_beneficiario2: {},
  edad_beneficiario2: {},
  celular_beneficiario2: {},
  telefono_convencional_beneficiario2: {},
  email_beneficiario2: { email },
  domicilio_beneficiario2: {},
  beneficiario3: {},
  cedula_beneficiario3: {},
  pasaporte_beneficiario3: {},
  nacimiento_beneficiario3: {},
  nacionalidad_beneficiario3: {},
  sexo_beneficiario3: {},
  parentezco_beneficiario3: {},
  edad_beneficiario3: {},
  celular_beneficiario3: {},
  telefono_convencional_beneficiario3: {},
  email_beneficiario3: { email },
  domicilio_beneficiario3: {},
};

const vuelidate = useVuelidate(rules, formEdit);

const { data: paisOptions } = useAsyncData("paises", async () => {
  const data = await $fetch(`${baseURL}/paises`, {
    method: "GET",
    headers: {
      "Content-Type": "application/json",
      Authorization: `Bearer ${authStore.token}`,
    },
  });
  const options = data.map((pais: any) => {
    return {
      text: pais.nombre,
      value: pais.nombre,
    };
  });
  return options;
});



const goToUploadDocuments = () => {
router.push("/personal/subir-documentos");
};


const { data: bloodOptions } = useAsyncData("tipo-de-sangres", async () => {
  const data = await $fetch(`${baseURL}/tipo-de-sangres`, {
    method: "GET",
    headers: {
      "Content-Type": "application/json",
      Authorization: `Bearer ${authStore.token}`,
    },
  });
  const options = data.map((tipo: any) => {
    return {
      text: tipo.nombre,
      value: tipo.nombre,
    };
  });
  return options;
});

const { data: cargaCivilOptions } = useAsyncData(
  "cargas",
  async () => {
    const data = await $fetch<CargaCivil[]>(`${baseURL}/cargas-civiles`, {
      method: "GET",
      headers: {
        "Content-Type": "application/json",
        Authorization: `Bearer ${authStore.token}`,
      },
    });
    const options = data.map((carga) => {
      return {
        text: carga.nombre,
        value: carga.nombre,
      };
    });
    return options;
  },
  { server: false }
);

const { data: nationalityOptions } = useAsyncData("nacionalidads", async () => {
  const data = await $fetch(`${baseURL}/nacionalidads`, {
    method: "GET",
    headers: {
      "Content-Type": "application/json",
      Authorization: `Bearer ${authStore.token}`,
    },
  });
  const options = data.map((nacionalidad: any) => {
    return {
      text: nacionalidad.nombre,
      value: nacionalidad.nombre,
    };
  });
  return options;
});

const { data: proyectoOptions } = useAsyncData("tipo-de-proyectos", async () => {
  const data = await $fetch(`${baseURL}/tipo-de-proyectos`, {
    method: "GET",
    headers: {
      "Content-Type": "application/json",
      Authorization: `Bearer ${authStore.token}`,
    },
  });
  const options = data.map((proyecto: any) => {
    return {
      text: proyecto.nombre,
      value: proyecto.nombre,
    };
  });
  return options;
});

const { data: tipoServicioOptions } = useAsyncData("tipo-de-servicios", async () => {
  const data = await $fetch(`${baseURL}/tipo-de-servicios`, {
    method: "GET",
    headers: {
      "Content-Type": "application/json",
      Authorization: `Bearer ${authStore.token}`,
    },
  });
  const options = data.map((tipoServicio: any) => {
    return {
      text: tipoServicio.nombre,
      value: tipoServicio.nombre,
    };
  });
  return options;
});

const { data: ocupationOptions } = useAsyncData("ocupaciones", async () => {
  const data = await $fetch(`${baseURL}/ocupaciones`, {
    method: "GET",
    headers: {
      "Content-Type": "application/json",
      Authorization: `Bearer ${authStore.token}`,
    },
  });
  const options = data.map((ocupacion: any) => {
    return {
      text: ocupacion.nombre,
      value: ocupacion.nombre,
    };
  });
  return options;
});

const { data: profesionOptions } = useAsyncData("profesiones", async () => {
  const data = await $fetch(`${baseURL}/profesiones`, {
    method: "GET",
    headers: {
      "Content-Type": "application/json",
      Authorization: `Bearer ${authStore.token}`,
    },
  });
  const options = data.map((profesion: any) => {
    return {
      text: profesion.nombre,
      value: profesion.nombre,
    };
  });
  return options;
});

const { data: declaracionOptions } = useAsyncData("declaraciones-juradas", async () => {
  const data = await $fetch(`${baseURL}/declaraciones-juradas`, {
    method: "GET",
    headers: {
      "Content-Type": "application/json",
      Authorization: `Bearer ${authStore.token}`,
    },
  });
  const options = data.map((declaracion: any) => {
    return {
      text: declaracion.nombre,
      value: declaracion.nombre,
    };
  });
  return options;
});

const { data: bankOptions } = useAsyncData("bancos", async () => {
  const data = await $fetch(`${baseURL}/bancos`, {
    method: "GET",
    headers: {
      "Content-Type": "application/json",
      Authorization: `Bearer ${authStore.token}`,
    },
  });
  const options = data.map((banco: any) => {
    return {
      text: banco.Nombre,
      value: banco.Nombre,
    };
  });
  return options;
});

const { data: accountTypeOptions } = useAsyncData("tipo-cuentas", async () => {
  const data = await $fetch(`${baseURL}/tipo-cuentas`, {
    method: "GET",
    headers: {
      "Content-Type": "application/json",
      Authorization: `Bearer ${authStore.token}`,
    },
  });
  const options = data.map((tipoCuenta: any) => {
    return {
      text: tipoCuenta.Tipo,
      value: tipoCuenta.Tipo,
    };
  });
  return options;
});

const { data: corregimientoOptions } = useAsyncData("corregimientos", async () => {
  const data = await $fetch(`${baseURL}/corregimientos`, {
    method: "GET",
    headers: {
      "Content-Type": "application/json",
      Authorization: `Bearer ${authStore.token}`,
    },
  });
  const options = data.map((corregimiento: any) => {
    return {
      text: corregimiento.nombre,
      value: corregimiento.nombre,
    };
  });
  return options;
});

const { data: provinciaOptions } = useAsyncData("provincias", async () => {
  const data = await $fetch(`${baseURL}/provincias`, {
    method: "GET",
    headers: {
      "Content-Type": "application/json",
      Authorization: `Bearer ${authStore.token}`,
    },
  });
  const options = data.map((provincia: any) => {
    return {
      text: provincia.nombre,
      value: provincia.nombre,
    };
  });
  return options;
});



const { data: DepartamentoOptions } = useAsyncData(
  "departamentos",
  async () => {
    const data = await $fetch(`${baseURL}/departamentos`, {
      method: "GET",
      headers: {
        "Content-Type": "application/json",
        Authorization: `Bearer ${authStore.token}`,
      },
    });
    const options = data.map((Departamentos: any) => {
      return {
        text: Departamentos.Nombre,
        value: Departamentos.Nombre,
      };
    });
    return options;
  },
);



const { data: cantonOptions } = useAsyncData(
  "cantones-ecuadors",
  async () => {
    const data = await $fetch(`${baseURL}/cantones-ecuadors`, {
      method: "GET",
      headers: {
        "Content-Type": "application/json",
        Authorization: `Bearer ${authStore.token}`,
      },
    });
    const options = data.map((cantonEcuador: any) => {
      return {
        text: cantonEcuador.nombre,
        value: cantonEcuador.nombre,
      };
    });
    return options;
  },
);


const { data: ciudadOptions } = useAsyncData("ciudades", async () => {
  const data = await $fetch(`${baseURL}/ciudades`, {
    method: "GET",
    headers: {
      "Content-Type": "application/json",
      Authorization: `Bearer ${authStore.token}`,
    },
  });
  const options = data.map((ciudad: any) => {
    return {
      text: ciudad.nombre,
      value: ciudad.nombre,
    };
  });
  return options;
});

const { data: parentescoOptions } = useAsyncData("parentescos", async () => {
  const data = await $fetch(`${baseURL}/parentescos`, {
    method: "GET",
    headers: {
      "Content-Type": "application/json",
      Authorization: `Bearer ${authStore.token}`,
    },
  });
  const options = data.map((parentesco: any) => {
    return {
      text: parentesco.nombre,
      value: parentesco.nombre,
    };
  });
  return options;
});

const formPersonalData = ref(null);

const toast = useToast();

const save = async () => {
  vuelidate.value.$touch();
  if (!(await vuelidate.value.$validate())) {
    toast.warning("Por favor, revise los campos marcados en rojo");
    return;
  }
  const data: { [key: string]: string } = {};
  const formData = new FormData();
  for (const key in formEdit) {
    if (key === "foto") {
      formData.append(`files.${key}`, formEdit[key]);
    }
    if (formEdit[key] !== "" && key !== "foto") {
      data[key] = formEdit[key];
    }
  }
  formData.append("data", JSON.stringify(data));
  await $fetch(`${baseURL}/datos-personales/${idDatos.value}`, {
    method: "PUT",
    headers: {
      Authorization: `Bearer ${authStore.token}`,
    },
    body: formData,
  }).catch((err) => {
    console.log(err);
    formData.delete("data");
    formData.delete("files.foto");
    toast.error("Error al guardar los datos");
  });
  formData.delete("data");
  formData.delete("files.foto");
  toast.success("Datos guardados correctamente");
  await router.push("/socios?created=true");
};





onBeforeMount(() => {
  if (!authStore.user?.role.type.includes("admin")) {
    router.push("/personal");
    toast.error('Disculpas, usted no esta autorizado en visitar "socios/id" page');
  }
});
</script>
<style scoped>
header {
  padding: 1rem 0;
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
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

.home__actions > h3 {
  font-size: var(--heading-2);
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


.float{

  position: fixed;
  top: 100px;
  right: 30px;
  z-index: 10;


}

.home__link {
  color: var(--links);
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
  }
</style>
<style>
@media only screen and (max-width: 600px) {
body .home__container {
  display: block !important;
}
}
</style>
