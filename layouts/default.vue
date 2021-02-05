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
  components: { Footer, Header }
}
</script>
