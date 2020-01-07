<template>
  <nav>
    <ul>
      <li v-for="rota in rotas">
        <router-link :to="rota.path ? rota.path : '/'">{{ rota.titulo }}</router-link>
        <!-- Se route.path estiver definido, vá para aquele path, se não, defina-o como '/' que equivale ao 'Home' -->
      </li>
    </ul>
  </nav>
</template>

<script>
export default {
//   props: ['rotas']
props: {
    rotas: {
        type: Array,
        required: true
    }
}
}
</script>

<style scoped>
</style>