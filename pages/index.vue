<template>
  <div>
    <v-pagination v-model="page" :length="10" :total-visible="8"></v-pagination>
    {{ page }}
    <div>index</div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      page: 1
    }
  }
}
</script>

<style>

</style>
