<template>
  <article>
    <ul>
      <li v-for="link in article.toc" :key="link.id">
        <a :href="`#${link.id}`" class="text-decoration-none">
          <div>
            <div class="v-list-item">
              <div class="v-list-item-title">{{ link.text }}</div>
            </div>
          </div>
        </a>
      </li>
    </ul>
    <h1>{{ article.title }}</h1>
    <p>{{ article.description }}</p>
    <img
      :src="require(`~/static/articles/${article.img}`)"
      :alt="article.alt"
    />
    <p>Article last updated: {{ formatDate(article.updatedAt) }}</p>

    <nuxt-content :document="article" />

    <AuthorComponent :author="article.author" />

    <PrevNext :prev="prev" :next="next" />
  </article>
</template>

<script>

  export default {
    async asyncData({ $content, params }) {
      const article = await $content('articles', params.slug).fetch()

      const [prev, next] = await $content('articles')
        .only(['title', 'slug'])
        .sortBy('createdAt', 'asc')
        .surround(params.slug)
        .fetch()

      return {
        article,
        prev,
        next
      }
    },
    methods: {
        formatDate(date) {
            const options = { year: 'numeric', month: 'long', day: 'numeric' };
            return new Date(date).toLocaleDateString('en', options);
        }
    }
}
</script>

<style>

.nuxt-content h2 {
  font-weight: bold;
  font-size: 28px;
}

.nuxt-content h3 {
  font-weight: bold;
  font-size: 22px;
}

.nuxt-content p {
  margin-bottom: 20px;
}
</style>
