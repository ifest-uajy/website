<template>
  <div class="container py-5">
    <div class="row">
      <div class="col-lg-8">
        <h1 class="title">{{ article.title }}</h1>
        <div v-if="article.user_created">
          <div class="row no-gutters my-3 align-items-center">
            <div class="col-auto mr-2">
              <b-img
                v-if="article.user_created.avatar"
                rounded="circle"
                :src="`https://cms.ifest-uajy.com/assets/` + article.user_created.avatar"
                height="64"
                width="64"
                class="mr-1"
              />
              <b-img
                v-else
                rounded="circle"
                src="https://cms.ifest-uajy.com/assets/d50813cc-87b3-4e4b-9a80-2d9d1e5f7cbb"
                height="64"
                width="64"
                class="mr-1"
              />
            </div>
            <div class="col">
              <p class="m-0 p-0 font-weight-bold">{{ article.user_created.first_name }} {{ article.user_created.last_name }}</p>
              <p
                class="m-0 p-0 text-black-50"
                style="font-size: 9pt"
              >{{article.user_created.description}}</p>
              <p
                class="m-0 p-0 text-black-50"
                style="font-size: 8.5pt"
              >{{ formatDate(article.date_created) }}</p>
            </div>
          </div>
        </div>
        <div class="content mt-5" v-html="article.content" />
        <div class="attachments" v-if="article.attachments">
          <h2 class="title mb-4">Attachments</h2>
          <div
            v-for="(attachment, k) in article.attachments"
            :key="k"
            class="mb-2 attachments-boxes"
          >
            <div class="row no-gutters align-items-center">
              <div class="col-sm-auto col-auto mx-1">
                <div class="d-flex icon-box align-items-center justify-content-center">
                  <font-awesome-icon
                    :icon="getIconByType(attachment.directus_files_id.type)"
                    style="height: 24px; width: 24px; color: #717d93"
                  />
                </div>
              </div>
              <div class="col">
                <a
                  class="a"
                  style="cursor:pointer; font-weight: 600; color: #212937"
                  :href="`https://cms.ifest-uajy.com/assets/` + attachment.directus_files_id.id + `?download`"
                >
                  {{ attachment.directus_files_id.title }}
                </a>
                <b-card-text class="mt-0 small text-black-50">
                  {{ formatFileSize(attachment.directus_files_id.filesize) }}, {{ formatFileType(attachment.directus_files_id.type) }}
                </b-card-text>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import directus from '@/plugins/directus'
import moment from 'moment'
import prettyBytes from 'pretty-bytes'
import mime from 'mime-types'

export default {
  head () {
    return {
      title: this.title
    }
  },
  data () {
    return {
      article: [],
      title: 'Artikel | Informatics Festival'
    }
  },
  beforeMount () {
    this.getArticle()
  },
  methods: {
    getArticle () {
      directus.items('article').read({
        fields: [
          '*, user_created.*',
          'attachments.directus_files_id.*'
        ],
        filter: {
          slug: {
            _eq: this.$route.params.slug
          }
        },
        single: 1
      }).then((data) => {
        this.article = data.data
        this.title = data.data.title + ' | Informatics Festival'
      })
    },
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
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Open+Sans:wght@400;600&display=swap');

.title {
  color: #212937 !important;
  font-family: 'Open Sans', sans-serif;
  font-weight: 600;
}
.content {
  color: #161616 !important;
  font-family: 'Open Sans', sans-serif;
  margin-bottom: 100px;
}

.attachments {
  margin-bottom: 100px;
  margin-top: -50px;
}

.attachments-boxes {
  border: 2pt solid #9b9b9b;
  transition: ease 0.2s;
  border-radius: 8px;
}

.attachments-boxes:hover {
  border: 2pt solid #717d93;
  transition: ease 0.2s;
}

.content img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 8px;
}
.icon-box {
  background-color: #212937;
  height: 45px;
  width: 45px;
  margin: 10px;
  border-radius: 8px;
}
</style>
