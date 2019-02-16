<template>
  <div id="app" class="container-fluid">
    <div id="logo-wrapper">
      <div id="logo" class="mt-5"></div>
    </div>

    <div id="cover"></div>
    <img width="100%" src="./assets/galleries/vajilla-ricky/DSCF8208.jpg" />
    <img width="100%" src="./assets/galleries/vajilla-ricky/DSCF8282.jpg" />
    <img width="100%" src="./assets/galleries/vajilla-ricky/DSCF8271.jpg" />
    <img width="100%" src="./assets/galleries/vajilla-ricky/DSCF8196.jpg" />
    <img width="100%" src="./assets/galleries/vajilla-ricky/DSCF8297.jpg" />
  </div>
</template>

<script>
export default {
  name: 'app',

  created() {
    window.onscroll = function() { scrollFunction() }

    function scrollFunction() {
      const logo = document.querySelector("#logo")
      const coverHeight = document.querySelector("#cover").offsetHeight * 0.55

      if (document.body.scrollTop > coverHeight || document.documentElement.scrollTop > coverHeight) {
        logo.style.width = "50px"
        logo.style.height = "50px"
        logo.classList.remove("mt-5")
        logo.classList.add("ml-3", "mt-3")
      } else {
        logo.style.width = "250px"
        logo.style.height = "250px"
        logo.classList.add("mt-5")
        logo.classList.remove("ml-3", "mt-3")
      }
    }
  }
}
</script>

<style lang="scss">
@import '../node_modules/bootstrap/scss/bootstrap.scss';
@import 'assets/scss/app.scss';
</style>``
