<template>

  <div>
    <h1>{{ titulo }}</h1>

    <ul>
        <li v-for="foto of fotos">
            <img :src="foto.url" :alt="foto.titulo">
        </li>
    </ul>

  </div>

</template>

<script>
export default {
  data(){
    return{
      titulo: 'VuePics',
      fotos:[
        {
          url: 'http://tudosobrecachorros.com.br/wp-content/uploads/cachorro-independente.jpg',
          titulo: 'cachorro'
        },
        {
          url: 'http://tudosobrecachorros.com.br/wp-content/uploads/cachorro-independente.jpg',
          titulo: 'cachorrinho'
        }
      ]
    }
  }
  
}
</script>

<style>

</style>
