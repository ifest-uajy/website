<template>
  <div class="container-xl">
    <b-navbar toggleable="lg" variant="light">
      <b-navbar-toggle target="nav-collapse" />
      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav class="ml-auto">
          <b-nav-item-dropdown text="Competition">
            <b-dropdown-item href="#">
              I2C
            </b-dropdown-item>
            <b-dropdown-item href="#">
              Competitive Programming
            </b-dropdown-item>
            <b-dropdown-item href="#">
              Multi Event
            </b-dropdown-item>
            <b-dropdown-item href="#">
              WDC
            </b-dropdown-item>
          </b-nav-item-dropdown>
          <b-nav-item-dropdown text="Talks">
            <b-dropdown-item href="#">
              Seminar Nasional
            </b-dropdown-item>
            <b-dropdown-item href="#">
              Sharing Alumni
            </b-dropdown-item>
          </b-nav-item-dropdown>
          <b-nav-item>Register</b-nav-item>
          <b-nav-item>Login</b-nav-item>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </div>
</template>

<script>
export default {
  name: 'Header'
}
</script>

<style scoped>

</style>
