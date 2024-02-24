<template>
  <div class="overflow-hidden">
    <client-only>
      <NuxtLink
        :to="{ name: 'blog-slug', params: { slug: article.slug } }"
        class="nuxt-link-wrapper"
      >
        <div class="row nuxt-link-content">
          <div class="col-11 col-md-7">
            <div class="px-5 pt-5">
              <p class="created-at-style">
                {{ formatDate(article.createdAt) }}
              </p>
              <div>
                <div class="article-title">{{ article.title }}</div>
              </div>
            </div>
            <div class="position-absolute bottom-0 pb-4 pl-5">
              <p class="reading-style">READ {{ article.reading }} MIN</p>
            </div>
          </div>
          <div class="col-1 col-md-5 overflow-hidden">
            <img :src="`/articles/${article.img}`" class="card-image" />
          </div>
        </div>
      </NuxtLink>
    </client-only>
  </div>
</template>

<script>
export default {
  props: {
    article: {
      type: Object,
      required: true,
    },
  },
  methods: {
    formatDate(date) {
      const options = { year: 'numeric', month: 'long', day: 'numeric' }
      return new Date(date).toLocaleDateString('en', options)
    },
  },
}
</script>

<style scoped>
.nuxt-link-wrapper .card-image {
  transition: transform 1s ease;
}

.nuxt-link-wrapper:hover .card-image {
  transform: scale(1.1);
  transition: transform 1s ease;
}

.nuxt-link-wrapper:hover {
  text-decoration: none;
}

.nuxt-link-wrapper:hover .article-title {
  color: #7c4dff;
}

.reading-style {
  color: #7c4dff;
}

.created-at-style {
  color: #4f4f4f;
}

.article-title {
  color: #272727;
  text-decoration: none;
  font-weight: 700;
  font-size: 2rem;
  transition: color 1s ease;
}

.nuxt-link-wrapper {
  display: block;
  height: 100%;
  background-color: #fafafa;
}

.nuxt-link-content {
  height: 100%;
}

.card-image {
  display: block;
  margin: 0 auto;
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.article-title {
  margin-top: 8rem;
}

@media only screen and (max-width: 600px) {
  .article-title {
    margin-top: 1rem;
  }
}
</style>
