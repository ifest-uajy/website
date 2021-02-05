<template>
  <div class="footer py-5 text-light">
    <div class="container">
      <div class="row no-gutters">
        <div class="col-sm-12 col-md-12 col-lg-8">
          <div class="row no-gutters">
            <div class="col-md-4">
              <p class="mb-3 font-weight-bold" style="opacity: 0.7;">
                Competitions
              </p>
              <p v-for="(competition, k) in competitions" :key="k">
                {{ competition.event_name }}
              </p>
              <p v-if="competitions === {}">
                Coming Soon
              </p>
            </div>
            <div class="col-md-4">
              <p class="mb-3 font-weight-bold" style="opacity: 0.7;">
                Events
              </p>
              <p v-if="events">
                Coming Soon
              </p>
            </div>
            <div class="col-md-4">
              <p class="mb-3 font-weight-bold" style="opacity: 0.7;">
                Access
              </p>
              <p>Registration</p>
              <p>Login</p>
            </div>
          </div>
        </div>
        <div class="col">
          <p class="mb-3 font-weight-bold" style="opacity: 0.7;">
            Subscribe
          </p>
          <p>Daftar <em>newsletter</em> Informatics Festival agar tidak tertinggal informasi terkini.</p>
          <div class="row no-gutters">
            <div class="col-8 col-sm-8 col-md-8 col-lg-8">
              <b-input disabled placeholder="Masukkan email..." />
            </div>
            <div class="col ml-2 ml-md-2 mt-sm-0 ml-sm-2 mt-md-0 ml-lg-2 mt-lg-0">
              <b-btn variant="primary" disabled block>
                Daftar
              </b-btn>
            </div>
            <p class="small text-light pt-3" style="opacity: 0.7">
              Kami tidak akan melakukan <em>spam</em> kepada email kamu.
            </p>
          </div>
        </div>
      </div>
      <hr class="bg-light" style="opacity: 0.4">
      <div class="row">
        <div class="col">
          &copy; {{ new Date().getFullYear() }} <strong>Informatics Festival (IFest)</strong>. Hak Cipta Dilindungi.
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import directus from '@/plugins/directus'

export default {
  name: 'Footer',
  data () {
    return {
      competitions: [],
      events: []
    }
  },
  beforeMount () {
    this.getCompetitions()
  },
  methods: {
    getCompetitions () {
      directus.items('competition').read({
        fields: 'event_name'
      }).then((data) => {
        this.competitions = data.data
      })
    }
  }
}
</script>

<style scoped>
.footer{
  background-color: #212937;
}
.hfooter{
  align-items: flex-start;
}
.hfooter li{
  font-family: medium;
  display: block;
  list-style: none;
  color: #959CA8;
  margin-top: 15px;
  text-transform: uppercase;
}
.hfooter a{
  font-family: regular;
  text-transform: none;
  color: #fff;
}
.hfooter p{
  text-transform: none;
  font-size: 15px;
  color: #959CA8;
}

.bfooter{
  height: auto;
  width: 100%;
  margin-top: 50px;
  padding-top: 25px;
  border-top: 1.5px solid #545c6b;
}
.bfooter p{
  font-size: 15px;
  color: #959CA8;
}
.bfooter li{
  display: inline-block;
  list-style: none;
  margin: 0 10px;
}
.bfooter i{
  font-size: 15px;
  color: #959CA8;
  transition: .5s;
}
.bfooter a{
  text-decoration: none;
}
.bfooter a:hover i{
  color: #fff;
  transition: .5s;
}
.bflex {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.sflex {
  display: flex;
  align-items: center;
  justify-content: flex-start;
}

</style>
