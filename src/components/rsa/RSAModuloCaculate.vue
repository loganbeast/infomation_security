<template>
  <div class='container'>
      <h3 class="mb-4"> Tính mũ theo Modulo y</h3>
      <div>
          <b-button variant="outline-secondary" @click="reset">Clear All</b-button>
      </div>
      <hr>
      <div>
          <b-form-input v-model="x" type="number" placeholder="Input x" class="mb-4"></b-form-input>
          <b-form-input v-model="e" type="number" placeholder="Input e" class="mb-4"></b-form-input>
          <b-form-input v-model="n" type="number" placeholder="Input n" class="mb-4"></b-form-input>
      </div>
      <h3>y = x ^ e mod n = {{this.answer || 'undefined'}}</h3>
  </div>
  
</template>

<script> 
import bigInt from 'big-integer';
export default {
    name: 'RSAModuloCaculate',
    components: {

    },
    data () {
        return {
            x : '',
            y : '',
            n : '',
            e : ''
        }
    },
    methods: {
        reset: function () {
            this.x = ''
            this.y = ''
            this.n = ''
            this.e = ''
        }
    },
    computed: {
        answer () {
            if (this.x && this.e && this.n) {
                return bigInt(this.x).modPow(this.e, this.n).toString()
            } else {
                return undefined
            }
        }
    }
}
</script>

<style scoped>
.container {
    margin-top: 100px;
    width: 50%;
}
</style>