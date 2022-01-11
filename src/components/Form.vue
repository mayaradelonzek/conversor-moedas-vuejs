<template>
  <section>
    <b-row align-h="center">
      <b-col sm="5">
        <h4 class="mt-5 mb-3">Faça a conversão de valores</h4>
        <b-form-group label="Valor a ser convertido"/>
        <b-input-group>
          <b-input-group-prepend>
            <span class="input-group-text">{{moedaSelecionada}} - $</span>
          </b-input-group-prepend>
          <b-input v-model="valorParaConverter" />
          <b-input-group-append>
            <b-button @click="converterValor" variant="primary">Converter</b-button>
          </b-input-group-append>
        </b-input-group>
        <b-alert class="mt-3" v-model="showDismissibleAlert" variant="danger">
          {{mensagemErro}}
        </b-alert>
      </b-col>
    </b-row>

    <b-row align-h="center">
      <b-col sm="5" class="mt-3">  
        <b-form-group label="Valor em reais"/>      
        <b-input-group prepend="BR - R$">          
          <b-input v-model="valorConvertido" disabled />          
        </b-input-group>
      </b-col>
    </b-row>    
  </section>
</template>

<script>
export default {
  name: "Form",
  data: function () {
    return {
      valorConvertido: 0.0000,
      valorParaConverter: 0.0000,
      mensagemErro: "",
      showDismissibleAlert: false
    };
  },
  props: {
    cotacaoReal: Number,
    moedaSelecionada: String,
    formatarMoeda: Function,
  },
  methods: {
    converterValor: function() {
      this.validarCampoConversao();

      if (this.naoHaErros()) {
        this.valorConvertido = this.formatarMoeda(this.valorParaConverter * this.cotacaoReal);
      }
    },
    validarCampoConversao: function () {
      this.validarSeEhNumero();
    },
    validarSeEhNumero: function () {
      if (isNaN(this.valorParaConverter)) {
        this.mensagemErro = "O valor digitado deve ser um número.";
        this.showDismissibleAlert = true;
        return;
      }

       this.mensagemErro = "";
       this.showDismissibleAlert = false;
    },
    naoHaErros: function() {
      return this.mensagemErro === "";
    }
  },
};
</script>

<style>
</style>