<script setup lang="ts">
import {ref, onMounted } from 'vue';
import CardPadrao from '@/components/CardPadrao.vue';

  const personagens = ref([]); //variável reativa

  //async - porque essa função faz uma conexão externa e o valor demora
  async function buscarPersonagens(){
    try{
    //await porque a conexão demora, logo é necessário esperar
    const resposta = await fetch("https://rickandmortyapi.com/api/character");
    const dados = await resposta.json();
    personagens.value = dados.results;
  }catch(erro){
    console.error('Erro com a conexão com a API')
  }
}
  onMounted(buscarPersonagens);

</script>
<template>
  <h2>Rick and Morty</h2>
  <section>
    <CardPadrao v-for="item in personagens"
    :key="item.id"
    :titulo="item.name"
    :subtitulo="item.species"
    :imagem="item.image"
    />
  </section>
</template>
<style scoped>
  section{
    display: flex;
    flex-wrap: wrap;
  }
</style>