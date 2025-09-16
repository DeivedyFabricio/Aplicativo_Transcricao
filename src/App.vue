<script setup>
import { ref, computed } from 'vue'

// Entrada digitada
const entrada = ref('')

// Transforma em array de letras maiúsculas
const letrasTransformadas = computed(() => {
  return entrada.value
    .split('')
    .map(l => l.toUpperCase())
})

// Cada letra agora é uma MATRIZ (linhas e colunas)
const mapaLetras = {
  A: [
    ["bloco_preto", "bloco_preto", "bloco_preto"],
    ["bloco_preto", "bloco_verde", "bloco_preto"],
    ["bloco_preto", "bloco_preto", "bloco_preto"],
    ["bloco_preto", "bloco_verde", "bloco_preto"],
    ["bloco_preto", "bloco_verde", "bloco_preto"]
  ],
  B: [
    ["bloco_preto", "bloco_preto", "bloco_verde"],
    ["bloco_preto", "bloco_verde", "bloco_preto"],
    ["bloco_preto", "bloco_preto", "bloco_verde"],
    ["bloco_preto", "bloco_verde", "bloco_preto"],
    ["bloco_preto", "bloco_preto", "bloco_verde"]
  ],
  C: [
    ["bloco_preto", "bloco_preto", "bloco_preto"],
    ["bloco_preto", "bloco_verde", "bloco_verde"],
    ["bloco_preto", "bloco_verde", "bloco_verde"],
    ["bloco_preto", "bloco_verde", "bloco_verde"],
    ["bloco_preto", "bloco_preto", "bloco_preto"]
  ]
}
</script>

<template>
  <div style="background-color: gray; padding: 10px; border-radius: 3px;">
    <h1 style="color:goldenrod;">Transcrição de Letras</h1>
    <h2 style="color:black;">Transforma letras comuns em letras formados por pixel, A, B e C.</h2>
    <input v-model="entrada" placeholder="Digite algo" class="caixa" />
    <div class="campo">
      <div v-for="(letra, index) in letrasTransformadas" :key="index" class="letra">
        <template v-if="mapaLetras[letra]">
          <div v-for="(linha, i) in mapaLetras[letra]" :key="i" class="linha">
            <div
              v-for="(cor, j) in linha"
              :key="j"
              :class="cor"
            ></div>
          </div>
        </template>
        <span v-else>{{ letra }}</span>
      </div>
    </div>
  </div>
</template>

<style scoped>
.bloco_preto {
  width: 15px;
  height: 15px;
  background-color: rgb(0, 0, 0);
  display: inline-block;
  margin-right: 10px;
}

.bloco_verde {
  width: 15px;
  height: 15px;
  background-color: darkgreen;
  display: inline-block;
  margin-right: 10px;
}


.campo {
  background-color: darkgreen;
  height: 100px;
  display: grid;
  grid-template-rows: repeat(1, 0px);
  grid-auto-flow: column;               
  gap: 15px;
  padding: 30px;
  border-radius: 3px;
}

.caixa {
  background-color: rgb(94, 94, 94);           
  padding: 10px;
  border-radius: 3px;
  margin: 10px;
}

</style>
