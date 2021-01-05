<template>
  <div class="corpo">
    <h1 class="titulo">{{titulo}}</h1>
    <ul class="lista-fotos">
      <li class="lista-fotos-item" v-for="foto of fotos" :key="foto">
        <div class="painel">
          <h2 class="painel-titulo">{{ foto.titulo}}</h2>
          <div class="painel-conteudo">
            <img class="imagem-responsiva" :src="foto.url" :alt="foto.alt">
          </div>
        </div> 
      </li>
    </ul>
  </div>
</template>

<script>
export default {

  data () {
    return {
      titulo: 'Alurapic',
      fotos: []
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

  /* estilo do painel */ 

   .painel {
    padding: 0 auto;
    border: solid 2px grey;
    display: inline-block;
    margin: 5px;
    box-shadow: 5px 5px 10px grey;
    width: 200px;
    height: 100%;
    vertical-align: top;
    text-align: center;
  }

  .painel .painel-titulo {
    text-align: center;
    border: solid 2px;
    background: lightblue;
    margin: 0 0 15px 0;
    padding: 10px;
    text-transform: uppercase;
  }
</style>
