<template>
  <div>
    <v-btn :disabled="disPrev" :to="page+'/' + (value-1)" @click="$emit('input', value-1)"><v-icon>mdi-chevron-left</v-icon></v-icon></v-btn>
    <template  v-for="(item, i) in compLength">
    <v-btn v-show="item !== '...'" :to="page+'/'+item" @click="$emit('input', item)" :key="'btn'+i" >{{ item }}</v-btn>
    <span  v-show="item === '...'" id="dots" :key="'dot'+i">...</span>
    </template>
    <v-btn :disabled="disNext" :to="page+'/' + (value+1)" @click="$emit('input', value+1)"><v-icon>mdi-chevron-right</v-icon></v-icon></v-btn>
  </div>
</template>
<script>
export default {
  props: ['value', 'length', 'page', 'totalVisible'],
  data () {
    return {
      count: 1,
      valueVar: this.value,
      disP: false
    }
  },
  computed: {
    compLength () {
      const finalPagination = []
      finalPagination[0] = 1
      finalPagination[this.totalVisible / 2] = '...'
      for (let i = 2; i <= this.totalVisible; i++) {
        if ((this.totalVisible === this.length) && (this.totalVisible >= this.length)) {
          finalPagination[i - 1] = i
        } else if ((i < this.totalVisible + 1) && (this.totalVisible === 6)) {
          finalPagination[i - 1] = i
          finalPagination[this.totalVisible - 1] = this.length
          finalPagination[this.totalVisible - 2] = this.length - 1
          if ((this.value < this.totalVisible / 2)) {
            finalPagination[this.totalVisible / 2] = '...'
          }
          if ((this.value > this.totalVisible / 2)) {
            finalPagination[this.totalVisible / 2] = this.value
            finalPagination[(this.totalVisible / 2) - 1] = this.value - 1
            finalPagination[(this.totalVisible / 2) + 1] = '...'
          }

          if ((this.value >= this.totalVisible - 1)) {
            finalPagination[this.totalVisible / 2] = this.value
            finalPagination[(this.totalVisible / 2) + 1] = '...'
            finalPagination[(this.totalVisible - 5)] = '...'
          }
          if (this.value >= this.length - 2) {
            finalPagination[(this.totalVisible / 2) + 1] = this.length - 1
            finalPagination[(this.totalVisible / 2)] = this.length - 2
            finalPagination[(this.totalVisible / 2) - 1] = this.length - 3
          }
        } else if ((this.totalVisible % 2) !== 0) {
          finalPagination[i - 1] = i
          finalPagination[this.totalVisible - 1] = this.length
          finalPagination[this.totalVisible - 2] = this.length - 1
          finalPagination[((this.totalVisible - 1) / 2)] = '...'
          if (this.value >= (((this.totalVisible - 1) / 2))) {
            finalPagination[((this.totalVisible - 1) / 2) + 1] = '...'
            finalPagination[((this.totalVisible - 1) / 2)] = i - 2
          }
          if (this.value >= this.totalVisible - 1) {
            finalPagination[this.totalVisible - ((this.totalVisible / 2) - 1)] = '...'
            finalPagination[this.totalVisible - (this.totalVisible - 1)] = '...'
            finalPagination[this.totalVisible - (this.totalVisible - 2)] = this.value
          }
          if (this.value >= (this.length - 2)) {
            finalPagination[this.totalVisible - 2] = this.length - 1
            finalPagination[this.totalVisible - 3] = this.length - 2
          }
        }
      }

      console.log('final pagination =>>>>', finalPagination)
      return finalPagination
    },
    disPrev () {
      return this.value === 1
    },
    disNext () {
      return this.value === this.length
    }

  }
}
</script>
<style scoped>
  #dots {
    display: inline-block;
    width: 45px;
    height: 5px;
    text-align: center;
  }
</style>
