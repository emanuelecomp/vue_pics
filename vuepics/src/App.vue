<template>
  
  <div class="corpo">
    <meu-menu :rotas="routes"/>
    <router-view></router-view>
  </div>

</template>

<script>
import { routes } from './routes';
import Menu from './components/shared/menu/Menu';

export default {
  components:{
    'meu-menu': Menu
  },
  data(){
    return {
      routes: routes
    }
    
  }
  
}
</script>

<style>
  .corpo {
    font-family: Helvetica, sans-serif;
    margin: 0 auto;
    width: 96%;
  }

</style>
