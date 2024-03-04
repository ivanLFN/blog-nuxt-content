<template>
  <div class="w-100 py-5">
    <div class="d-flex justify-content-end">
      <NuxtLink class="nuxt-link" :to="`/blog/author/${author.name}`">
        <div class="d-flex align-items-center">
          <img class="author-img rounded-circle" :src="author.image" alt="..." />
          <div class="author-link">
            <div>Author</div>
            <div>{{ author.name }}</div>
            <div class="author-page">{{ author.bio }}</div>
          </div>
        </div>
      </NuxtLink>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    author: {
      type: Object,
      required: true,
    },
  },
}
</script>

<style scoped>

.nuxt-link {
  text-decoration-color: #272727;
}

.author-link {
  font-size: 1.5rem !important;
  padding-left: 30px;
  color: #272727;
}

.author-page {
  font-size: 1rem !important;
}

.author-img {
  width: 150px;
  height: 150px;
  border-radius: 50%;
  border: 5px solid #272727;
}

</style>
