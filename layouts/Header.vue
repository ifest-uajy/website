<template>
  <div class="container ifest-header">
    <b-navbar id="nav" class="navbar fixed-top navbar-light bg-light ifest-nav" toggleable="lg">
      <div class="container">
        <b-navbar-brand to="/">
          <img id="logo-image" class="ifest-header--image-logo" :src="images.logo" alt="Logo">
        </b-navbar-brand>
        <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>
        <b-collapse id="nav-collapse" is-nav>
          <b-navbar-nav class="ml-auto">
            <b-nav-item-dropdown text="Competition" :disabled="competitions.length <= 0">
              <b-dropdown-item
                v-for="(competition, k) in competitions"
                :key="k"
                :to="`/competition/` + competition.slug"
              >
                {{ competition.event_name }}
              </b-dropdown-item>
            </b-nav-item-dropdown>
            <b-nav-item-dropdown text="Events" :disabled="events.length <= 0">
              <b-dropdown-item
                v-for="(event, k) in events"
                :key="k"
                :to="`/competition/` + event.slug"
              >
                {{ event.event_name }}
              </b-dropdown-item>
            </b-nav-item-dropdown>
            <b-nav-item to="/article">
              Article
            </b-nav-item>
            <b-nav-item>Register</b-nav-item>
            <b-nav-item>Login</b-nav-item>
          </b-navbar-nav>
        </b-collapse>
      </div>
    </b-navbar>
  </div>
</template>

<script>
import directus from '~/plugins/directus'

export default {
  name: 'Header',
  data () {
    return {
      competitions: [],
      events: [],
      images: {
        logo: require('@/assets/images/logo.png')
      }
    }
  },
  async fetch () {
    this.competitions = (await directus.items('competition').read({
      fields: ['event_name', 'slug']
    })).data
  }
}
</script>

<style scoped>
.ifest-header {
  background-color: #ffffff;
  margin-bottom: 150px;
}
.ifest-header--image-logo {
  max-height: 50px;
  margin-top: 10px;
  margin-bottom: 10px;
}
.ifest-nav {
  padding-top: 30px;
  padding-bottom: 30px;
  background-color: #fff !important;
  transition: .5s;
}
.nav-shrink {
  padding-top: 5px;
  padding-bottom: 5px;
  box-shadow: 0px 3px 5px rgb(245 246 245);
  transition: .5s;
}
</style>
