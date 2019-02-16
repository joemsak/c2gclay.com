<template>
  <div id="app" class="container-fluid">
    <div id="logo-wrapper">
      <div id="logo" class="mt-5"></div>
    </div>

    <div id="cover" class="d-flex justify-content-center">
      <i @click="scrollToGallery" class="fas fa-chevron-down"></i>
    </div>

    <div id="gallery">
      <img
        v-for="fileName in galleryFileNames"
        :key="fileName"
        width="100%"
        :srcset="getSrcSet(fileName)"
        sizes="100vw"
        :src="getImgUrl(fileName)"
      />
    </div>
  </div>
</template>

<script>
import $ from 'jquery'

export default {
  name: 'app',

  data () {
    return {
      galleryFileNames: [
        'DSCF8208',
        'DSCF8282',
        'DSCF8271',
        'DSCF8196',
        'DSCF8297',
      ],
    }
  },

  methods: {
    getSrcSet (fileName) {
      return `
        ${this.getImgUrl(fileName, 640, 2)} 640w,
        ${this.getImgUrl(fileName, 1125, 3)} 1125w,
        ${this.getImgUrl(fileName)} 2000w
      `
    },

    getImgUrl (fileName, size, dpr) {
      const images = require.context('./assets/galleries/vajilla-ricky/', false, /\.jpg$/)

      if (size) {
        return images(`./${fileName}-${size}@${dpr}x.jpg`)
      } else {
        return images(`./${fileName}.jpg`)
      }
    },

    scrollToGallery () {
      const target = $("#gallery")

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
  },
}
</script>

<style lang="scss">
@import '../node_modules/bootstrap/scss/bootstrap.scss';
@import 'assets/scss/app.scss';
</style>``
