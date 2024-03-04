<template>
  <div class="row d-flex mt-5">
    <div class="col">
      <NuxtLink
        v-if="prev"
        :to="{ name: 'blog-slug', params: { slug: prev.slug } }"
        class="left-link"
      >
        {{ prev.title }}
      </NuxtLink>
    </div>
    <div class="col">
      <div class="d-flex justify-content-end">
        <NuxtLink
          v-if="next"
          :to="{ name: 'blog-slug', params: { slug: next.slug } }"
          class="right-link"
        >
          {{ next.title }}
        </NuxtLink>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    prev: {
      type: Object,
      default: () => null,
    },
    next: {
      type: Object,
      default: () => null,
    },
  },
}
</script>

<style scoped>

.left-link {
  font-size: 1.3rem;
  color: #272727;
  transition: color 0.5s ease;
}

.left-link:hover {
  color: #7b4dff;
}

.right-link {
  font-size: 1.3rem;
  color: #272727;
  transition: color 0.5s ease;
}

.right-link:hover {
  color: #7b4dff;
}

</style>