<template>
  <div>
    <Header />
    <Nuxt />
    <Footer />
  </div>
</template>

<script>
import Footer from '@/layouts/Footer'
import Header from '~/layouts/Header'
export default {
  components: { Footer, Header },
  mounted () {
    this.$nextTick(function () {
      window.addEventListener('scroll', function () {
        const navbar = document.getElementById('nav')
        const logo = document.getElementById('logo-image')
        const navClasses = navbar.classList
        const logoClasses = logo.classList
        if (document.documentElement.scrollTop > 50) {
          navClasses.add('nav-shrink')
          logoClasses.remove('image-hidden')
        } else {
          navClasses.remove('nav-shrink')
          logoClasses.add('image-hidden')
        }
      })
    })
  }
}
</script>
