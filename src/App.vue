<template>
  <div class="corpo">
    <h1 class="titulo">{{titulo}}</h1>

    <input type="search" class="filtro" @input="filtro = $event.target.value" placeholder="Procure uma foto">
    <ul class="lista-fotos">
      <li class="lista-fotos-item" v-for="foto of fotosComFiltro" :key="foto">

        <meu-painel :titulo="foto.titulo">
          <imagem-responsiva :url="foto.url" :titulo="foto.titulo"/>
        </meu-painel>

      </li>
    </ul>
  </div>
</template>

<script>

import Painel from './components/shared/painel/Painel.vue';
import ImagemResponsiva from './components/shared/imagem-responsiva/ImagemResponsiva.vue';

export default {

  components:{
    'meu-painel': Painel,
    'imagem-responsiva': ImagemResponsiva
  },

  data () {
    return {
      titulo: 'Alurapic',
      fotos: [],
      filtro: ''
    }
  },

  computed:{
    fotosComFiltro(){
      if(this.filtro){
        let exp = new RegExp(this.filtro.trim(), 'i');
        return this.fotos.filter(foto => exp.test(foto.titulo));
      }
      else{
        return this.fotos;
      }
    }
  },

  created(){
    let promise = this.$http.get('http://localhost:3000/v1/fotos/')
      .then(response => response.json())//Devolve a resposta em formato JSON
      .then(fotos => this.fotos = fotos, error => console.log(error))//Pega o JSON e seleciona só a lista de fotos
  }
    

}
</script>

<style>

  .titulo {
    text-align: center;
  }

  .filtro {
    display:block;
    width:100%;
  }

  .corpo {
    font-family: Helvetica, sans-serif;
    margin: 0 auto;
    width: 96%;
  }

  .lista-fotos {
    list-style: none;
  }

  .lista-fotos .lista-fotos-item {
    display: inline-block;
  }

  .imagem-responsiva {
    width: 100%;
  }
</style>
