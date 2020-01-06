<template>
  <div>
    <h1>{{ titulo }}</h1>

    <ul>
      <li v-for="foto of fotos">
        <img :src="foto.url" :alt="foto.titulo" />
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      titulo: "Alurapic",
      fotos: []
    };
  },

  created() {
    this.$http.get("http://localhost:3000/v1/fotos") //Faz a requisição GET
    .then(res => res.json()) //Quando a requisição retorna, salva esse resultado em 'res' e converte para json através do 'res.json()'
    .then(fotos => this.fotos = fotos, err => console.log(err)); 
    //Quando a res.json() retorna, a resposta dela é definida como a 'fotos' e salva no objeto através de 'this.fotos'
    // E caso não receba retorno, é apresentado um erro no console através do 'console.log(err)'
  }
};
</script>

<style>
</style>
