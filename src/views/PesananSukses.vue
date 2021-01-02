<template>
  <div class="pesanan-sukses">
      <Navbar />
      <div class="container">
          <div class="row justify-content-center">
              <div class="col text-center">
                  <img src="assets/images/menunggu.png"  width="300" class="mb-3">
                  <h2><strong>Sukses dipesan!</strong></h2>
                  <br>
                  <h4>Pesanan Anda Segera diproses <br> <br> Terima Kasih</h4>
              </div>
          </div>
      </div>
  </div>
</template>

<script>
import Navbar from '@/components/Navbar.vue'

export default {
    name: "PesananSukses",
    components: {
    Navbar
  },

}
</script>

<style>

</style>