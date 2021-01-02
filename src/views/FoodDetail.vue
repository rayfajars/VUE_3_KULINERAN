<template>
  <div class="food-detail">
      <Navbar />
      <div class="container">
          <!-- breadcrumb -->
          <div class="row">
              <div class="col">
                  <nav aria-label="breadcrumb">
                    <ol class="breadcrumb">
                        <li class="breadcrumb-item">
                            <router-link class="text-dark" to="/">Home</router-link>
                        </li>
                        <li class="breadcrumb-item">
                        <router-link class="text-dark" to="/foods">Foods</router-link>
                        </li>
                         <li class="breadcrumb-item active" aria-current="page">Detail Makanan</li>
                        
                    </ol>
                 </nav>
              </div>
          </div>

          <!-- food detail -->
          <div class="row mt-3">
              <div class="col-md-6">
                   <img :src="'../assets/images/'+ product.gambar " class="img-fluid shadow" alt="...">
              </div>
              <div class="col-md-6">
                  <h2><strong>{{ product.nama}}</strong></h2>
                  <hr>
                  <h4>Harga : <strong>Rp. {{ product.harga }}</strong></h4>

                 <form class="mt-3" v-on:submit.prevent>
                    <div class="mb-3 form-group">
                        <label for="jumlah_pesanan" class="form-label">Jumlah Pesanan : </label>
                        <input type="number" class="form-control" id="jumlah_pesanan" v-model="pesan.jumlah_pemesanan" min="">
                    </div>
                    <div class="mb-3 form-group">
                        <label for="keterangan" class="form-label">Keterangan Pesanan : </label>
                        <textarea name="keterangan" id="keterangan" class="form-control" placeholder="Keterangan spt: Pedas, Nasi setengah .." cols="20" rows="5" v-model="pesan.keterangan"></textarea>
                    </div>

                    <button class="btn btn-success btn-sm float-right" type="submit" @click="pemesananBtn"><b-icon-cart-plus></b-icon-cart-plus> Pesan</button>
                    
                    </form>
              </div>
          </div>
      </div>
  </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import axios from 'axios'

export default {
    name:"FoodDetail",
    components:{
        Navbar
    },
    data() {
        return {
            product: [],
            pesan: {}
        }
    },
    methods:{
        setProduct(data){
            this.product = data 
        },
        pemesananBtn(){
            if(this.pesan.jumlah_pemesanan) {
            this.pesan.products = this.product
            axios
            .post('http://localhost:3000/keranjangs', this.pesan)
            .then(()=> {
                // kehalaman lain
                this.$router.push({path : "/keranjang"})
                // notification
                this.$toast.success('Berhasil dipesan', {
                    type:"success",
                    position:"top-right",
                    duration:3000,
                    dismissible:true
                })
            })
            .catch((err) =>{
                console.log(err)
            }) 
            }else {
                this.$toast.error('Pesanan belum dimasukan', {
                    type:"error",
                    position:"top-right",
                    duration:3000,
                    dismissible:true
                })
            }          
        }
    },
    mounted(){
      //mounted adalah ketika halaman home itu dipasang/dijalankan koding didalam mounted ini dijalankan
      axios.get('http://localhost:3000/products/'+this.$route.params.id)
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

<style>

</style>