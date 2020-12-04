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
  name: 'app',
  data () {
    return {
      titulo: 'Alurapic',
      fotos: [
        {
          url: 'https://conteudo.imguol.com.br/c/entretenimento/54/2020/04/28/cachorro-pug-1588098472110_v2_450x337.jpg',
          alt: 'cachorro pug'
        },
        {
          url: 'https://www.incorposul.com.br/wp-content/uploads/2019/08/cropped-cachorros-em-apartamentos-01-1024x576.jpg',
          alt: 'cachorro bdf'
        }
      ]
    }
  }
}
</script>

<style>
  li{
    list-style:none;
  }
</style>
