<template>
  <div class="wrapper">
    <div class="menu-nav">
      <MenuNav />
    </div>
    <div class="content">
      <nuxt />
    </div>
    <div class="footer">
      <FooterComponent />
    </div>
  </div>
</template>

<script>
import MenuNav from '~/components/MenuNav.vue'
import FooterComponent from '~/components/FooterComponent.vue'

export default {
  components: {
    MenuNav,
    FooterComponent
  }
}
</script>

<style scoped>
.wrapper {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

.content {
  flex: 1;
}

.footer {
  flex-shrink: 0;
}

</style>