<template>
  <div>
    <client-only>
      <NuxtLink :to="{ name: 'blog-slug', params: { slug: article.slug } }">
        <img :src="article.img" />
        <div>
          <h2>{{ article.title }}</h2>
          <p>by {{ article.author.name }}</p>
          <p>{{ article.description }}</p>
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
      required: true
    }
  }
}
</script>
