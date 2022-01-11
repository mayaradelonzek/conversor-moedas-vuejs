<template>
  <b-row class="justify-content-md-center" align-h="center">
    <b-col md="3" class="mb-5">
      <b-card class="text-center mt-5" bg-variant="light">
        <b-card-text>          
          <p class="templateReal mt-4">R$ {{ this.formatarMoeda(moedaSelecionada.ask) }}</p>
          <p>Cotação do <strong>{{ moedaSelecionada.code }}</strong> hoje</p>
          <p class="templateMoeda">Moeda:</p>
          <SelectCurrency :obterMoedaSelecionada = "obterMoedaSelecionada"/>
        </b-card-text>
      </b-card>
    </b-col>    
  </b-row>
</template>

<script>
import SelectCurrency from './SelectCurrency.vue';
export default {
  name: "Card",
  components: {
    SelectCurrency,
  },
  data() {
    return { 
      moedaSelecionada: "",
    }
  },
  props: {
    getMoedaSelecionada: Function,
    formatarMoeda: Function,
  },
  methods: {
    obterMoedaSelecionada: function(moedaSelecionada) {
      this.moedaSelecionada = moedaSelecionada;
    },    
        
  },
  updated: function () {
    this.getMoedaSelecionada(this.moedaSelecionada);
  },
};
</script>

<style>
.templateReal {
  font-size: 2em;
  font-weight: bold;
  line-height: 30px;
}

.templateMoeda {
  margin-bottom: 5px;
}
</style>