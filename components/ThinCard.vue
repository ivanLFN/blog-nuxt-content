<template>
  <div>
    <client-only>
      <NuxtLink
        :to="{ name: 'blog-slug', params: { slug: article.slug } }"
        class="parent-link nuxt-link-wrapper"
      >
        <div class="img-style">
          <img :src="`/articles/${article.img}`" class="card-image" />
        </div>
        <div class="content p-3">
          <p class="created-at-style">{{ formatDate(article.createdAt) }}</p>
          <div>
            <div class="article-title">{{ article.title }}</div>
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
.article-title {
  color: #272727;
  text-decoration: none;
  font-weight: 700;
  font-size: 1.5rem;
  transition: color 1s ease;
}

.created-at-style {
  color: #4f4f4f;
}

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

.parent-link {
  display: flex;
  flex-direction: column;
  height: 100%;
}

.img-style {
  flex: 1;
  overflow: hidden;
}

.content {
  flex: 1;
}

.img-style img {
  height: 100%;
  width: 100%;
}

.card-image {
  display: block;
  margin: 0 auto;
  width: 100%;
  height: 100%;
  object-fit: cover;
}
</style>
