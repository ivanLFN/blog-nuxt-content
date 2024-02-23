<template>
  <div class="default-container">
    <div class="row">
      <div
        v-for="(article, index) of articles"
        :key="article.slug"
        :class="getCardClass(index)"
      >
        <component :is="getComponent(index)" :article="article" class="mt-5 default-card">
        </component>
      </div>
    </div>
  </div>
</template>


<script>
import WideCard from '@/components/WideCard.vue';
import ThinCard from '@/components/ThinCard.vue';

export default {
  name: 'Index',
  components: {
    WideCard,
    ThinCard
  },
  layout: 'Default',
  async asyncData({ $content, params }) {
    const articles = await $content('articles', params.slug)
      .only(['title', 'description', 'img', 'slug', 'author', 'reading', 'createdAt'])
      .sortBy('createdAt', 'asc')
      .fetch()

    return {
      articles
    }
  },
  data() {
    return {
      col6Indexes: Array.from({ length: 10 }, (_, index) => index === 0 ? 0 : index * 10 - 1)
    };
  },
  methods: {
    getComponent(index) {
      return this.isWideCard(index) ? WideCard : ThinCard;
    },
    isWideCard(index) {
      return this.col6Indexes.includes(index);
    },
    getCardClass(index) {
      return this.isWideCard(index) ? 'col-12 col-md-6' : 'col-12 col-md-3';
    }
  }
}
</script>

<style scoped>

.default-card {
  height: 500px;
  border: 2px solid #efefef;
  border-radius: 5px;
}

@media only screen and (max-width: 600px) {
  .default-card {
    height: 350px;
  }
}

</style>
