<template>
  
  <div>
    <h1 class="centralizado">{{ titulo }}</h1>
    <p v-show="mensagem" class="centralizado">{{ mensagem }}</p>
    <input type="search" class="filtro" v-on:input="filtro = $event.target.value" placeholder="Filtre por parte do título"></input>
    <ul class="lista-fotos">
        <li class="lista-fotos-item" v-for="foto of fotosComFiltro">
          <meu-painel :titulo="foto.titulo">
            <imagem-responsiva v-meu-transform="15" :url="foto.url" :titulo="foto.titulo"></imagem-responsiva>
            <router-link :to="{ name:'altera', params: { id: foto._id } }">
              <meu-botao tipo="button" rotulo="Alterar"></meu-botao>
            </router-link>
            <meu-botao tipo="button" rotulo="Remover" @botaoAtivado="remove(foto)" estilo="perigo"></meu-botao>
          </meu-painel>   
        </li>
    </ul>
  </div>

</template>

<script>
import Painel from '../shared/painel/Painel';
import ImagemResponsiva from '../shared/imagem-responsiva/ImagemResponsiva';
import Botao from '../shared/botao/Botao';
import FotoService from '../../domain/foto/FotoService.js';

export default {
  
  components:{
    'meu-painel': Painel,
    'imagem-responsiva': ImagemResponsiva,
    'meu-botao': Botao
  },

  data(){
    return{
      titulo: 'VuePics',
      fotos:[],
      filtro: '',
      mensagem: ''
    }
  },

  computed: {
    fotosComFiltro(){
      if(this.filtro){
        let exp = new RegExp(this.filtro.trim(), 'i' );
        return this.fotos.filter(foto => exp.test(foto.titulo));
      }else{
        return this.fotos;
      }
    }
  },

  methods:{
    remove(foto){
      this.service.apaga(foto._id)
          .then(() => {
          let indice = this.fotos.indexOf(foto);
          this.fotos.splice(indice, 1);
          this.mensagem = 'Foto removida com sucesso';

        }, err => {
            console.log(err)
            this.mensagem = 'Nao foi possível remover a foto';
          });        
    }
  },

  created(){
    this.service = new FotoService(this.$resource);
    this.service.lista()
      .then(fotos => this.fotos = fotos, err => console.log(err));
          
  }
  
}
</script>

<style>

  .centralizado {
    text-align: center;
  }

  .lista-fotos {
    list-style: none;
  }

  .lista-fotos .lista-fotos-item {
    display: inline-block;
  }

  .filtro {
    display: block;
    width: 100%;
  }

</style>
