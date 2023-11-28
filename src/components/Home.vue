<template>
  <div class="h-100 background-color">
    <v-responsive class="text-center align-center h-100 fill-height">
      <v-row justify="center">
        <v-col cols="3">
          <v-card color="white">
            <v-row
              ><v-col cols="4">
                <v-img
                  class="ma-3 mx-auto"
                  src="../assets/img/estado-email.png"
                  height="100"
                  width="100"
                />
              </v-col>
              <v-col class="d-flex">
                <p class="ma-auto text-h5">Sorteio</p>
              </v-col>
              <v-col cols="4">
                <v-img
                  class="ma-3 mx-auto"
                  src="../assets/img/sgto-logo.png"
                  height="110"
                  width="110"
                />
              </v-col>
            </v-row>
            <v-row>
              <v-col cols="12">
                <v-col class="pb-0">
                  <v-text-field
                    v-model="participantes"
                    class="px-3"
                    type="number"
                    label="Quantidade de participantes"
                    variant="outlined"
                    placeholder="Insira a quantidade"
                  ></v-text-field>
                </v-col>
                <v-col>{{}}</v-col>
                <v-col class="pt-0">
                  <v-btn @click="teste()" class="text-capitalize">
                    Sortear
                  </v-btn>
                </v-col>
              </v-col>
            </v-row>
          </v-card>
        </v-col>
      </v-row>
    </v-responsive>
  </div>
</template>

<script lang="ts" setup>
import { ref } from "vue";

const participantes = ref("");

const sorteado = [];
const maximoParticipantes = participantes;

const teste = () => {
  const numeroSorteado = Math.ceil(Math.random() * maximoParticipantes.value);
  sorteado.push(numeroSorteado);
  console.log(numeroSorteado);
};
</script>
<style>
.background-color {
  background-image: url("../assets/img/background.jpg");
  background-repeat: no-repeat;
  background-size: cover;
}
</style>
