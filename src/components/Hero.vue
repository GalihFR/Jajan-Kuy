<template>
  <div class="hero">
    <!-- Dekstop -->
    <div class="d-none d-md-block">
      <div class="row mt-4">
        <div class="col-md-6">
          <div class="d-flex h-100">
            <div class="justify-content-center align-self-center">
              <h2>
                <strong>Delicious Food Menu, </strong> <br />in Your Gadget
              </h2>
              <p>Come on, immediately choose your favorite food</p>
              <router-link to="/foods" class="btn btn-lg btn-danger">
                Order <b-icon-arrow-right></b-icon-arrow-right>
              </router-link>
            </div>
          </div>
        </div>
        <div class="col-md-6">
          <img src="../assets/images/hero.png" alt="hero" width="100%" />
        </div>
      </div>
    </div>

    <!-- Mobile -->
    <div class="d-sm-block d-md-none">
      <div class="row mt-4">
        <div class="col-md-6">
          <img src="../assets/images/hero.png" alt="hero" width="100%" />
        </div>
        <div class="col-md-6">
          <div class="d-flex h-100">
            <div class="justify-content-center align-self-center">
              <h2>
                <strong>Delicious Food Menu, </strong> <br />in Your Gadget
              </h2>
              <p>Come on, immediately choose your favorite food</p>
              <button class="btn btn-lg btn-danger">
                Order <b-icon-arrow-right></b-icon-arrow-right>
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Hero",
};
</script>

<style>
</style>