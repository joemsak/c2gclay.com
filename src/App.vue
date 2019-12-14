<template>
  <div id="app" class="container-fluid">
    <div id="logo-wrapper">
      <div id="logo"></div>
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
      const logoWrapper = document.querySelector("#logo-wrapper")
      const logo = logoWrapper.querySelector("#logo")
      const coverHeight = document.querySelector("#cover").offsetHeight * 0.55

      let fullSizeWidth
      let fullSizeHeight

      if (window.innerWidth > 900) {
        fullSizeWidth = 850
        fullSizeHeight = 207
      } else if (window.innerWidth > 600) {
        fullSizeWidth = 550
        fullSizeHeight = 134
      } else {
        fullSizeWidth = 350
        fullSizeHeight = 85
      }

      if (
            document.body.scrollTop > coverHeight ||
              document.documentElement.scrollTop > coverHeight
         ) {
        logo.style.width = "200px"
        logo.style.height = "49px"
        logo.classList.add("ml-3")
        logoWrapper.classList.add("scrolled")
      } else {
        logo.style.width = `${fullSizeWidth}px`
        logo.style.height = `${fullSizeHeight}px`
        logo.classList.remove("ml-3")
        logoWrapper.classList.remove("scrolled")
      }
    }
  },
}
</script>

<style lang="scss">
@import '../node_modules/bootstrap/scss/bootstrap.scss';
@import 'assets/scss/app.scss';
</style>``
