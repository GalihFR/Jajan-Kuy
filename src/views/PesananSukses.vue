<template>
  <div class="pesanan-sukses">
    <Navbar />
    <div class="container">
      <div class="row justify-content-center mt-5">
        <div class="col text-center">
          <img src="../assets/images/menunggu.png" alt="waiting" width="300" />
          <h2 class="mt-2"><strong>Sukses Checkout !</strong></h2>
          <h4>
            Pesanan anda segera diproses <br />
            Mohon ditunggu :)
          </h4>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";

export default {
  name: "PesananSukses",
  components: {
    Navbar,
  },
  methods: {
    movingHome(){
      // this.$router.push({ path: "/foods" })
      this.$route.router.push({path: '/keranjang'}); 
    }
  },
  mounted(){
    setTimeout(function(){
      this.movingHome
      console.log("ok")
    },2000)
  }
};
</script>

<style>
</style>