<template>
  <div class="container py-5">
    <div class="row">
      <div class="col-lg-8">
        <h1>Articles</h1>
        <p class="mb-5">
          Temukan berbagai informasi terbaru seputar Informatics Festival (IFest) #9 disini
        </p>

        <div v-for="(article, k) in articles" :key="k" class="mb-4">
          <NuxtLink :to="`/article/`+article.slug">
            <h4 class="mb-0">
              {{ article.title }}
            </h4>
          </NuxtLink>
          <p class="text-black-50 mt-0 mb-1 small">
            By <span class="font-weight-bold">{{ article.user_created.first_name }} {{ article.user_created.last_name }}</span>
            on {{ formatDate(article.date_created) }}
          </p>
          <p>{{ article.short_desc }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import directus from '@/plugins/directus'
import moment from 'moment'

export default {
  name: 'Home',
  async asyncData () {
    const articles = (await directus.items('article').read({
      fields: ['title', 'short_desc', 'slug', 'user_created.*', 'date_created'],
      limit: 10,
      sort: '-date_created'
    })).data
    return { articles }
  },
  data () {
    return {
      articles: []
    }
  },
  methods: {
    formatDate (date) {
      moment.locale('id')
      return moment(date).format('LL')
    }
  }
}
</script>

<style scoped>

</style>
