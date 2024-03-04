<template>
  <div class="container">
    <article>
      <div class="row d-flex mt-5">
        <div class="col">
          <nav aria-label="breadcrumb">
          <ol class="breadcrumb">
            <li class="breadcrumb-item"><a class="breadcrumb-link" href="/">Home</a></li>
            <li class="breadcrumb-item"><a class="breadcrumb-link" href="/blog">Blog</a></li>
            <li class="breadcrumb-item active" aria-current="page">{{ article.title }}</li>
          </ol>
        </nav>
        </div>
        <div class="col d-flex justify-content-end">
          <a class="sections-link" href="#" data-bs-toggle="collapse" data-bs-target="#multiCollapseExample2" aria-expanded="false" aria-controls="multiCollapseExample2">Article sections</a>
        </div>
      </div>
      <div class="d-flex justify-content-end">
        <div>
          <div id="multiCollapseExample2" class="collapse multi-collapse">
            <div class="card card-body">
              <ul>
                <li v-for="link in article.toc" :key="link.id">
                  <a :href="`#${link.id}`" class="section-link">
                    <div>
                      <div class="v-list-item">
                        <div class="v-list-item-title">{{ link.text }}</div>
                      </div>
                    </div>
                  </a>
                </li>
              </ul>
            </div>
          </div>
        </div>
      </div>

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
  </div>
</template>

<script>
export default {
  layout: 'Default',
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
      next,
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

<style>

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

.card {
  border: none;
}

.section-link {
  font-size: 1.2rem;
  color: rgb(168, 168, 168);
  transition: color 0.5s ease;
}

.section-link:hover {
  color: #7b4dff;
  text-decoration: none;
}

.sections-link {
  font-size: 1.3rem;
  color: rgb(168, 168, 168);
  transition: color 0.5s ease;
}

.sections-link:hover {
  color: #272727;
  text-decoration: none;
}

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
