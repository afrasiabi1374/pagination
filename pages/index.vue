<template>
  <div>
    <v-pagination v-model="page" :length="15" :total-visible="12"></v-pagination>
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
