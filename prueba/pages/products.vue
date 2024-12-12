<script setup>
import { usePaymentStore } from '@/store/payment/index.js';
import { useCuponStore } from '@/store/payment/cupon.js'
const store = usePaymentStore()
const cuponStore = useCuponStore()


</script>

<template>
    <ui-header></ui-header>
    <div class="spacer"></div>
    <section class="cart-wrapper">
        <div class="cart">
            <h1>Tu <span class="highlight">carrito</span></h1>

            <CartItems />

            <CartPriceCard class="cards" />

            <div class="total">
                <h3>Tienes un cupon? Haz clic aqui para introducir tu codigo</h3>
                <!-- <div class="discount">
                    <input type="text" placeholder="ingresar cupón" v-model="cuponStore.cuponCode">
                    <button @click="cuponStore.applyCupon">Aplicar cupón</button>
                </div>
                <div class="discount-msg">{{ cuponStore.cuponMessage }}</div> -->

                <CartCupon />

                <div class="subtotal">
                    <span>Subtotal</span>
                    <span> USD $ {{ store.total }}</span>
                </div>

                <div class="total">
                    <span>Total</span>
                    <span>USD $ {{ store.total }}</span>
                </div>
            </div>

        </div>
        <div class="form">
            <div class="payment-icons">
                <img src="@/assets/payment-icons/mastercard-64.png" alt="">
                <img src="@/assets/payment-icons/paypal-48.png" alt="">
                <img src="@/assets/payment-icons/visa-48.png" alt="">
            </div>
            
            <div class="remaining">
                <p>Selecciona tu forma de pago preferida  <span class="bold">Transferencia o Tarjeta</span></p>
            </div>
            <CartForm />
        
        </div>

    </section>
    <CartSecurityCard />
    <scroll-top></scroll-top>
    <ui-footer></ui-footer>
</template>

<style lang="scss" scoped>
.cart-wrapper {
    display: flex;
    width: 100%;
    justify-content: space-around;
    align-items: flex-start;
    margin-bottom: 2rem;
    margin-top: -1rem;
    flex-wrap: wrap;
    padding: 2rem 1rem;
    background-color: rgb(236, 236, 236);


    .form {
        display: flex;
        flex-direction: column;
        justify-content: flex-start;
        align-items: center;
        height: 100%;
        max-width: 500px;

        .text-box {
            width: 100%;
            display: flex;
            justify-content: space-around;
            align-items: center;
            background-color: white;
            padding: 1rem;
            border: 1px solid rgb(145, 145, 145);
            border-radius: 6px;

            img {
                width: 64px;
            }

            p {
                font-size: 10px;
            }
        }

        .payment-icons {
            width: 70%;
            display: flex;
            justify-content: space-around;
            align-items: center;
            margin: 1rem auto;

            img {
                width: 32px;
            }

            p {
                width: 70%;
                margin: 1rem auto;
            }

        }

        .remaining {
            margin-top: 1rem;
            width: 100%;
            background-color: lightyellow;
            padding: 1rem 3rem;
            text-align: center;
            border-radius: 6px;
            font-size: 1rem;

        }
    }
}

.cart {
    max-width: 490px;

    h1 {
        font-weight: 800;
        font-size: 1.5rem;

        .highlight {
            color: #0200AB;
        }
    }


    .cards {
        margin: 1rem auto;
    }

    .total {
        h3 {
            font-weight: 600;
            color: #0200AB;
            margin: 2rem auto 8px auto;
        }

        // .discount {
        //     display: flex;
        //     width: 100%;
        //     justify-content: space-between;
        //     align-items: center;



        //     input {
        //         border-radius: 4px;
        //         width: 100%;
        //         margin-right: 4px;

        //         @media (width < 640px) {
        //             width: 85%;
        //         }
        //     }

        //     button {
        //         width: 50%;
        //         padding: 1.4rem 1rem;
        //         font-size: 1rem;
        //         background-color: #148162;
        //         color: white;
        //         border-radius: 4px;
        //         display: flex;
        //         justify-content: center;
        //         align-items: center;

        //         @media (width < 640px) {
        //             width: 85%;
        //         }
        //     }
        // }

        // .discount-msg {
        //     font-size: 14px;
        //     margin-top: 4px;
        // }

        .subtotal,
        .total {
            width: 100%;
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin: 1rem auto;
        }

        .total {
            span {
                font-weight: 600;
                font-size: 1.1em;
            }
        }
    }

    .list-wrapper {
        margin: 2rem auto;

        h2 {
            font-size: 1.2rem;
            font-weight: bold;
        }

        .comprando-list {
            margin-left: 1rem;

            li {
                font-size: 14px;
                margin: 1rem auto;

                .fa-check {
                    margin-right: 8px;
                    font-size: 1rem;

                }
            }
        }
    }
}

.spacer {
  height: 15px; /* Altura del espacio entre los divs */
}
</style>