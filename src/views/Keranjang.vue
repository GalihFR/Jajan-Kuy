<template>
  <div class="keranjang">
    <Navbar :updateDataKeranjang="keranjangs" />
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
                Keranjang
              </li>
            </ol>
          </nav>
        </div>
      </div>

      <div class="row">
        <div class="col">
          <h2>Keranjang <strong>Saya</strong></h2>
          <div class="table-responsive mt-3">
            <table class="table">
              <thead>
                <tr>
                  <th scope="col">No.</th>
                  <th scope="col">Foto</th>
                  <th scope="col">Makanan</th>
                  <th scope="col">Keterangan</th>
                  <th scope="col">Jumlah</th>
                  <th scope="col">Harga</th>
                  <th scope="col">Total Harga</th>
                  <th scope="col">Hapus</th>
                </tr>
              </thead>
              <tbody>
                <tr
                  v-for="(keranjang, index) in keranjangs"
                  :key="keranjang.id"
                >
                  <th>{{ index + 1 }}</th>
                  <td>
                    <img
                      :src="'../assets/images/' + keranjang.products.gambar"
                      :alt="keranjang.products.nama"
                      class="img-fluid shadow"
                      width="250"
                    />
                  </td>
                  <td>
                    <strong>{{ keranjang.products.nama }}</strong>
                  </td>
                  <td>
                    {{ keranjang.keterangan ? keranjang.keterangan : "-" }}
                  </td>
                  <td>{{ keranjang.jumlah_order }}</td>
                  <td align="right">Rp. {{ keranjang.products.harga }}</td>
                  <td align="right">
                    <strong
                      >Rp.
                      {{
                        keranjang.jumlah_order * keranjang.products.harga
                      }}</strong
                    >
                  </td>
                  <td align="center" class="text-danger del-keranjang">
                    <b-icon-trash
                      v-on:click="hapusKeranjang(keranjang.id)"
                    ></b-icon-trash>
                  </td>
                </tr>
                <tr>
                  <td colspan="6" align="right">
                    <strong>Total Harga:</strong>
                  </td>
                  <td align="right">
                    <strong>Rp. {{ totalHarga }}</strong>
                  </td>
                  <td></td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>

      <!-- form-checkout -->
      <div class="row justify-content-end">
        <div class="col-md-4">
          <form class="mt-4" v-on:submit.prevent>
            <div class="form-group">
              <label for="nama">Nama : </label>
              <input type="text" class="form-control" v-model="checkout.nama" />
            </div>
            <div class="form-group">
              <label for="noMeja">No Meja : </label>
              <input
                type="text"
                class="form-control"
                v-model="checkout.noMeja"
              />
            </div>
            <button
              type="submit"
              class="btn btn-primary float-right"
              v-on:click="checkoutOrder"
            >
              <b-icon-cart-check></b-icon-cart-check> Checkout
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
  name: "Keranjang",
  components: {
    Navbar,
  },
  data() {
    return {
      keranjangs: [],
      checkout: {},
    };
  },
  methods: {
    setKeranjang(data) {
      this.keranjangs = data;
    },
    hapusKeranjang(id) {
      axios
        .delete("http://localhost:3000/keranjangs/" + id)
        .then(() => {
          this.$toast.error("Isi keranjang berhasil dihapus", {
            type: "error",
            position: "top",
            duration: 3000,
            dismissible: true,
          });
        })
        .catch((err) => console.log(err));

      //update data keranjang
      axios
        .get("http://localhost:3000/keranjangs")
        .then((res) => this.setKeranjang(res.data))
        .catch((err) => console.log(err));
    },
    checkoutOrder() {
      if (this.checkout.nama && this.checkout.noMeja) {
        this.checkout.keranjangs = this.keranjangs;

        // delete value keranjangs
        this.keranjangs.map(function(item){
            return axios.delete("http://localhost:3000/keranjangs/" + item.id)
                   .catch((err) => console.log(err))
        })

        axios
          .post("http://localhost:3000/pesanans", this.checkout)
          .then(() => {
            this.$router.push({ path: "/pesanan-sukses" });
            this.$toast.success("Success Diorder", {
              type: "success",
              position: "top",
              duration: 3000,
              dismissible: true,
            });
          })
          .catch((err) => console.log(err));
      } else {
        this.$toast.error("Nama dan No Meja harus diisi !", {
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
      .get("http://localhost:3000/keranjangs")
      .then((res) => this.setKeranjang(res.data))
      .catch((err) => console.log(err));
  },
  //   computed merupakan fungsi untuk melakukan penjumlahan
  computed: {
    totalHarga() {
      return this.keranjangs.reduce(function (items, data) {
        return items + data.products.harga * data.jumlah_order;
      }, 0);
    },
  },
};
</script>

<style>
</style>