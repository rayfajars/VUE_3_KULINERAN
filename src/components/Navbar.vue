<template>
<div class="mb-5">
  <b-navbar toggleable="lg" type="light">
    <div class="container">
      <b-navbar-brand href="#"><strong>Kulineran</strong></b-navbar-brand>

    <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

    <b-collapse id="nav-collapse" is-nav>
      <b-navbar-nav>

         <li class="nav-item">
              <router-link class="nav-link" to="/">Home</router-link>
            </li>
            <li class="nav-item">
              <router-link class="nav-link" to="/foods">Foods</router-link>
            </li>
       
      </b-navbar-nav>

      <!-- Right aligned nav items -->
      <b-navbar-nav class="ml-auto">
             <li class="nav-item">
              <router-link class="nav-link" to="/keranjang">keranjang 
              <b-icon-bag></b-icon-bag>
              <span class="badge badge-success ml-2"> {{ updateKeranjang ? updateKeranjang.length :jumlah_pesanan.length}} </span>
              </router-link>
            </li>
      </b-navbar-nav>
    </b-collapse>

    </div>
    
  </b-navbar>
</div>
</template>

<script>
import axios from 'axios'

export default {
  nama: "Navbar",
  data(){
    return {
      jumlah_pesanan : []
    }
  },
  props:['updateKeranjang'],
  methods: {
    setJumlah(data){
      this.jumlah_pesanan = data
    }
  },
  mounted(){
      //mounted adalah ketika halaman home itu dipasang/dijalankan koding didalam mounted ini dijalankan
      axios.get('http://localhost:3000/keranjangs')
      .then((response) =>
        // handle success
        this.setJumlah(response.data)
        // console.log(response.data);
      )
      .catch((error) =>
        // handle error
        console.log(error)
      )
    }
};
</script>

<style></style>
