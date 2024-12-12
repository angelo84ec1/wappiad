<template>
  <div>
    <div class="login">
      <div class="login__container">
        <div class="login__content">
          <div class="login__text">
            <img class="logo" src="~/assets/logos/logo_amc_black.png" alt="" />
            <h2>Ingresar tu usuario y contraseña</h2>
            <p>
              No estas registrado ? Registrarse !
            </p>
          </div>

          <form class="login__form" @submit.prevent="login">
            <h2>Iniciar sesión</h2>
            <BaseSelect v-model="formLogin.documentType" :v="vuelidate.documentType" label="Tipo de identificación"
              for="tipo de identificacion" :options="options" />
            <BaseInput v-model="formLogin.idDocument" :v="vuelidate.idDocument" label="Identificación" for="id"
              :has-icon="true"
              placeholder="Ingrese su Cédula, Ruc o Pasaporte"
              >
              <template #img>
                <img src="~/assets/images/account_rosado.png" alt="User icon" />
              </template>
            </BaseInput>
            <div>
              <BaseInput v-model="formLogin.password"
                label="Contraseña"
                for="password"
                name="password"
                :has-icon="true"
                placeholder="Ingrese su contraseña "
                :type="showPassword ? 'text' : 'password'">
                <template #img>
                  <img src="~/assets/images/Password.png" alt="Left icon" />
                </template>
                <template #img-right>

                </template>
              </BaseInput>
            </div>
            <BaseButton type="submit" :disabled="loading">
              <template #text>
                <span v-if="loading">
                  <Loader />
                </span>
                <span v-else>
                  Iniciar sesión
                </span>
              </template>
            </BaseButton>
            <NuxtLink class="forgot-password-link" to="/recuperar">¿Olvidaste tu contraseña?</NuxtLink>
            <NuxtLink class="forgot-password-link" to="/crearcuenta">Crear Cuenta</NuxtLink>
          </form>
        </div>
      </div>
      <div class="login__image">
        <!-- <span>Emprende este nuevo viaje al portal del futuro</span> -->
      </div>
    </div>
    <AccountNotExistModal v-if="showModal" @close="hideAccountNotExistModal" @action="sendMailto" />
  </div>
</template>

<script lang="ts" setup>
import useVuelidate from "@vuelidate/core";
import { helpers, required } from "@vuelidate/validators";
import { POSITION, useToast } from "vue-toastification";
import BaseButton from "~/components/common/buttons/base-button.vue";
import BaseInput from "~/components/common/inputs/base-input.vue";
import BaseSelect from "~/components/common/inputs/base-select.vue";
import Loader from "~/components/login/Loader.vue";
import { useAuthStore } from '~/store/auth';
import { defineComponent, ref, reactive } from 'vue'; // Importa las utilidades de Vue
import AccountNotExistModal from "~/components/login/AccountNotExistModal.vue";
definePageMeta({
  name: "LoginPage",
  components: {
    BaseInput,
    BaseSelect,
    BaseButton,
    AccountNotExistModal,
    Loader
  },
})

const options = ref([
  { text: "Pasaporte", value: "pasaporte" },
  { text: "Cedula", value: "cedula" },
  { text: "RUC", value: "ruc" },
]);
const formLogin = reactive({
  documentType: 'pasaporte',
  idDocument: '',
  password: '',
});


const showPassword = ref(false); // Define la referencia para mostrar/ocultar contraseña
const loading = ref(false); // Define la referencia para mostrar/ocultar el loader

const togglePasswordVisibility = () => {
  showPassword.value = !showPassword.value;
};

const showModal = ref(false)

const showAccountNotExistModal = () => {
  showModal.value = true
}

const hideAccountNotExistModal = () => {
  showModal.value = false
}

const { public: { MAILTO } } = useRuntimeConfig()

const sendMailto = () => {
  window.open(`mailto:${MAILTO}`)
}

const toast = useToast()
const rules = {
  documentType: {
    required: helpers.withMessage("El tipo de documento es requerido", required),
  },
  idDocument: {
    required: helpers.withMessage("El documento es requerido", required),
  },
  password: {
    required: helpers.withMessage("La contraseña es requerida", required),
  },
};
const vuelidate = useVuelidate(rules, formLogin)
const authStore = useAuthStore()
const router = useRouter()
if (authStore.isAuthenticated) {
    router.push({ path: "/" })
}
const login = async () => {
  try {
    vuelidate.value.$touch();
    if (!await vuelidate.value.$validate()) {
      return;
    }
    loading.value = true; // Show the loader
    const { response, data } = await authStore.login({
      documentType: formLogin.documentType,
      identifier: formLogin.idDocument,
      password: formLogin.password,
    })
    if (response.status === 400) {
      if (data.message[0].messages[0].id === "Auth.form.error.account.not-exist") {
        showAccountNotExistModal()
        return;
      }
      if (data.message[0].messages[0].id === "Auth.form.error.invalid") {
        toast.error('Usuario o contraseña incorrectos', {
          position: POSITION.BOTTOM_RIGHT,
          timeout: 3000,
          closeOnClick: true,
        })
        return;
      }
    }
    if (authStore.getUser?.role.name === 'admin' || authStore.getUser?.role.name === 'digitador') {
      await router.push('/usuarios')
    } else {
      await router.push('/resumen')
    }
  } catch (error) {
    console.error(error);
  } finally {
    loading.value = false; // Hide the loader
  }
}
</script>

<style scoped>
.login {
  display: flex;
  min-height: 100vh;
}

.login>* {
  flex: 50% 1;
}

.login__content {
  max-width: 423px;
}

.login__container {
  display: grid;
  place-items: center;
  padding: 1rem;
}

.logo {
  width: 250px;
  height: auto;
}

.login__text {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.login__form {
  margin-top: 2rem;
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.login__image {
  text-align: center;
  display: flex;
  justify-content: center;
  align-items: flex-end;
  padding: 1rem;
  background-image: url("../assets/images/groupini.png");
  background-repeat: no-repeat;
  background-size: cover;
}

.login__image>span {
  font-size: var(--heading-2);
  line-height: var(--heading-line-height);
  color: var(--white);
  max-width: 497px;
}

.forgot-password-link {
  color: #2563EB;
  font-style: normal;
  font-weight: 400;
  font-size: 14px;
  line-height: 20px;
  text-decoration: none;
}


@media (max-width: 800px) {
  .login__image {
    display: none;
  }
}
</style>
