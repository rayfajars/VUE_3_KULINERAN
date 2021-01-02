<template>
  <div>
    <Navbar />
    <div class="container">
      <div class="row">
        <div class="col">
          <h2>Daftar <strong>Makanan</strong></h2>
        </div>
      </div>

      <div class="row mt-3">
        <div class="col">
          <div class="input-group mb-3">
            <input  v-model="cariMakanan" type="text" class="form-control" placeholder="Cari Makanan Favorit Mu.." aria-label="Cari" aria-describedby="basic-addon1" @keyup="searchFood">
            <!-- v-model memasukan nama input ke function input, keyup event ketikan data -->
            <span class="input-group-text" id="basic-addon1"><b-icon-search></b-icon-search></span>
          </div>
        </div>
      </div>

      <div class="row mb-4">
        <div class="col-md-4 mt-4" v-for="product in products" :key="product.id">
          <!-- v-for = looping -->
          <!-- pharsing data/lempar data ke CardProduct, products variable dari return products, key kunci data -->
          <CardProduct :product="product"/>
        </div>
  </div>

    </div>
  </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import CardProduct from '@/components/CardProduct.vue'
import axios from 'axios'

export default {
  name: "Foods",
  components: {
    Navbar,
    CardProduct
  },
  data(){
    return {
      products:[],
      cariMakanan:''
    }
    },
    methods:{
      setProduct(data){
        this.products = data
      },
      searchFood(){
        axios.get('http://localhost:3000/products?q='+this.cariMakanan)
      .then((response) =>
        // handle success
        this.setProduct(response.data)
        // console.log(response.data);
      )
      .catch((error) =>
        // handle error
        console.log(error)
      )

      }
    },
    mounted(){
      //mounted adalah ketika halaman home itu dipasang/dijalankan koding didalam mounted ini dijalankan
      axios.get('http://localhost:3000/products')
      .then((response) =>
        // handle success
        this.setProduct(response.data)
        // console.log(response.data);
      )
      .catch((error) =>
        // handle error
        console.log(error)
      )
    }
};
</script>

<style>
</style>