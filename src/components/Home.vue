<template>
  <div class="h-100 background-imagem">
    <v-responsive class="text-center align-center h-100">
      <v-row justify="center">
        <v-col cols="10">
          <v-form ref="submmit" @submit.prevent="submmitNumber">
            <v-card variant="flat" color="transparent">
              <v-row
                class="transparent-item ml-10 mb-16 pb-10"
                style="font-family: Poppins !important"
                ><v-col cols="4">
                  <v-img
                    class="ma-3 mt-6 mx-auto logo-tictalk"
                    src="../assets/img/logo-tictalk.svg"
                    height="170"
                    width="auto"
                  />
                </v-col>
                <v-col cols="4" class="d-flex px-0">
                  <p
                    class="ma-auto text-h1 font-text-custom font-weight-bold text-color"
                  >
                    SORTEIO
                  </p>
                </v-col>
                <v-col cols="4">
                  <v-img
                    class="ma-3 my-6 mx-auto logo-sgto"
                    src="../assets/img/sgto-logo.png"
                    height="180"
                    width="auto"
                  />
                </v-col>
              </v-row>
              <v-row class="transparent-item">
                <v-col cols="12" class="pa-0">
                  <v-col cols="7" class="pb-0 px-0 mx-auto" v-if="input">
                    <span
                      class="text-color font-text-custom titulo-input font-weight-bold text-h2"
                    >
                      Quantidade de participantes
                    </span>
                    <v-text-field
                      v-model="participantes"
                      class="px-0 pt-5"
                      type="number"
                      base-color="white"
                      color="white"
                      variant="outlined"
                    ></v-text-field>
                  </v-col>

                  <v-col cols="2" class="pt-0 mx-auto" v-if="botao">
                    <v-btn
                      size="50"
                      :block="true"
                      @click="iniciarSorteio()"
                      type="submit"
                      class="text-capitalize d-flex mx-auto text-h4 mt-3"
                    >
                      Sortear
                    </v-btn>
                  </v-col>
                  <v-col v-if="numeroSorteadoExibir">
                    <p
                      class="text-color titulo-input titulo-sorteio font-weight-bold text-h3"
                    >
                      O Numero sorteado foi:
                    </p>
                    <p
                      class="pt-4 numero-sorteado titulo-sorteio font-weight-bold text-color"
                    >
                      {{ numeroSorteadoExibir }}
                    </p>
                  </v-col>
                  <v-col cols="4" class="mx-auto" v-if="botaoVoltar">
                    <v-btn
                      size="70"
                      @click="voltar()"
                      :block="true"
                      class="text-capitalize text-h4 justify-center"
                    >
                      Sortear Novamente
                    </v-btn>
                  </v-col>
                </v-col>
              </v-row>
            </v-card>
          </v-form>
        </v-col>
      </v-row>
    </v-responsive>
  </div>
</template>

<script lang="ts" setup>
import { ref } from "vue";

const participantes = ref("");
const submmit = ref(null);
var numeroSorteadoExibir = ref("");
var input = ref(true);
var botao = ref(true);
var botaoVoltar = ref(false);

const iniciarSorteio = async () => {
  const valid = await submmit.value.validate();
  if (valid) {
    input.value = !input.value;
    botao.value = !botao.value;
    botaoVoltar.value = true;
    const numeroMaximo = participantes.value;
    const tempoSorteio = 5000;
    const numeroSorteado = await numerosAleatorios(numeroMaximo, tempoSorteio);
    numeroSorteadoExibir.value = numeroSorteado;
  }
};

const voltar = () => {
  input.value = !input.value;
  botao.value = !botao.value;
  botaoVoltar.value = !botaoVoltar.value;
  numeroSorteadoExibir.value = !numeroSorteadoExibir.value;
};

// const campoObrigatorio = () => {
//   if (participantes.value === "") {
//     input.value = true;
//     botao.value = true;
//     return "Este campo é obrigatório";
//   }
// };

const numerosAleatorios = (numeroMaximo: number, tempoSorteio: number) => {
  return new Promise((resolve) => {
    const intervalo = 100;
    let steps = tempoSorteio / intervalo;

    const intervaloId = setInterval(() => {
      const numeroSorteado = Math.ceil(Math.random() * numeroMaximo);
      numeroSorteadoExibir.value = numeroSorteado.toString();

      if (--steps === 0) {
        clearInterval(intervaloId);
        resolve(numeroSorteado);
      }
    }, intervalo);
  });
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@600&display=swap");
* {
  font-family: "Poppins", sans-serif !important;
  overflow: hidden !important;
}

.background-imagem {
  background-image: url("../assets/img/Background.png");
  background-repeat: no-repeat;
  background-size: cover;
}

.v-messages__message {
  color: white;
  font-size: 16px;
}

.text-color {
  color: white !important;
}

input[type="number"]::-webkit-inner-spin-button {
  -webkit-appearance: none;
}

.logo-tictalk {
  filter: drop-shadow(2px 2px 5px rgba(0, 0, 0, 0.4));
}

.logo-sgto {
  filter: drop-shadow(2px 2px 10px rgba(0, 0, 0, 1));
}

.titulo-sorteio {
  filter: drop-shadow(0 0 0.75rem black);
}
.titulo-input {
  filter: drop-shadow(2px 2px 5px rgba(0, 0, 0, 1));
}
.font-text-custom {
  font-family: "Poppins", sans-serif !important;
}
.v-field__input {
  color: rgb(10, 235, 10) !important;
  font-size: 100px;
  font-weight: bold;
  text-align: center;
  margin: 0 auto;
}
.numero-sorteado {
  color: rgb(10, 235, 10) !important;
  font-size: 150px;
  font-weight: bold;
  text-align: center;
  margin: 0 auto;
}
</style>
