<script lang="ts" setup>
import { Play, Pause } from "lucide-vue-next";
</script>

<template>
  <div class="is-flex is-align-items-center is-justify-content-space-between">
    <Cronometro :tempoEmSegundos="tempoEmSegundos" />
    <Button 
    :text="'Play'"
    :clickEvent="iniciar"
    :buttonState="!cronometroRodando"
    :icon="Play"/>
    <Button
      :text="'Pause'"
      :clickEvent="finalizar"
      :buttonState="cronometroRodando"
      :icon="Pause"
    />
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import Cronometro from "../components/Cronometro.vue";
import Button from "../components/Button.vue";

export default defineComponent({
  name: "Temporizador",
  emits: ["aoTemporizadorFinalizado"],
  components: {
    Cronometro,
    Button,
  },
  data() {
    return {
      tempoEmSegundos: 0,
      cronometro: 0,
      cronometroRodando: false,
    };
  },
  methods: {
    iniciar(): void {
      this.cronometroRodando = true;
      this.cronometro = setInterval(() => {
        this.tempoEmSegundos++;
      }, 1000);
    },
    finalizar(): void {
      this.cronometroRodando = false;
      clearInterval(this.cronometro);
      this.$emit("aoTemporizadorFinalizado", this.tempoEmSegundos);
      this.tempoEmSegundos = 0;
    },
  },
});
</script>

<style scoped></style>

