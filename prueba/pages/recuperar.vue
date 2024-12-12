<template>
    <div class="login">
        <div class="login__container">
            <div class="login__content">
                <div class="login__text">
                    <img class="logo" src="~/assets/logos/logo_amc_black.png" alt="" />
                    <h1>Bienvenidos a nuestro Club</h1>
                    <p>Introduce tu email para recibir un email para restablecer tu contraseña</p>
                </div>

                <form class="login__form" @submit.prevent="sendForm">
                    <h2>Restablecer contraseña</h2>
                    <BaseInput v-model="formForgot.email" :v="vuelidate.email" label="Correo electronico" for="id"
                        :has-icon="true">
                        <template #img>
                           
                        </template>
                    </BaseInput>
                    <BaseButton type="submit">
                        <template #text> Recuperar contraseña </template>
                    </BaseButton>
                    <NuxtLink class="forgot-login" to="/login">Login</NuxtLink>
                </form>
            </div>
        </div>
        <div class="login__image">
           
        </div>
    </div>
</template>
<script lang="ts" setup>
import useVuelidate from "@vuelidate/core";
import { email, helpers, required } from "@vuelidate/validators";
import { POSITION, useToast } from "vue-toastification";
import BaseButton from "~/components/common/buttons/base-button.vue";
import BaseInput from "~/components/common/inputs/base-input.vue";
import { useAuthStore } from '~/store/auth';
definePageMeta({
    name: "RecuperarPage",
    components: {
        BaseInput,
        BaseButton,
    }
})
const formForgot = reactive({
    email: ''
});

const toast = useToast()
const rules = {
    email: {
        required: helpers.withMessage("Este campo es requerido", required),
        email: helpers.withMessage("Este campo debe ser un correo electrónico", email)
    }
};
const vuelidate = useVuelidate(rules, formForgot)
const authStore = useAuthStore()
const router = useRouter()
const sendForm = async () => {
    try {
        vuelidate.value.$touch();
        if (!await vuelidate.value.$validate()) {
            return;
        }
        const response = await authStore.forgotPassword({
            email: formForgot.email
        })
        if (!response.ok && response.status === 400) {
            toast.error('Ocurrio un error', {
                position: POSITION.BOTTOM_RIGHT,
                timeout: 3000,
                closeOnClick: true,
            })
            return;
        }
        toast.success('Se ha enviado un correo electrónico para restablecer su contraseña', {
            position: POSITION.BOTTOM_RIGHT,
            timeout: 3000,
            closeOnClick: true,
        })
        router.push('/login')
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
    background-image: url("../assets/images/bann_password1.png");
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

.forgot-login{
    color: #2563EB;
    font-style: normal;
    font-weight: 400;
    font-size: 14px;
    line-height: 20px;
    text-decoration: none;
    text-align: left;
  }


@media (max-width: 800px) {
    .login__image {
        display: none;
    }
}
</style>
  