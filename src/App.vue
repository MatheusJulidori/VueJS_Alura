<template>
  <div id="app">
    <h1>{{titulo}}</h1>
    <ul>
      <li v-for="foto of fotos" :key="foto">
        <img :src="foto.url" :alt="foto.alt">
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
  li{
    list-style:none;
  }
  img{
    width: 400px;
  }
</style>
