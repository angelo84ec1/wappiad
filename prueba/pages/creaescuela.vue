<template>
    <Loading v-if="authStore.loading" />
    <div v-else>
      <div class="login">
        <div class="login__container">
          <div class="login__content">
            <div class="login__text">
              <img class="logo" src="~/assets/logos/logo_amc_black.png" alt="" />
              <h1>Ingresar tu usuario y contraseña</h1>
              <p>
                No estas registrado ?   Registrarse !
              </p>
            </div>
  
            <form class="login__form" @submit.prevent="login">
              <h2>Iniciar sesión</h2>
              <BaseSelect v-model="formLogin.documentType" :v="vuelidate.documentType" label="Tipo de identificación"
                for="tipo de identificacion" :options="options" />
              <BaseInput v-model="formLogin.idDocument" :v="vuelidate.idDocument" label="Identificación" for="id"
                :has-icon="true">
                <template #img>
                 
                </template>
              </BaseInput>
              <BaseInput v-model="formLogin.password" :v="vuelidate.password" label="Contraseña" for="password"
                name="password" :has-icon="true" type="password">
                <template #img>
                 
                </template>
              </BaseInput>
              <BaseButton type="submit" class="border-9 hover:bg-purple-600 hover:text-white">
                <template #text> Iniciar sesión </template>
              </BaseButton>
              <NuxtLink class="forgot-password-link" to="/recuperar">¿Olvidaste tu contraseña?</NuxtLink>
              <NuxtLink class="forgot-create-count" to="/crearcuenta">Crear Cuenta</NuxtLink>
            </form>
          </div>
        </div>
        <div class="login__image">
          <span></span>
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
  import { useAuthStore } from '~/store/auth';
  import AccountNotExistModal from "~/components/login/AccountNotExistModal.vue";
  definePageMeta({
    name: "LoginPage",
    components: {
      BaseInput,
      BaseSelect,
      BaseButton,
      AccountNotExistModal
    }
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
  
  const showModal = ref(false)
  // const loading = ref(false)
  
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
  const login = async () => {
    try {
      vuelidate.value.$touch();
      if (!await vuelidate.value.$validate()) {
        return;
      }
      const { response, data } = await authStore.login({
        documentType: formLogin.documentType,
        identifier: formLogin.idDocument,
        password: formLogin.password,
      })
      if (!response.ok && response.status === 400) {
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
      if (authStore.getUser?.role.name === 'admin') {
        await router.push('/usuarios')
      } else {
        await router.push('/resumen')
      }
    } catch (error) {
      console.error(error);
  
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
    max-width: 317px;
  }
  
  .border-9 {
    border: 9px;
  }
  
  
  .forgot-password-link {
    color: #2563EB;
    font-style: normal;
    font-weight: 400;
    font-size: 14px;
    line-height: 20px;
    text-decoration: none;
  
  }
  
  .forgot-create-count {
    color: #2563EB;
    font-style: normal;
    font-weight: 400;
    font-size: 14px;
    line-height: 20px;
    text-decoration: none;
    position: relative;
    top: 0px;
  
  
  }
  
  @media (max-width: 800px) {
    .login__image {
      display: none;
    }
  }
  </style>
  