<template>
  <div class="card shadow card-product">
    <img :src=" '../assets/images/' + product.gambar " class="card-img-top" :alt="product.nama" height="250"/>
    <div class="card-body">
      <h5 class="card-title">{{product.nama}}</h5>
      <p class="card-text">
        Harga: Rp. {{product.harga}}
      </p>
      <router-link :to="'/foods/'+product.id" class="btn btn-primary"><b-icon-cart></b-icon-cart> Order</router-link>
    </div>
  </div>
</template>

<script>
export default {
  name: "CardProduct",
  props: ["product"],
};
</script>

<style>
</style>