<script setup>
import { usePaymentStore } from '@/store/payment';

const store = usePaymentStore()


</script>

<template #img>
    <ui-header></ui-header>
    <div class="spacer"></div>
    <div class="card">
        <CompanyCard />
    </div>
    <section class="feature">
        <div class="top">
            <div class="top-content">
                <h1>PLAN<span> BLACK</span>
                </h1>
                <p span style="color:black;">Black Plan es una exclusiva membresía de club de autos que ofrece una experiencia premium. Los miembros disfrutan de acceso a una flota de vehículos de lujo, incluyendo deportivos y SUVs de alta gama. Además, cuentan con servicios de mantenimiento y limpieza, asistencia en carretera las 24 horas y entregas a domicilio.  <i class=""></i></p>

            </div>
        </div>
        <div class="bottom">
            <div class="list">
                <h2>Beneficios</h2>
                <ul class="aprenderas-list">
                    <li><i class="fas fa-check"></i> Protección financiera: Un seguro de auto te brinda protección financiera en caso de accidentes, daños al vehículo, lesiones personales o daños a la propiedad de terceros, evitando gastos inesperados y costosos.
                    </li>
                    <li> <i class="fas fa-check"></i>Cumplimiento legal: En la mayoría de los lugares, tener un seguro de auto es un requisito legal. Cumplir con esta obligación te ayuda a evitar multas y sanciones legales.</li>
                    <li> <i class="fas fa-check"></i>Paz mental: Saber que estás protegido en caso de un accidente te proporciona tranquilidad mientras conduces y te permite concentrarte en la carretera.<span></span> </li>
                    
                </ul>
            </div>


        </div>

    </section>
    <scroll-top></scroll-top>
    <ui-footer></ui-footer>
</template>

<style scoped lang="scss">
body {
    position: relative;
}


section.feature {
    width: 100%;
    margin-top: -1rem;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    position: relative;
    overflow: hidden;

    @media (width < 1024px) {
        max-width: 1000px;
    }

    .top {
        width: 100%;
        background-color:#FBF8FF;
        height: 400px;
        display: flex;
        justify-content: center;
        align-items: flex-start;
        padding: 2rem;
        flex-direction: column;

        @media (width < 1024px) {
            height: 500px;
        }

        .top-content {
            width: 60%;

            @media (width < 1024px) {
                width: 80%;
            }

            @media (width < 768px) {
                width: 100%;
            }

            h1 {
                font-size: 2rem;
                color: #000000;

                @media (width < 640px) {
                    font-size: 1.5rem;
                }

                span {
                    font-weight: 800;
                }
            }

            p {
                color: white;
                margin: 2rem auto;

                @media (width < 640px) {
                    font-size: 12px;
                }

            }

            .rating {
                display: flex;
                color: white;

                @media (width < 640px) {
                    flex-direction: column;
                    justify-content: center;
                    align-items: center;
                }

                span {
                    margin: 0rem 1rem;

                    &.bold,
                    &.fa-star {
                        margin: 0 4px;
                        font-weight: 600;
                    }

                    &.fa-star {
                        color: red;
                    }
                }

                .user-icon {
                    background-color: black;
                    border-radius: 50%;
                    color: red;
                    width: 30px;
                    height: 30px;
                    display: flex;
                    justify-content: center;
                    align-items: center;
                }

            }
        }

    }

    .bottom {
        padding: 2rem 6rem;
        margin: 1rem auto;
        width: 100%;

        @media (width <=1280px) {
            padding: 1rem;
        }

        h2 {
            font-size: 2rem;
            margin: 1rem auto;
            text-decoration: underline;
            font-weight: 600;

            @media (width < 640px) {
                font-size: 1.5rem;
            }

        }

        .list {

            .aprenderas-list {
                margin-left: 2rem;

                @media (width < 450px) {
                    margin-left: 1rem;
                    width: 330px;
                }


                li {
                    font-size: 1rem;
                    margin: 1rem auto;

                    .fa-check {
                        margin-right: 1rem;
                        font-size: 1rem;
                        color: red;

                        @media (width < 450px) {
                            margin-right: 8px;
                        }
                    }

                    span {
                        font-weight: 600;
                    }

                    @media (width < 640px) {
                        font-size: 12px;
                    }

                }
            }
        }

        .bottom-content {
            margin: 2rem 0rem;
            width: 60%;

            @media (width < 1024px) {
                width: 100%;
            }

            h3 {
                font-size: 2.2rem;
                font-weight: 900;
                color: orangered;

                @media (width < 640px) {
                    font-size: 1.3rem;
                }
            }

            p {
                margin: 2rem auto;
                font-size: 1.2rem;

                @media (width < 640px) {
                    font-size: 1rem;
                }

                @media (width < 640px) {
                    font-size: 12px;
                }
            }
        }

        .testimonial {
            display: flex;
            justify-content: space-between;
            align-items: center;
            width: 400px;
            border: 1px solid #b7b3b3;
            border-radius: 6px;
            padding: 8px;

            @media (width < 640px) {
                width: 340px;
            }

            .img {
                width: 20%;

                img {
                    width: 100%;
                    border-radius: 50%;
                    margin-right: 8px;
                }
            }

            .text {
                width: 75%;

                p {
                    margin-bottom: 8px;
                }

                .customer {
                    .name {
                        font-weight: 600;

                        .fa-check-circle {
                            color: green;
                        }
                    }

                    .uv {
                        color: #9d9d9d;
                    }

                }

                .fa-star {
                    color: yellow;
                }
            }

        }
    }
}

.card {
    position: absolute;
    top: 0;
    left: 0;
    top: 20%;
    left: 65%;
    z-index: 111;

    @media (width < 1024px) {
        width: 100%;
        display: flex;
        justify-content: center;
        align-items: center;
        position: relative;
        top: 0;
        left: 0;
        margin: 2rem auto;
    }
}

.spacer {
  height: 15px; /* Altura del espacio entre los divs */
}
</style>