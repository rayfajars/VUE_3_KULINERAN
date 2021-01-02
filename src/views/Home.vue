<template>
  <div class="home">
    
    <Navbar />
    <div class="container">
    <Hero />

    <div class="row mt-4">
      <div class="col">
        <h2>Best <strong>Foods</strong></h2>
      </div>
      <div class="col">
        <router-link to="/foods" class="btn btn-success float-right"><b-icon-eye></b-icon-eye> Lihat Semua</router-link>
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
// @ is an alias to /src
import Navbar from '@/components/Navbar.vue'
import Hero from '@/components/Hero.vue'
import CardProduct from '@/components/CardProduct.vue'
import axios from 'axios'


export default {
  name: 'Home',
  components: {
    Navbar,
    Hero,
    CardProduct
  },
  data(){
    return {
      products:[]
    }
    },
    methods:{
      setProduct(data){
        this.products = data
      }
    },
    mounted(){
      //mounted adalah ketika halaman home itu dipasang/dijalankan koding didalam mounted ini dijalankan
      axios.get('http://localhost:3000/best-products')
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
  
}
</script>
