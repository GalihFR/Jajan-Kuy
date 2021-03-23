<template>
  <div class="food-detail">
    <Navbar />
    <div class="container">
      <div class="row mt-4">
        <div class="col">
          <nav aria-label="breadcrumb">
            <ol class="breadcrumb">
              <li class="breadcrumb-item">
                <router-link to="/" class="text-dark">Home</router-link>
              </li>
              <li class="breadcrumb-item">
                <router-link to="/foods" class="text-dark">Foods</router-link>
              </li>
              <li class="breadcrumb-item active" aria-current="page">
                Foods Detail
              </li>
            </ol>
          </nav>
        </div>
      </div>

      <div class="row mt-2">
        <div class="col-md-6">
          <img
            :src="'../assets/images/' + product.gambar"
            :alt="product.nama"
            class="img-fluid shadow"
          />
        </div>
        <div class="col-md-6">
          <h2>
            <strong>{{ product.nama }}</strong>
          </h2>
          <h5>
            Harga <strong>Rp. {{ product.harga }}</strong>
          </h5>
          <form class="mt-4" v-on:submit.prevent>
            <div class="form-group">
              <label for="jumlah_order">Jumlah Order</label>
              <input
                type="number"
                class="form-control"
                v-model="order.jumlah_order"
              />
            </div>
            <div class="form-group">
              <label for="keterangan">Keterangan</label>
              <textarea
                class="form-control"
                placeholder="Exc: Nasi Setengah, pedas, Manis..."
                v-model="order.keterangan"
              ></textarea>
            </div>
            <button
              type="submit"
              class="btn btn-success"
              v-on:click="pemesanan"
            >
              <b-icon-cart-plus></b-icon-cart-plus> Keranjang
            </button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import axios from "axios";

export default {
  name: "FoodDetail",
  components: {
    Navbar,
  },
  data() {
    return {
      product: {},
      order: {},
    };
  },
  methods: {
    setProduct(data) {
      this.product = data;
    },
    pemesanan() {
      if (this.order.jumlah_order) {
        this.order.products = this.product;
        axios
          .post("http://localhost:3000/keranjangs", this.order)
          .then(() => {
              this.$router.push({ path: "/keranjang" })
            this.$toast.success("Success Order", {
              type: "success",
              position: "top",
              duration: 3000,
              dismissible: true,
            });
          })
          .catch((err) => console.log(err));
      } else {
        this.$toast.error("Jumlah order harus diisi !", {
          type: "error",
          position: "top",
          duration: 3000,
          dismissible: true,
        });
      }
    },
  },
  mounted() {
    axios
      .get("http://localhost:3000/products/" + this.$route.params.id)
      .then((res) => this.setProduct(res.data))
      .catch((err) => console.log(err));
  },
};
</script>

<style>
</style>