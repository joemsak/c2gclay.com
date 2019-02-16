<template>
  <div id="app" class="container-fluid">
    <div id="logo-wrapper">
      <div id="logo" class="mt-5"></div>
    </div>

    <div id="cover" class="d-flex justify-content-center">
      <i @click="scrollToFirst" class="fas fa-chevron-down"></i>
    </div>

    <img id="first" width="100%" src="./assets/galleries/vajilla-ricky/DSCF8208.jpg" />
    <img width="100%" src="./assets/galleries/vajilla-ricky/DSCF8282.jpg" />
    <img width="100%" src="./assets/galleries/vajilla-ricky/DSCF8271.jpg" />
    <img width="100%" src="./assets/galleries/vajilla-ricky/DSCF8196.jpg" />
    <img width="100%" src="./assets/galleries/vajilla-ricky/DSCF8297.jpg" />
  </div>
</template>

<script>
import $ from 'jquery'

export default {
  name: 'app',

  methods: {
    scrollToFirst () {
      const target = $("#first")

      $('html, body').animate({
        scrollTop: target.offset().top
      }, 500, function() {
        var $target = $(target)
        $target.focus()

        if ($target.is(":focus")) {
          return false
        } else {
          $target.attr('tabindex','-1')
          $target.focus()
        }
      })
    },
  },

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
