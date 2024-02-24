<template>
  <div class="default-container">
    <div>
      <div class="page-title">Blog</div>
    </div>
    <div class="row d-flex flex-wrap tags align-items-center">
      <nuxt-link
        :to="{ path: `/blog/` }"
        class="tag col-auto ml-3"
        :class="{ 'tag-active': !currentTag }"
        >ALL</nuxt-link
      >
      <div v-for="tag of tags" :key="tag" class="col-auto">
        <nuxt-link
          :to="{ path: `/blog/tag/${tag}`, query: { tagsArray: tags } }"
          class="tag"
          :class="{ 'tag-active': currentTag && currentTag === tag }"
        >
          {{ tag.toUpperCase() }}
        </nuxt-link>
      </div>
    </div>
    <div class="row">
      <div
        v-for="(article, index) of articles"
        :key="article.slug"
        :class="getCardClass(index)"
      >
        <component
          :is="getComponent(index)"
          :article="article"
          class="mt-5 default-card"
        >
        </component>
      </div>
    </div>
  </div>
</template>

<script>
import WideCard from '@/components/WideCard.vue'
import ThinCard from '@/components/ThinCard.vue'
export default {
  components: {
    WideCard,
    ThinCard,
  },
  layout: 'Default',
  async asyncData({ $content, params, route }) {
    const articles = await $content('articles')
      .where({
        tags: {
          $regex: params.tag,
          $options: 'i',
        },
      })
      .sortBy('createdAt', 'asc')
      .fetch()

    const tags = route.query.tagsArray || []
    const currentTag = params.tag || null

    return {
      articles,
      tags,
      currentTag,
    }
  },
  data() {
    return {
      col6Indexes: Array.from({ length: 10 }, (_, index) =>
        index === 0 ? 0 : index * 10 - 1
      ),
    }
  },
  methods: {
    getComponent(index) {
      return this.isWideCard(index) ? WideCard : ThinCard
    },
    isWideCard(index) {
      return this.col6Indexes.includes(index)
    },
    getCardClass(index) {
      return this.isWideCard(index) ? 'col-12 col-md-6' : 'col-12 col-md-3'
    },
  },
}
</script>

<style scoped>
.tag-active {
  background-color: #7b4dff !important;
  color: white !important;
  border: 2px solid #7b4dff !important;
  font-weight: 600;
  padding: 5px 15px;
  font-size: 0.95rem;
  border-radius: 5px;
}

.tag-active:hover {
  text-decoration: none;
}

.tag {
  background-color: white;
  color: black;
  font-weight: 600;
  border: 2px solid #efefef;
  padding: 5px 15px;
  font-size: 0.95rem;
  border-radius: 5px;
  transition: background-color 0.5s ease;
}

.tag:hover {
  text-decoration: none;
  background-color: rgb(242, 242, 242);
}

.tags {
  margin-top: 4rem;
  margin-bottom: 1vm;
}

.default-card {
  height: 500px;
  border: 2px solid #efefef;
  border-radius: 5px;
}

.page-title {
  font-size: 4rem;
  color: #272727;
  font-weight: 600;
  margin-top: 6rem;
}

@media only screen and (max-width: 600px) {
  .default-card {
    height: 350px;
  }

  .page-title {
    font-size: 2.5rem;
    margin-top: 3rem;
  }

  .tags {
    margin-top: 2rem;
    margin-bottom: 1rem;
  }
}
</style>
