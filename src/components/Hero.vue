<template>
<div class="hero">
    <!-- desktop -->

    <div class="d-none d-md-block">
        <!-- d-md-block kalo layarnya hp diblock -->
    <div class="row">
        <div class="col-md-6">
            <div class="d-flex h-100"> 
                <div class="justify-content-center align-self-center">
                    <h2><strong>Menu Makanan Enak,</strong> <br> di Gadget Mu !</h2>
                    <p>Ayo segera pilih makanan favorit mu !</p>
                    <router-link to="/foods" class="btn btn-lg btn-success"> Pesan <b-icon-caret-right></b-icon-caret-right></router-link>
                </div>
            </div>
           
        </div>
        <div class="col-md-6">
            <div class="d-flex h-100">
                <div class="justify-content-center align-self-center">
                    <img src="../assets/images/hero.png" alt="" width="100%">
                </div>
            </div>
        </div>
    </div>

    </div>

<!-- mobile -->

<div class="d-sm-block d-md-none">
    <div class="row">
        <!-- d-sm-block kalo layarnya smal di block kalo menengah di transparantin -->
         <div class="col-md-6 mb-5">
            <div class="d-flex h-100">
                <div class="justify-content-center align-self-center">
                    <img src="../assets/images/hero.png" alt="" width="100%">
                </div>
            </div>
        </div>
        <div class="col-md-6">
            <div class="d-flex h-100"> 
                <div class="justify-content-center align-self-center">
                    <h2><strong>Menu Makanan Enak,</strong> <br> di Gadget Mu !</h2>
                    <p>Ayo segera pilih makanan favorit mu !</p>
                    <button class="btn btn-lg btn-success">Pesan <b-icon-caret-right></b-icon-caret-right></button>
                </div>
            </div>
           
        </div>
       
    </div>
</div>
    
</div>
  
</template>

<script>
export default {
    name:"Hero"

}
</script>

<style>

</style>