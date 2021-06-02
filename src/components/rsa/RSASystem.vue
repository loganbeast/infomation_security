<template>
  <div class='container'>
        <h3 class="mb-4">Xây dựng hệ mật RSA</h3>
        <div>
            <b-button variant="outline-secondary" @click="reset">Clear All</b-button>
        </div>
        <hr>
        <div>
            <b-form-input v-model="x" type="number" placeholder="Nhap ban ro x" class="mb-4"></b-form-input>
            <b-form-input v-model="p" type="number" placeholder="Nhap p" class="mb-4"></b-form-input>
            <b-form-input v-model="q_tmp" type="number" placeholder="Nhap q" class="mb-4"></b-form-input>
            <b-form-input v-model="e" type="number" placeholder="Nhap khoa ky e" class="mb-4"></b-form-input>
        </div>
        <div><strong>x = </strong> {{this.x || 'undefined'}}</div>
        <div><strong>y = </strong> {{this.y || 'undefined'}}</div>
        <div><strong>p = </strong>{{this.p || 'undefined'}}</div>
        <div><strong>q = </strong> {{this.q_tmp || 'undefined'}}</div>
        <div><strong>Khoa cong khai (e,n) = </strong>({{this.e || 'undefined'}} , {{this.n || 'undefined'}})</div>
        <div><strong>Khoa bi mat (d,n) = </strong>({{this.d || 'undefined'}} , {{this.n || 'undefined'}})</div>
        <hr>
        
        <div v-if="p*q_tmp>0">
            <strong>n = p * q = </strong> {{this.p}} * {{this.q_tmp}} = {{this.n}} 
            <strong>m = phi(n) = (p - 1)(q - 1) = </strong> {{this.p - 1}} * {{this.q_tmp - 1}} = {{this.m}}
            <strong>gcd(e, m) = </strong> <span class="text-danger">{{this.g}}</span>
            <div v-if="g!==1">
                <strong>gcd(e, m) = </strong> <span class="text-danger">{{this.g}} != 1</span> => e duoc chon la khong thoa man
            </div>
            <div v-else>
                Ta nhân thấy e được chọn thỏa mãn <span class="text-danger">gcd(e, m) = 1.</span>
            </div>
            <hr>
            <h3>Bước 1: Thực hiện tính khóa bí mật d</h3>
            <p>Áp dụng thuật toán Euclid mở rộng, ta có:</p>
            <strong>d = e ^ -1 mod m = </strong> {{this.e}} ^ -1 modulo {{this.m}} = {{this.d}}

            <div v-if="!x || x<=0">
                <hr>
                <h3 class="text-danger">Hãy nhập x > 0 !!!</h3>
            </div>
            <div v-else>
                <h3>Bước 2: Mã hóa bản rõ x = {{this.x}}</h3>
                <p>
                    <strong>y = x ^ e mod n = </strong>{{this.x}} ^ {{this.e}} modulo {{this.n}} = {{this.y}}  
                </p>
                <hr>
                <h3>Bước 3: Giải mã y khi biết d, n</h3>
                <strong>x = y ^ d mod n = </strong> {{this.y}} ^ {{this.d}} mod {{this.n}}
                <hr>
                <h3 class="text-danger"><strong>x = {{this.de}}</strong></h3>
            </div>
        </div>
  </div>
  
</template>

<script> 
import bigInt from 'big-integer';
import { BigNumber } from 'bignumber.js';
import { gcd } from '../../helpers/exculid_extends';
export default {
    name: 'RSASystem',
    components: {
    },
    data () {
        return {
            x : '',
            e : '',
            p : '',
            q_tmp : '',   


        }
    },
    methods: {
        reset: function () {
            this.p = ''
            this.q_tmp = ''
            this.e = ''
            this.x = ''
        }
    },
    computed: {
        n () {
            console.log("==================asdasdas")
            if (this.p && this.q_tmp) {
                return new BigNumber(this.p).multipliedBy(this.q_tmp).toFixed()
            } else return undefined
        },
        m () {
            if (this.p && this.q_tmp) {
                return new BigNumber(new BigNumber(this.p).minus(1)).multipliedBy(new BigNumber(this.q_tmp).minus(1)).toFixed()
            } else return undefined
        },
        g () {
            if (this.e && this.m) {
                return gcd(this.e, this.m)
            } else return undefined
        },
        d () {
            if (this.e && this.m) {
                return bigInt(this.e).modInv(this.m).toString()
            } else return undefined
        },
        y () {
            if (this.x && this.e && this.n) {
                return bigInt(this.x).modPow(this.e, this.n).toString()
            } else return undefined
        },
        de () {
            if (this.y && this.d && this.n) {
                return bigInt(this.y).modPow(this.d, this.n).toString()
            } else return undefined
        }
    }
}
</script>

<style scoped>
.container {
    margin-top: 100px;
    width: 50%;
    overflow: auto;
}
</style>