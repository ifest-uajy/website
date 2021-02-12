<template>
  <div class="container-xl mt-5">
    <b-row>
      <b-col
        v-for="(article, k) in articles"
        :key="k"
        class="col-md-4"
      >
        <b-card
          :title="article.title"
          img-src="https://picsum.photos/600/300/?image=25"
          img-alt="Image"
          img-top
          tag="article"
          class="mb-2"
        >
          <b-card-text v-html="article.short_desc" />
          <NuxtLink :to="`/article/`+article.slug">
            Read More
          </NuxtLink>
        </b-card>
      </b-col>
    </b-row>
    <div class="card-columns">
      <b-card v-for="(faq, k) in faqs" :key="k" :title="faq.title">
        <b-card-text v-html="faq.content" />
      </b-card>
    </div>
  </div>
</template>

<script>
import directus from '@/plugins/directus'

export default {
  name: 'Home',
  async asyncData () {
    const articles = (await directus.items('article').read({
      limit: 2,
      sort: '-date_created'
    })).data
    const faqs = (await directus.items('faq').read()).data
    return { articles, faqs }
  },
  data () {
    return {
      articles: {},
      faqs: {}
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
@media (min-width: 576px) {
  .card-columns {
    column-count: 1;
  }
}

@media (min-width: 768px) {
  .card-columns {
    column-count: 2;
  }
}

@media (min-width: 992px) {
  .card-columns {
    column-count: 2;
  }
}

@media (min-width: 1200px) {
  .card-columns {
    column-count: 2;
  }
}
</style>
