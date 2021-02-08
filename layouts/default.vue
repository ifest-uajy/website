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
        const navClasses = navbar.classList
        if (document.documentElement.scrollTop > 50) {
          navClasses.add('nav-shrink')
        } else {
          navClasses.remove('nav-shrink')
        }
      })
    })
  }
}
</script>
