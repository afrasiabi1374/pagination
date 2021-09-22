<template>
  <v-app>
    <v-container>
      <Paginate v-model="page" page="/blog" :length="15" :totalVisible="6" />
      {{ page }}
      <Nuxt />
    </v-container>
  </v-app>
</template>

<script>
import Paginate from '../components/Paginate'
export default {
  components: { Paginate },
  data () {
    return {
      page: 1
    }
  }
}
</script>
<style scoped>
a{
  text-decoration: none;
}
</style>
