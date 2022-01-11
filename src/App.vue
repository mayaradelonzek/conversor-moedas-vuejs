<template>
  <div id="app">
    <Header/>
    <b-container >
      <Card :getMoedaSelecionada="getMoedaSelecionada"
            :formatarMoeda="formatarMoeda" />
      <Form :moedaSelecionada="moedaSelecionada.code"
            :cotacaoReal="Number(moedaSelecionada.ask)"
            :formatarMoeda="formatarMoeda" />
    </b-container>    
  </div>
</template>

<script>
import Header from './components/Header.vue';
import Card from './components/Card.vue';
import Form from './components/Form.vue';

export default {
  name: 'App',
  components: {
    Header,
    Card,
    Form
  },
  data: function () {
    return {
      moedaSelecionada: "",
    };
  },
  methods: {
    getMoedaSelecionada: function (moedaSelecionada) {
      this.moedaSelecionada = moedaSelecionada;
    },
    formatarMoeda: function(moedaParaFormatar) {
      return parseFloat(moedaParaFormatar).toFixed(2).replace('.', ',');
    }
  },
}
</script>

<style>
</style>
