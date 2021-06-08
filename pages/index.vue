<template>
  <main>
    <carousel
      class="index-carousel w-full mb-8"
    />
    <section class="mt-8">
      <h3 class="text-primary-600 dark:text-primary-400 max-w-5xl mx-auto">Berita terkini</h3>
      <posts post-type="bola" :amount="6" />
    </section>

    <a href="https://103.3.61.238/?utm_medium=blog&utm_source=ads&utm_campaign=daily%20bola%20ads" class="self-center w-full md:w-1/2 mt-2">
      <picture class="w-full">
        <source srcset="/img/live22-euro-guess2win-desktop.jpg" media="(min-width: 500px)">
        <img src="/img/live22-euro-guess2win.jpg" alt="JUDIBRO">
      </picture>
    </a>
  </main>
</template>

<script>
import carousel from '~/components/posts/carousel.vue'
export default {
  components: { carousel },
  
}
</script>
<style scoped>

</style>