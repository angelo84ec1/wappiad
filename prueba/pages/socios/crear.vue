<template>
  <main style="background-color: #f1f8f8">
    <header>
      <div class="home__actions">
        <h2>Agregar socio</h2>
      </div>
    </header>
    <div class="home__content">
      <div class="home__actions">
        <h3>Sobre el socio</h3>
        <div class="home__buttons">
          <button class="button button--secondary" @click.prevent="save()">
            <img src="~/assets/images/save-green.png" alt="" /> Guardar cambios
          </button>
        </div>
      </div>
      <form ref="formPersonalData" class="form">
        <div class="form__group">
          <div class="two-columns">
            <BaseFileInput
              v-model="formCreate.foto"
              :v="vuelidate"
              class="full-column"
              label="Foto de perfil"
              name="foto"
              @update:modelValue="formCreate.foto = $event"
            />
            <BaseSelect
              v-model="formCreate.status"
              :v="vuelidate.status"
              name="status"
              type="text"
              label="Status"
              placeholder="Activo"
              :options="statusOptions"
            />
            <BaseInput
              v-model="formCreate.nombres"
              :v="vuelidate.nombres"
              type="text"
              label="Nombres"
              placeholder="Luis"
              class="new-line"
              name="nombres"
            />
            <BaseInput
              v-model="formCreate.apellidos"
              :v="vuelidate.apellidos"
              type="text"
              label="Apellidos"
              placeholder="Vasquez"
              name="apellidos"
            />
            <BaseInput
              v-model="formCreate.compania"
              name="compania"
              :v="vuelidate.compania"
              type="text"
              label="Compañia"
            />
            <BaseInput
              v-model="formCreate.categoria"
              name="categoria"
              :v="vuelidate.categoria"
              type="text"
              label="Categoría"
            />
            <BaseInput
              v-model="formCreate.cedula_ruc"
              name="cedula_ruc"
              :v="vuelidate.cedula_ruc"
              type="text"
              label="Identificación o Ruc"
            />
            <BaseInput
              v-model="formCreate.cedula"
              name="cedula"
              :v="vuelidate.cedula"
              type="text"
              label="Cedula"
            />
            <BaseInput
              v-model="formCreate.pasaporte"
              name="pasaporte"
              :v="vuelidate.pasaporte"
              type="text"
              label="Pasaporte"
            />
            <BaseInput
              v-model="formCreate.fecha_nacimiento"
              :v="vuelidate.fecha_nacimiento"
              type="date"
              label="Nacimiento"
              name="fecha_nacimiento"
            />
            <BaseSelect
              v-model="formCreate.sexo"
              :v="vuelidate.sexo"
              label="Sexo"
              :options="sexOptions"
              name="sexo"
            />
            <BaseSelect
              v-model="formCreate.discapacidad"
              :v="vuelidate.discapacidad"
              label="Discapacidad fisica o mental"
              :options="yesNoOptions"
              name="discapacidad"
            />
            <BaseSelect
              v-model="formCreate.jubilacion"
              :v="vuelidate.jubilacion"
              label="Jubilación"
              :options="yesNoOptions"
              name="jubilacion"
            />
            <BaseSelect
              v-model="formCreate.tipo_sangre"
              :v="vuelidate.tipo_sangre"
              label="Tipo de sangre"
              :options="bloodOptions"
              name="tipo_sangre"
            />
            <BaseSelect
              v-model="formCreate.nacionalidad"
              :v="vuelidate.nacionalidad"
              label="Nacionalidad"
              :options="nationalityOptions"
              name="nacionalidad"
            />
            <BaseSelect
              v-model="formCreate.estado_civil"
              :v="vuelidate.estado_civil"
              label="Estado civil"
              :options="civilStateOptions"
              name="estado_civil"
            />
            <BaseSelect
              v-model="formCreate.carga_civil"
              :v="vuelidate.carga_civil"
              label="Cargar civil"
              :options="cargaCivilOptions"
              name="carga_civil"
            />
          </div>
        </div>

        <div class="form__group">
          <h2>Contacto</h2>
          <div class="two-columns">
            <BaseInput
              v-model="formCreate.celular"
              :v="vuelidate.celular"
              type="text"
              label="Celular"
              name="celular"
            />
            <BaseInput
              v-model="formCreate.telefono_convencional"
              :v="vuelidate.telefono_convencional"
              type="text"
              label="Teléfono convencional"
              name="telefono_convencional"
            />
            <BaseInput
              v-model="formCreate.correo"
              :v="vuelidate.correo"
              type="email"
              label="Correo"
              name="correo"
            />
            <BaseInput
              v-model="formCreate.correo_alternativo"
              :v="vuelidate.correo_alternativo"
              type="email"
              label="Correo alternativo"
              name="correo_alternativo"
            />
            <BaseInput
              v-model="formCreate.coordinador"
              name="coordinador"
              :v="vuelidate.coordinador"
              type="text"
              label="Coordinador"
            />
            <BaseInput
              v-model="formCreate.cedula_coordinador"
              name="cedula_coordinador"
              :v="vuelidate.cedula_coordinador"
              type="text"
              label="Cedula coordinador"
            />
          </div>
        </div>

        <div class="form__group">
          <h2>Datos avanzados</h2>
          <div class="one-column">
            <BaseSelect
              v-model="formCreate.tipo_de_proyecto"
              :v="vuelidate.tipo_de_proyecto"
              name="tipo_de_proyecto"
              label="Tipo de proyecto"
              :options="proyectoOptions"
            />
            <BaseSelect
              v-model="formCreate.tipo_de_servicio"
              :v="vuelidate.tipo_de_servicio"
              name="tipo_de_servicio"
              label="Tipo de servicio"
              :options="tipoServicioOptions"
            />
            <BaseSelect
              v-model="formCreate.ocupacion"
              :v="vuelidate.ocupacion"
              name="ocupacion"
              label="Ocupación"
              :options="ocupationOptions"
            />
            <BaseSelect
              v-model="formCreate.profesion"
              :v="vuelidate.profesion"
              name="profesion"
              label="Profesión"
              :options="profesionOptions"
            />
            <BaseInput
              v-model="formCreate.fecha_de_ingreso_a_la_organizacion"
              :v="vuelidate.fecha_de_ingreso_a_la_organizacion"
              name="fecha_de_ingreso_a_la_organizacion"
              type="date"
              label="Fecha de Ingreso a la Organización"
            />
            <BaseSelect
              v-model="formCreate.pais"
              :v="vuelidate.pais"
              name="pais"
              label="Pais"
              :options="paisOptions"
            />
            <BaseSelect
              v-model="formCreate.ciudad"
              :v="vuelidate.ciudad"
              name="ciudad"
              label="Ciudad"
              :options="ciudadOptions"
            />
            <BaseSelect
              v-model="formCreate.corregimiento"
              :v="vuelidate.corregimiento"
              name="corregimiento"
              label="Corregimiento"
              :options="corregimientoOptions"
            />
            <BaseSelect
              v-model="formCreate.provincia"
              :v="vuelidate.provincia"
              name="provincia"
              label="Provincia"
              :options="provinciaOptions"
            />
            <BaseInput
              v-model="formCreate.departamento"
              :v="vuelidate.departamento"
              name="departamento"
              label="Departamento"
            />
            <BaseInput
              v-model="formCreate.canton"
              :v="vuelidate.canton"
              name="canton"
              label="Cantón"
            />
            <BaseInput
              v-model="formCreate.domicilio1"
              :v="vuelidate.domicilio1"
              name="domicilio1"
              type="text"
              label="Domilicio 1 (opcional)"
            />
            <BaseInput
              v-model="formCreate.domicilio2"
              :v="vuelidate.domicilio2"
              name="domicilio2"
              type="text"
              label="Domilicio 2 (opcional)"
            />
            <BaseInput
              v-model="formCreate.casa"
              :v="vuelidate.casa"
              name="casa"
              type="text"
              label="Casa (opcional)"
            />
            <BaseInput
              v-model="formCreate.pasaje"
              :v="vuelidate.pasaje"
              name="pasaje"
              type="text"
              label="Pasaje (opcional)"
            />
            <BaseInput
              v-model="formCreate.codigo_postal"
              :v="vuelidate.codigo_postal"
              name="codigo_postal"
              type="text"
              label="Código Postal (opcional)"
            />
          </div>
        </div>

        <div class="form__group">
          <h2>Compromisos de pagos</h2>
          <div class="two-columns">
            <BaseInput
              v-model="formCreate.valor_del_contrato"
              name="valor_del_contrato"
              :v="vuelidate.valor_del_contrato"
              type="text"
              label="Valor del contrato"
            />
            <BaseInput
              v-model="formCreate.valor_adendum"
              name="valor_adendum"
              :v="vuelidate.valor_adendum"
              type="text"
              label="Valor Adendum"
            />
            <BaseInput
              v-model="formCreate.valor_cheque"
              name="valor_cheque"
              :v="vuelidate.valor_cheque"
              type="text"
              label="Valor Cheque"
            />
            <BaseInput
              v-model="formCreate.acta_de_adelanto"
              name="acta_de_adelanto"
              :v="vuelidate.acta_de_adelanto"
              type="text"
              label="Acta de adelanto"
            />
            <BaseInput
              v-model="formCreate.acta_de_finiquito"
              name="acta_de_finiquito"
              :v="vuelidate.acta_de_finiquito"
              type="text"
              label="Acta de finiquito"
            />
            <BaseInput
              v-model="formCreate.acta_compromiso_pago"
              name="acta_compromiso_pago"
              :v="vuelidate.acta_compromiso_pago"
              type="text"
              label="Acta de compromiso de pago"
            />
            <BaseInput
              v-model="formCreate.contrato_privado_gestion_intermediacion"
              name="contrato_privado_gestion_intermediacion"
              :v="vuelidate.contrato_privado_gestion_intermediacion"
              type="text"
              label="Contrato de privado de gestión e intermedicación"
            />
            <BaseInput
              v-model="formCreate.pagare"
              name="pagare"
              :v="vuelidate.pagare"
              type="text"
              label="Pagaré"
            />
            <BaseInput
              v-model="formCreate.valor_letra_de_cambio"
              name="valor_letra_de_cambio"
              :v="vuelidate.valor_letra_de_cambio"
              type="text"
              label="Valor letra de cambio"
            />
            <BaseInput
              v-model="formCreate.bono_eficiencia_cumplimiento"
              name="bono_eficiencia_cumplimiento"
              :v="vuelidate.bono_eficiencia_cumplimiento"
              type="text"
              label="Bono eficiencia cumplimiento"
            />
            <BaseInput
              v-model="formCreate.convenio_compensacion"
              name="convenio_compensacion"
              :v="vuelidate.convenio_compensacion"
              type="text"
              label="Convenio compensasion"
            />
            <BaseInput
              v-model="formCreate.certificado_garantia_depositos"
              name="certificado_garantia_depositos"
              :v="vuelidate.certificado_garantia_depositos"
              type="text"
              label="Certificado de garantía y depósitos"
            />
            <BaseInput
              v-model="formCreate.numero_contrato"
              name="numero_contrato"
              :v="vuelidate.numero_contrato"
              type="text"
              label="Numero del contrato"
            />
            <BaseSelect
              v-model="formCreate.declaracion_jurada"
              name="declaracion_jurada"
              :v="vuelidate.declaracion_jurada"
              label="Declaración jurada"
              :options="declaracionOptions"
            />
          </div>
        </div>

        <div class="form__group">
          <h2>Aprobaciones</h2>
          <div class="one-column">
            <h3>Banco 1</h3>
            <BaseInput
              v-model="formCreate.numero_cuenta"
              :v="vuelidate.numero_cuenta"
              name="numero_cuenta"
              type="text"
              label="Número de cuenta"
            />
            <BaseSelect
              v-model="formCreate.banco_cooperativa"
              :v="vuelidate.banco_cooperativa"
              name="banco_cooperativa"
              label="Banco/Cooperativa"
              :options="bankOptions"
            />
            <BaseSelect
              v-model="formCreate.tipo_cuenta"
              :v="vuelidate.tipo_cuenta"
              name="tipo_cuenta"
              label="Tipo de cuenta"
              :options="accountTypeOptions"
            />
            <h3>Banco 2</h3>
            <BaseInput
              v-model="formCreate.numero_cuenta2"
              :v="vuelidate.numero_cuenta2"
              name="numero_cuenta2"
              type="text"
              label="Número de cuenta"
            />
            <BaseSelect
              v-model="formCreate.banco_cooperativa2"
              :v="vuelidate.banco_cooperativa2"
              name="banco_cooperativa2"
              label="Banco/Cooperativa"
              :options="bankOptions"
            />
            <BaseSelect
              v-model="formCreate.tipo_cuenta2"
              :v="vuelidate.tipo_cuenta2"
              name="tipo_cuenta2"
              label="Tipo de cuenta"
              :options="accountTypeOptions"
            />
            <h3>Banco 3</h3>
            <BaseInput
              v-model="formCreate.numero_cuenta3"
              :v="vuelidate.numero_cuenta3"
              name="numero_cuenta3"
              type="text"
              label="Número de cuenta"
            />
            <BaseSelect
              v-model="formCreate.banco_cooperativa3"
              :v="vuelidate.banco_cooperativa3"
              name="banco_cooperativa3"
              label="Banco/Cooperativa"
              :options="bankOptions"
            />
            <BaseSelect
              v-model="formCreate.tipo_cuenta3"
              :v="vuelidate.tipo_cuenta3"
              name="tipo_cuenta3"
              label="Tipo de cuenta"
              :options="accountTypeOptions"
            />
          </div>
        </div>

        <div class="form__group">
          <h2>Beneficiario(s) en caso de fallecimiento</h2>
          <div class="two-columns">
            <BaseInput
              v-model="formCreate.beneficiario1"
              :v="vuelidate.beneficiario1"
              name="beneficiario1"
              class="full-column"
              type="text"
              label="Beneficiario #1"
            />
            <BaseInput
              v-model="formCreate.cedula_beneficiario1"
              :v="vuelidate.cedula_beneficiario1"
              name="cedula_beneficiario1"
              type="text"
              label="Cedula"
            />
            <BaseInput
              v-model="formCreate.pasaporte_beneficiario1"
              :v="vuelidate.pasaporte_beneficiario1"
              name="pasaporte_beneficiario1"
              type="text"
              label="Pasaporte"
            />
            <BaseInput
              v-model="formCreate.nacimiento_beneficiario1"
              :v="vuelidate.nacimiento_beneficiario1"
              name="nacimiento_beneficiario1"
              type="date"
              label="Nacimiento"
            />
            <BaseSelect
              v-model="formCreate.nacionalidad_beneficiario1"
              :v="vuelidate.nacionalidad_beneficiario1"
              name="nacionalidad_beneficiario1"
              label="Nacionalidad"
              :options="nationalityOptions"
            />
            <BaseSelect
              v-model="formCreate.sexo_beneficiario1"
              :v="vuelidate.sexo_beneficiario1"
              name="sexo_beneficiario1"
              label="Sexo"
              :options="sexOptions"
            />
            <BaseSelect
              v-model="formCreate.parentezco_beneficiario1"
              :v="vuelidate.parentezco_beneficiario1"
              name="parentezco_beneficiario1"
              label="Parentesco"
              :options="parentescoOptions"
            />
            <BaseInput
              v-model="formCreate.edad_beneficiario1"
              :v="vuelidate.edad_beneficiario1"
              name="edad_beneficiario1"
              type="number"
              label="Edad"
            />
            <BaseInput
              v-model="formCreate.celular_beneficiario1"
              :v="vuelidate.celular_beneficiario1"
              name="celular_beneficiario1"
              type="number"
              label="Celular"
            />
            <BaseInput
              v-model="formCreate.telefono_convencional_beneficiario1"
              :v="vuelidate.telefono_convencional_beneficiario1"
              name="telefono_convencional_beneficiario1"
              type="number"
              label="Teléfono convencional"
            />
            <BaseInput
              v-model="formCreate.email_beneficiario1"
              :v="vuelidate.email_beneficiario1"
              name="email_beneficiario1"
              type="email"
              label="Correo"
            />
            <BaseInput
              v-model="formCreate.domicilio_beneficiario1"
              :v="vuelidate.domicilio_beneficiario1"
              name="domicilio_beneficiario1"
              type="text"
              label="Domicilio"
            />

            <BaseInput
              v-model="formCreate.beneficiario2"
              :v="vuelidate.beneficiario2"
              name="beneficiario2"
              class="full-column"
              type="text"
              label="Beneficiario #2"
            />
            <BaseInput
              v-model="formCreate.cedula_beneficiario2"
              :v="vuelidate.cedula_beneficiario2"
              name="cedula_beneficiario2"
              type="text"
              label="Cedula"
            />
            <BaseInput
              v-model="formCreate.pasaporte_beneficiario2"
              :v="vuelidate.pasaporte_beneficiario2"
              name="pasaporte_beneficiario2"
              type="text"
              label="Pasaporte"
            />
            <BaseInput
              v-model="formCreate.nacimiento_beneficiario2"
              :v="vuelidate.nacimiento_beneficiario2"
              name="nacimiento_beneficiario2"
              type="date"
              label="Nacimiento"
            />
            <BaseSelect
              v-model="formCreate.nacionalidad_beneficiario2"
              :v="vuelidate.nacionalidad_beneficiario2"
              name="nacionalidad_beneficiario2"
              label="Nacionalidad"
              :options="nationalityOptions"
            />
            <BaseSelect
              v-model="formCreate.sexo_beneficiario2"
              :v="vuelidate.sexo_beneficiario2"
              name="sexo_beneficiario2"
              label="Sexo"
              :options="sexOptions"
            />
            <BaseSelect
              v-model="formCreate.parentezco_beneficiario2"
              :v="vuelidate.parentezco_beneficiario2"
              name="parentezco_beneficiario2"
              label="Parentesco"
              :options="parentescoOptions"
            />
            <BaseInput
              v-model="formCreate.edad_beneficiario2"
              :v="vuelidate.edad_beneficiario2"
              name="edad_beneficiario2"
              type="number"
              label="Edad"
            />
            <BaseInput
              v-model="formCreate.celular_beneficiario2"
              :v="vuelidate.celular_beneficiario2"
              name="celular_beneficiario2"
              type="number"
              label="Celular"
            />
            <BaseInput
              v-model="formCreate.telefono_convencional_beneficiario2"
              :v="vuelidate.telefono_convencional_beneficiario2"
              name="telefono_convencional_beneficiario2"
              type="number"
              label="Teléfono convencional"
            />
            <BaseInput
              v-model="formCreate.email_beneficiario2"
              :v="vuelidate.email_beneficiario2"
              name="email_beneficiario2"
              type="email"
              label="Correo"
            />
            <BaseInput
              v-model="formCreate.domicilio_beneficiario2"
              :v="vuelidate.domicilio_beneficiario2"
              name="domicilio_beneficiario2"
              type="text"
              label="Domicilio"
            />

            <BaseInput
              v-model="formCreate.beneficiario3"
              :v="vuelidate.beneficiario3"
              name="beneficiario3"
              class="full-column"
              type="text"
              label="Beneficiario #3"
            />
            <BaseInput
              v-model="formCreate.cedula_beneficiario3"
              :v="vuelidate.cedula_beneficiario3"
              name="cedula_beneficiario3"
              type="text"
              label="Cedula"
            />
            <BaseInput
              v-model="formCreate.pasaporte_beneficiario3"
              :v="vuelidate.pasaporte_beneficiario3"
              name="pasaporte_beneficiario3"
              type="text"
              label="Pasaporte"
            />
            <BaseInput
              v-model="formCreate.nacimiento_beneficiario3"
              :v="vuelidate.nacimiento_beneficiario3"
              name="nacimiento_beneficiario3"
              type="date"
              label="Nacimiento"
            />
            <BaseSelect
              v-model="formCreate.nacionalidad_beneficiario3"
              :v="vuelidate.nacionalidad_beneficiario3"
              name="nacionalidad_beneficiario3"
              label="Nacionalidad"
              :options="nationalityOptions"
            />
            <BaseSelect
              v-model="formCreate.sexo_beneficiario3"
              :v="vuelidate.sexo_beneficiario3"
              name="sexo_beneficiario3"
              label="Sexo"
              :options="sexOptions"
            />
            <BaseSelect
              v-model="formCreate.parentezco_beneficiario3"
              :v="vuelidate.parentezco_beneficiario3"
              name="parentezco_beneficiario3"
              label="Parentesco"
              :options="parentescoOptions"
            />
            <BaseInput
              v-model="formCreate.edad_beneficiario3"
              :v="vuelidate.edad_beneficiario3"
              name="edad_beneficiario3"
              type="number"
              label="Edad"
            />
            <BaseInput
              v-model="formCreate.celular_beneficiario3"
              :v="vuelidate.celular_beneficiario3"
              name="celular_beneficiario3"
              type="number"
              label="Celular"
            />
            <BaseInput
              v-model="formCreate.telefono_convencional_beneficiario3"
              :v="vuelidate.telefono_convencional_beneficiario3"
              name="telefono_convencional_beneficiario3"
              type="number"
              label="Teléfono convencional"
            />
            <BaseInput
              v-model="formCreate.email_beneficiario3"
              :v="vuelidate.email_beneficiario3"
              name="email_beneficiario3"
              type="email"
              label="Correo"
            />
            <BaseInput
              v-model="formCreate.domicilio_beneficiario3"
              :v="vuelidate.domicilio_beneficiario3"
              name="domicilio_beneficiario3"
              type="text"
              label="Domicilio"
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
import { useAuthStore } from "~~/store/auth";
import { useToast } from "vue-toastification";

definePageMeta({
  name: "CreateSociosPage",
  components: {
    BaseInput,
    BaseFileInput,
    BaseSelect,
    ScrollTop,
  },
  layout: "private",
});
const router = useRouter();

const goToUploadDocuments = () => {
  router.push("/socios/subir-documentos");
};

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
const cargaCivilOptions = ref<SelectOption[]>([
  { text: "1", value: "Uno" },
  { text: "2", value: "Dos" },
  { text: "3", value: "Tres" },
  { text: "4", value: "Cuatro" },
  { text: "5", value: "Cinco" },
]);

const formCreate = reactive({
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

const vuelidate = useVuelidate(rules, formCreate);

const {
  public: { baseURL },
} = useRuntimeConfig();

const authStore = useAuthStore();

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
    return;
  }
  const data: { [key: string]: string } = {};
  const formData = new FormData();
  for (const key in formCreate) {
    if (key === "foto") {
      formData.append(`files.${key}`, formCreate[key]);
    }
    if (formCreate[key] !== "" && key !== "foto") {
      data[key] = formCreate[key];
    }
  }
  formData.append("data", JSON.stringify(data));
  const { data: datos, error: errorDatos } = await useFetch(
    `${baseURL}/datos-personales`,
    {
      method: "POST",
      headers: {
        Authorization: `Bearer ${authStore.token}`,
      },
      body: formData,
    }
  );
  if (errorDatos.value) {
    console.log(errorDatos.value);
    formData.delete("data");
    formData.delete("files.foto");
    toast.error("Error al guardar los datos");
    return;
  }
  if (datos.value) {
    const { data: userData, error: userError } = await useFetch(`${baseURL}/users`, {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
        Authorization: `Bearer ${authStore.token}`,
      },
      body: JSON.stringify({
        email: formCreate.correo,
        username: formCreate.cedula_ruc,
        estado: formCreate.status ? StatusRegistry.ACTIVO : StatusRegistry.INACTIVO,
        password: Math.random().toString(36).slice(2),
        datos_personales: datos.value?.id,
      }),
    });
    if (userError.value) {
      console.log(userError.value);
      formData.delete("data");
      formData.delete("files.foto");
      toast.error("Error al guardar los datos");
      return;
    }
    if (userData.value) {
      formData.delete("data");
      formData.delete("files.foto");
      toast.success("Datos guardados correctamente");
      await router.push("/socios?created=true");
    }
  }
  // await $axios.$post('/users', )
};

onBeforeMount(() => {
  if (!authStore.user?.role.type.includes("admin")) {
    router.push("/personal");
    toast.error('Disculpas, usted no esta autorizado en visitar "socios/crear" page');
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
</style>
