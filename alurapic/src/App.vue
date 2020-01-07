<template>
  <div class="corpo">
    <meu-menu :rotas="routes" />
    <!-- Hora exibe um componente e outra hora outro. -->
    <transition name="pagina">
      <router-view></router-view>
    </transition>
  </div>
</template>

<script>
import { routes } from "./routes";
import Menu from "./components/shared/menu/Menu.vue";

export default {
  components: {
    "meu-menu": Menu
  },

  data() {
    return {
      // Equivale a routes:routes
      routes
    };
  }
};
</script>

<style>
.corpo {
  font-family: Helvetica, sans-serif;
  margin: 0 auto;
  width: 96%;
}

.pagina-fade,
.pagina-leave-active {
  opacity: 0;
}

.pagina-enter-actitve,
.pagina-leave-active {
  transition: opacity 0.4s;
}
</style>
