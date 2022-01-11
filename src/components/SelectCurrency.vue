<template>
  <b-row>
    <b-col>
      <b-form-group>
        <b-form-select v-model="moedaSelecionada">
          <b-form-select-option
            v-for="(moeda, index) in moedas"
            :key="index"
            :value="moeda"
          >
            {{ moeda.code }} {{ obterNomeMoedaFormatado(moeda.name) }}
          </b-form-select-option>
        </b-form-select>
      </b-form-group>
    </b-col>
  </b-row>
</template>

<script>
export default {
  name: "SelectCurrency",
  data: function () {
    return {
      moedas: [],
      moedaSelecionada: "",
      nomeDolar: "Dólar Americano",
      nomeEuro: "Euro",
    };
  },
  props: {
    obterMoedaSelecionada: Function,
  },
  methods: {
    buscarConversaoMoeda: async function (tipoMoeda) {
      return await fetch(
        "https://economia.awesomeapi.com.br/json/last/" + tipoMoeda
      )
        .then((res) => res.json())
        .then((res) => res)
        .catch((error) => {
          return {
            error: true,
            message: error,
          };
        });
    },
    obterNomeMoedaFormatado: function(nomeMoeda) {
      return " (" + nomeMoeda.split("/")[0] + ")";
    },

    buscarMoedas: async function () {
      const dolarReal = await this.buscarConversaoMoeda("USD-BRL");
      const euroReal = await this.buscarConversaoMoeda("EUR-BRL");

      if (!dolarReal.error && !euroReal.error) {
        this.moedas.push(dolarReal.USDBRL);
        this.moedas.push(euroReal.EURBRL);

        this.moedaSelecionada = this.moedas[0];
      }
    },
  },
  //ciclo de vida
  created: function () {
    this.buscarMoedas();
  },
  updated: function () {
    this.obterMoedaSelecionada(this.moedaSelecionada);
  },
};
</script>

<style>
</style>