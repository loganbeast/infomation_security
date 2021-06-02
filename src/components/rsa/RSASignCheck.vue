<template>
  <div class='container'>
      <h3 class="mb-4">Kiểm tra chữ ký</h3>
      <div>
          <b-button variant="outline-secondary" @click="reset">Clear All</b-button>
      </div>
      <hr>
      <div>
          <b-form-input v-model="x" type="number" placeholder="Nhap ban ro x" class="mb-4"></b-form-input>
          <b-form-input v-model="s" type="number" placeholder="Nhap chu ky s" class="mb-4"></b-form-input>
          <b-form-input v-model="e" type="number" placeholder="Nhap khoa ky e" class="mb-4"></b-form-input>
          <b-form-input v-model="n" type="number" placeholder="Nhap n" class="mb-4"></b-form-input>
      </div>
      <h3>x = {{this.x || 'undefined'}}</h3>
      <h3>Chu ky so s = {{this.s || 'undefined'}}</h3>
      <h3>Khoa cong khai e = {{this.e || 'undefined'}}</h3>
      <h3>Modulo khóa công khai n = {{this.n || 'undefined'}}</h3>
      <hr>
      <h2>
          Kiem tra (x, s) = (x === s ^ e mod n) ? {{this.check === this.x}}
      </h2>
      <hr>
      <div v-if="s && e && n">
        <h3>s ^ e mod n = {{this.s}} ^ {{this.e}} mod {{this.n}} = <span class="text-danger">{{this.check}}</span> </h3>
        <h2 v-if="check === x" class="text-danger"> Chữ ký hợp lệ</h2>
        <h2 v-else class="text-danger"> Chữ ký không hợp lệ</h2>
      </div>
  </div>
  
</template>

<script> 
import bigInt from 'big-integer';
export default {
    name: 'RSASignCheck',
    components: {

    },
    data () {
        return {
            x : '',
            e : '',
            n : '',
            s : ''
        }
    },
    methods: {
        reset: function () {
            this.x = ''
            this.e = ''
            this.n = ''
            this.s = ''
        }
    },
    computed: {
        check () {
            if (this.s && this.e && this.n) {
                return bigInt(this.s).modPow(this.e, this.n).toString()
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