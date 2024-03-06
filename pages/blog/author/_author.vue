<template>
  <div>
    <div class="container-sm">
      <div class="row author-el align-items-center">
        <div class="col-md-4 col-12 d-flex justify-content-center">
          <img class="author-img rounded-circle" :src="articles[0].author.image" alt="..." />
        </div>
        <div class="col-md-8 col-12">
          <div class="author-name">
              {{ articles[0].author.name }}
          </div>

          <nav aria-label="breadcrumb">
            <ol class="breadcrumb">
              <li class="breadcrumb-item"><a class="breadcrumb-link" href="/">Home</a></li>
              <li class="breadcrumb-item"><a class="breadcrumb-link" href="/blog">Blog</a></li>
              <li class="breadcrumb-item active" aria-current="page">{{ articles[0].author.name }}</li>
            </ol>
          </nav>
          <div class="author-bio">
            {{ articles[0].author.bio }}
          </div>
        </div>
      </div>
    </div>
    <div class="w-100 mt-5 wive-backround d-flex justify-content-center align-items-center">
      <div class="articles-section">
        <div class="author-name">
          {{ articles[0].author.name }}'s articles
        </div>
        <div>
          <div>
            <div v-for="article in articles" :key="article.slug">
              <NuxtLink class="article-link" :to="{ name: 'blog-slug', params: { slug: article.slug } }">
                <div class="d-flex align-items-center mt-3">
                  <div class="d-flex justify-content-center">
                    <img src="/images/icons8-article-64.png" alt="..." />
                  </div>
                  <div>
                    <div>
                      <div class="article article-date">{{ formatDate(article.updatedAt) }}</div>
                      <div class="article article-header">{{ article.title }}</div>
                      <div class="article article-desc">{{ article.description }}</div>
                    </div>
                  </div>
                </div>
              </NuxtLink>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    layout: 'Default',
    async asyncData({ $content, params }) {
      const articles = await $content('articles')
        .where({
          'author.name': {
            $regex: params.author,
            $options: 'i'
          }
        })
        .without('body')
        .sortBy('createdAt', 'asc')
        .fetch()

      return {
        articles
      }
    },
    methods: {
      formatDate(date) {
        const options = { year: 'numeric', month: 'long', day: 'numeric' }
        return new Date(date).toLocaleDateString('en', options)
      }
    }
  }
</script>

<style scoped>

.article-link {
  text-decoration: none;
  transition: color 1s ease;
}

.article-link:hover {
  color: #7b4dff;
}

.article {
  color: #272727;
}

.article-header {
  font-size: 1.5rem;
  font-weight: 500;
}

.article-date {
  font-size: 1.1rem;
}

.articles-section {
  margin-top: 180px;
  margin-bottom: 280px;
}

.wive-backround {
  background-image: url('/images/wave_backround.png');
  background-size: cover;
  height: auto;
}

.breadcrumb-link {
  color: #7f7f7f;
  transition: color 0.5s ease;
}

.breadcrumb-link:hover {
  color: #7b4dff;
}

.breadcrumb .active {
  color: #272727;
}

.breadcrumb {
  background-color: white;
}

.author-bio {
  margin-top: 20px;
  color: #272727;
  font-size: 1.3rem;
}

.author-name {
  font-weight: bold;
  font-size: 2.2rem;
  color: #272727;
  margin-bottom: 20px;
}

.author-el {
  margin-top: 5rem;
}

.author-link {
  font-size: 1.5rem !important;
  padding-left: 30px;
  color: #272727;
}

.author-img {
  width: 350px;
  height: 350px;
  border-radius: 50%;
  border: 5px solid #272727;
}


</style>
