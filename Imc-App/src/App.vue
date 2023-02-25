<template>
  <div>
    <h2 class="label-title">Calcule seu IMC</h2>

    <h3 class="label-subtitle">
      Por favor, digite seu peso e altura para calcular o IMC!
    </h3>

    <div class="div-imc">
      <span class="p-inputtext-sm">
        <InputText
          style="
            border-top: none;
            border-left: none;
            border-right: none;
            font-size: larger;
            background-color: black;
            color: lightgoldenrodyellow;
          "
          id="input-weight"
          type="number"
          v-model="weight"
          :disabled="imc"
          placeholder="Peso"
        />
        <label for="input-weight"></label>
      </span>
    </div>

    <div class="div-imc">
      <span class="p-inputtext-sm">
        <InputText
          style="
            border-top: none;
            border-left: none;
            border-right: none;
            font-size: larger;
            background-color: black;
            color: lightgoldenrodyellow;
          "
          id="input-height"
          type="number"
          v-model="height"
          :disabled="imc"
          placeholder="Altura"
        />
        <label for="input-height"></label>
      </span>
    </div>

    <div class="div-imc" v-if="!imc">
      <Button
        style="
          background-color: transparent;
          color: red;
          border: none;
          font-size: larger;
        "
        label="Limpar"
        @click="clear"
      />
      <Button
        style="
          background-color: transparent;
          border: none;
          color: limegreen;
          font-size: larger;
        "
        label="Calcular"
        @click="calculate"
      />
    </div>

    <div v-if="imc">
      <p class="label-result" style="color: fuchsia; margin-top: 5rem">
        Seu IMC é : {{ imc }}
      </p>
      <p
        class="label-classification"
        style="color: lightpink; margin-top: 2rem; margin-bottom: 2rem"
      >
        A classificação do seu IMC é: {{ classification }}
      </p>
      <Button
        style="
          background-color: transparent;
          color: red;
          border: none;
          font-size: larger;
        "
        @click="clear"
        label="Calcular Novamente"
      />
    </div>
  </div>
</template>

<script>
import Button from "primevue/button";
import InputText from "primevue/inputtext";

export default {
  data() {
    return {
      height: null,
      weight: null,
      imc: null,
      classification: "",
    };
  },
  methods: {
    calculate: function () {
      this.imc = (this.weight / (this.height * this.height)).toFixed(2);
      console.log(this.imc);
      if (this.imc < 18.5) {
        this.classification = "Magreza";
      } else if (this.imc >= 18.5 && this.imc < 25) {
        this.classification = "Normal";
      } else if (this.imc >= 25 && this.imc < 30) {
        this.classification = "Sobrepeso";
      } else if (this.imc >= 30 && this.imc < 40) {
        this.classification = "Obesidade";
      } else {
        this.classification = "Obesidade Grave";
      }
    },
    clear() {
      this.height = null;
      this.weight = null;
      this.imc = null;
      this.result = "";
      this.classification = "";
    },
  },
  components: { InputText, Button },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
* {
  background-color: black;
  text-align: center;
  margin: 50px auto;
  padding: 0;
}

.div-imc span {
  cursor: pointer;
  margin-top: 4rem;
}

.label-title {
  color: rgba(255, 0, 255, 0.725);
  font-size: 2rem;
  margin-top: 15px;
  margin-bottom: 2rem;
}

.label-subtitle {
  color: purple;
  margin-bottom: 2rem;
  font-size: 1.1rem;
}

.label-result {
  font-size: 2rem;
}

.label-classification {
  font-size: 1.5rem;
}

.div-imc Button {
  margin-left: 1rem;
  cursor: pointer;
}
</style>
