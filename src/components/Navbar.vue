<template>
  <div>
    <b-navbar toggleable="lg" type="light">
      <div class="container">
        <b-navbar-brand href="#">Jajankuy</b-navbar-brand>

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
              <router-link class="nav-link" to="/keranjang">
                Keranjang
                <b-icon-bag></b-icon-bag>
                <span class="badge badge-danger ml-2">{{
                  updateDataKeranjang
                    ? updateDataKeranjang.length
                    : jumlah_order.length
                }}</span>
              </router-link>
            </li>
          </b-navbar-nav>
        </b-collapse>
      </div>
    </b-navbar>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Navbar",
  data() {
    return {
      jumlah_order: [],
    };
  },
  props: ["updateDataKeranjang"],
  methods: {
    setJumlahOrder(data) {
      this.jumlah_order = data;
    },
  },
  mounted() {
    axios
      .get("http://localhost:3000/keranjangs")
      .then((res) => this.setJumlahOrder(res.data))
      .catch((err) => console.log(err));
  },
};
</script>

<style>
</style>