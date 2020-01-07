<template>
  <div>
    <h1 class="centralizado">{{ titulo }}</h1>

    <input
      type="search"
      class="filtro"
      @input="filtro = $event.target.value"
      placeholder="filtre por parte do título"
    />

    <!-- {{ filtro }} -->

    <ul class="lista-fotos">
      <li class="lista-fotos-item" v-for="foto of fotosComFiltro">
        <meu-painel :titulo="foto.titulo">
          <imagem-responsiva :url="foto.url" :titulo="foto.titulo" />
        </meu-painel>
      </li>
    </ul>
  </div>
</template>

<script>
import Painel from "../shared/painel/Painel.vue";
import ImagemResponsiva from "../shared/imagem-responsiva/ImagemResponsiva.vue";

export default {
  components: {
    "meu-painel": Painel,
    "imagem-responsiva": ImagemResponsiva
  },

  data() {
    return {
      titulo: "Alurapic",
      fotos: [],
      filtro: ""
    };
  },

  computed: {
    fotosComFiltro() {
      if (this.filtro) {
        /*Filtrar*/
        let exp = new RegExp(
          this.filtro.trim(),
          "i"
        ); /* Salva no exp o valor digitado no fitro */
        return this.fotos.filter(foto => exp.test(foto.titulo));
      } else {
        return this.fotos;
      }
    }
  },

  created() {
    this.$http
      .get("http://localhost:3000/v1/fotos") //Faz a requisição GET
      .then(res => res.json()) //Quando a requisição retorna, salva esse resultado em 'res' e converte para json através do 'res.json()'
      .then(fotos => (this.fotos = fotos), err => console.log(err));
    //Quando a res.json() retorna, a resposta dela é definida como a 'fotos' e salva no objeto através de 'this.fotos'
    // E caso não receba retorno, é apresentado um erro no console através do 'console.log(err)'
  }
};
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
