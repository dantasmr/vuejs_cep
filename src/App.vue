<template>
  <div>
    <label for="cep">CEP:</label>
    <input v-model="cep" id="cep" type="text" placeholder="Insira o CEP">
    <button @click="searchAddress">Buscar</button>
    <p v-if="address">{{ address }}</p>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      cep: '',
      address: ''
    }
  },
  methods: {
    async searchAddress() {
      try {
        const response = await axios.get(`https://viacep.com.br/ws/${this.cep}/json/`)
        this.address = `${response.data.logradouro}, ${response.data.localidade} - ${response.data.uf}`
      } catch (error) {
        console.error(error)
        this.address = 'CEP não encontrado'
      }
    }
  }
}
</script>
