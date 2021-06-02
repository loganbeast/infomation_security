<template>
  <div class='container'>
      <h3 class="mb-4"> Ký văn bản X bằng cặp khóa bí mật (d, n)</h3>
      <div>
          <b-button variant="outline-secondary" @click="reset">Clear All</b-button>
      </div>
      <hr>
      <div>
          <b-form-input v-model="x" type="number" placeholder="Nhap ban ro x" class="mb-4"></b-form-input>
          <b-form-input v-model="d" type="number" placeholder="Nhap khoa ky d" class="mb-4"></b-form-input>
          <b-form-input v-model="n" type="number" placeholder="Nhap n" class="mb-4"></b-form-input>
      </div>
      <h3>x = {{this.x || 'undefined'}}</h3>
      <h3>(d,n) = ({{this.d || 'undefined'}}, {{this.n || 'undefined'}})</h3>
      <hr>
      <h3>Chữ ký s = x ^ d mod n = <span>{{this.x || 'undefined'}} ^ {{this.d || 'undefined'}} modulo {{this.n || 'undefined'}} = {{this.s || 'undefined'}} </span></h3> 
      <h2 v-if="s && s!== 0" class="text-danger">
          Kết luận: chữ ký số: {{this.s || 'undefined'}}
      </h2>
  </div>
  
</template>

<script> 
import bigInt from 'big-integer';
export default {
    name: 'RSASign',
    components: {

    },
    data () {
        return {
            x : '',
            d : '',
            n : '',
        }
    },
    methods: {
        reset: function () {
            this.x = ''
            this.d = ''
            this.n = ''
        }
    },
    computed: {
        s () {
            if (this.x && this.d && this.n) {
                return bigInt(this.x).modPow(this.d, this.n).toString()
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