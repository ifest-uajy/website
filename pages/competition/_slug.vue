<template>
  <div class="container my-5">
    <div class="container">
      <div
        class="ccom flickity-enabled aos-init aos-animate"
        data-aos="fade-up"
        data-aos-delay="200"
        data-flickity="{&quot;content&quot;:true, &quot;wrapAround&quot;:true, &quot;autoPlay&quot;:2500, &quot;pageDots&quot;:false, &quot;prevNextButtons&quot;: false}"
        tabindex="0"
      >
        <div class="flickity-viewport" style="height: 350px; touch-action: pan-y;">
          <div class="flickity-slider" style="left: 0px; transform: translateX(0%);">
            <div aria-selected="true" class="dcom bflex is-selected" style="position: absolute; left: 0%;">
              <div class="ldcom">
                <div class="sflex mb-3">
                  <div class="ov-img">
                    <img src="assets/image/I2C.png">
                  </div>
                  <div>
                    <h2>{{ competition.event_name }}</h2>
                  </div>
                </div>
                <div class="cat sflex">
                  <label class="lab l-blue">
                    <span v-if="competition.registration_fee > 0">
                      {{ formatMoney(competition.registration_fee) }}
                    </span>
                    <span v-else>
                      Gratis
                    </span>
                  </label>
                  <label class="lab l-green" style="margin-left: 5px; margin-right: 5px;">SMA/SMK</label>
                  <label class="lab l-red">1 Maret 2021</label>
                </div>
                <p v-html="competition.event_description"></p>
                <a class="btn btn-logins" href="dashboard.ifest-uajy.com">Register</a>
                <a
                  class="a"
                  style="cursor:pointer; font-weight: 600; color: #212937"
                  :href="`https://cms.ifest-uajy.com/assets/` + competition.rulebook + `?download`"
                >
                  Download Rulebook
                </a>
              </div>
              <div class="rdcom">
                <img src="poster/poster-I2C-terbaru.jpg">
              </div>
            </div>
          </div>
        </div>
      </div>
      <img class="abs aos-init aos-animate" data-aos="zoom-in" data-aos-delay="300" src="assets/image/abs2.png">
    </div>
    {{ competition }}
  </div>
</template>

<script>
import directus from '@/plugins/directus'
import moment from 'moment'
import prettyBytes from 'pretty-bytes'
import mime from 'mime-types'

export default {
  name: 'Slug',
  async asyncData ({ params }) {
    const competition = (await directus.items('competition').read({
      fields: [
        '*'
      ],
      filter: {
        slug: {
          _eq: params.slug
        }
      },
      single: 1
    })).data
    return { competition }
  },
  data () {
    return {
      competition: []
    }
  },
  head () {
    return {
      title: this.competition.title + ' | Informatics Festival #9',
      meta: [
        {
          hid: 'twitter:title',
          name: 'twitter:title',
          content: this.competition.event_name
        },
        {
          hid: 'twitter:description',
          name: 'twitter:description',
          content: this.competition.event_description
        },
        {
          hid: 'og:title',
          property: 'og:title',
          content: this.competition.event_name
        },
        {
          hid: 'og:description',
          property: 'og:description',
          content: this.competition.event_description
        },
        {
          hid: 'og:site_name',
          property: 'og:site_name',
          content: 'Informatics Festival (IFest) #9'
        }
      ]
    }
  },
  methods: {
    formatDate (date) {
      moment.locale('id')
      return moment(date).format('LL')
    },
    formatFileSize (size) {
      return prettyBytes(size)
    },
    getIconByType (type) {
      const iconClasses = {
        image: 'file-image',
        'application/pdf': 'file-pdf',
        'application/zip': 'file-archive'
      }
      for (const key in iconClasses) {
        // eslint-disable-next-line no-prototype-builtins
        if (iconClasses.hasOwnProperty(key)) {
          if (type.search(key) === 0) {
            return iconClasses[key]
          }
        } else {
          return 'file'
        }
      }
    },
    formatFileType (fileType) {
      return mime.extension(fileType).toUpperCase()
    },
    formatMoney (price) {
      const formatter = new Intl.NumberFormat('id-ID', {
        style: 'currency',
        currency: 'IDR'
      })
      return formatter.format(price)
    }
  }
}
</script>

<style scoped>
.ccom {
  position: relative;
  height: auto;
  width: 100%;
  padding: 0px 45px 35px;
  box-sizing: border-box;
  z-index: 1;
}

.ccom:before {
  position: absolute;
  content: '';
  height: 350px;
  width: 100%;
  bottom: 0;
  left: 0;
  margin: auto;
  border-radius: 35px;
  transform: rotate(2deg);
  background-image: linear-gradient(#6C7BFF, #00A3FF);
  z-index: 0;
}

 *,*:focus,*:hover{
   outline:none;
 }
</style>
