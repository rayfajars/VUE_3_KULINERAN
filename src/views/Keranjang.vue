<template>
<div class="keranjang">
    <Navbar :updateKeranjang="keranjangs"/>
    <div class="container">
        <div class="row">
              <div class="col">
                  <nav aria-label="breadcrumb">
                    <ol class="breadcrumb">
                        <li class="breadcrumb-item">
                            <router-link class="text-dark" to="/">Home</router-link>
                        </li>
                        <li class="breadcrumb-item">
                        <router-link class="text-dark" to="/foods">Keranjang</router-link>
                        </li>
                         <li class="breadcrumb-item active" aria-current="page">Detail Pesanan</li>
                        
                    </ol>
                 </nav>
              </div>
          </div>

          <div class="row mt-3">
              <div class="col">
                  <h2>Pesanan <strong>Saya</strong></h2>
                  <div class="table-responsinve mt-4">
                      <table class="table">
                    <thead>
                        <tr>
                        <th scope="col">#</th>
                        <th scope="col">Foto</th>
                        <th scope="col">Makanan</th>
                        <th scope="col">Keterangan</th>
                        <th scope="col">Jumlah</th>
                        <th scope="col">Harga</th>
                        <th scope="col">Total Harga</th>
                        <th scope="col">Action</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="(keranjang, index) in keranjangs" :key="keranjang.id">
                        <th>{{ index+1}}</th>
                        <td><img :src="'../assets/images/'+ keranjang.products.gambar " class="img-fluid shadow" alt="..." width="200px" height="200px"></td>
                        <td>{{ keranjang.products.nama}}</td>
                        <td>{{ keranjang.keterangan ? keranjang.keterangan : "-" }}</td>
                        <!-- ternary opperator, kaya if else jika keterangan tidak ada maka isi dengan - -->
                        <td>{{ keranjang.jumlah_pemesanan}}</td>
                        <td align="right">Rp. {{ keranjang.products.harga}}</td>
                        <td align="right"><strong>Rp. {{ keranjang.products.harga * keranjang.jumlah_pemesanan}} </strong></td>
                        <td align="center" class="text-danger">
                            <button class="btn btn-danger btn-sm float-right" @click="hapusKeranjangs(keranjang.id)"><b-icon-trash></b-icon-trash> Hapus</button>
                            
                        </td>
                        </tr>
                        <tr>
                            <td colspan="6" align="right">
                                <strong> Total Harga : </strong>
                            </td> 
                            <td align="right">
                                <strong>RP. {{ totalHarga }}</strong>
                                <!-- <strong>RP. {{ totalJumlah }}</strong> -->
                            </td>
                            <td></td>
                        </tr>
                        
                    </tbody>
                    </table>
                  </div>
              </div>
          </div>

          <!-- form check out -->
          <div class="row justify-content-end">
              <div class="col-md-4">
                  <form class="mt-3" v-on:submit.prevent>
                    <div class="mb-3 form-group">
                        <label for="nama" class="form-label">Nama Pemesan : </label>
                        <input type="text" class="form-control" id="nama" v-model="pesan.nama" placeholder="Masukan nama">
                    </div>
                    <div class="mb-3 form-group">
                        <label for="noMeja" class="form-label">Nomor Meja : </label>
                        <input type="number" class="form-control" id="noMeja" v-model="pesan.noMeja" placeholder="Masukan No Meja">
                    </div>

                    <button class="btn btn-success btn-sm float-right" type="submit" @click="checkOut"><b-icon-cart-plus></b-icon-cart-plus> Check Out</button>
                    
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
    name: "Keranjang",
    components:{
        Navbar
    },
    data() {
        return {
            keranjangs: [],
            pesan:{}
        }
    },
     methods: {
    setKeranjangs(data){
      this.keranjangs = data
    },
   hapusKeranjangs(id) {
       axios.delete('http://localhost:3000/keranjangs/'+id)
      .then(() =>
        // handle success
        this.$toast.error('Succes hapus keranjang', {
                    type:"error",
                    position:"top-right",
                    duration:3000,
                    dismissible:true,
        }),
        // console.log(response.data)
      )
      .catch((error) =>
        // handle error
        console.log(error)
      );

    //   update data keranjang
    axios.get('http://localhost:3000/keranjangs')
      .then((response) =>
        // handle success
        this.setKeranjangs(response.data)
        // console.log(response.data)
      )
      .catch((error) =>
        // handle error
        console.log(error)
      )
    },
    checkOut(){
        if(this.pesan.nama && this.pesan.noMeja){
            this.pesan.keranjangs = this.keranjangs
            axios
            .post('http://localhost:3000/pesanans', this.pesan)
            .then(()=> {

                this.keranjangs.map(function(item){
                    // hapus semua keranjang
                    return axios.delete('http://localhost:3000/keranjangs/'+item.id)
                    .catch((error) =>
                        // handle error
                        console.log(error)
                    )
                });


                // kehalaman lain
                this.$router.push({path : "/pesanan-sukses"})
                // notification
                this.$toast.success('Makanan Sukses dipesan', {
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
            this.$toast.error('Nama dan No Meja Harus diisi!', {
                    type:"error",
                    position:"top-right",
                    duration:3000,
                    dismissible:true,
        })
        }
    }
  },
  mounted(){
      //mounted adalah ketika halaman home itu dipasang/dijalankan koding didalam mounted ini dijalankan
      axios.get('http://localhost:3000/keranjangs')
      .then((response) =>
        // handle success
        this.setKeranjangs(response.data)
        // console.log(response.data)
      )
      .catch((error) =>
        // handle error
        console.log(error)
      )
    },computed:
    {
// function computed untuk menjumllahkan
    totalHarga(){
        return this.keranjangs.reduce(function (items, data) {
            return items+data.products.harga*data.jumlah_pemesanan
        },0)
    },
    totalJumlah(){
        return this.keranjangs.reduce(function (items, data){
            return items+parseInt(data.jumlah_pemesanan) * data.products.harga
        },0)
    }
    }
    

}
</script>

<style>

</style>