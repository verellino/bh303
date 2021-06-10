<template>
  <div class="carousel md:px-12"> 
    <VueSlickCarousel class="w-full h-full" :arrows="true" :dots="true" v-if="posts.length > 0" v-bind="settings">
            <li
            v-for="(post, index) in posts"
            :key="index"
            >
                <nuxt-link
                    :to="`${postType}/${post.slug}`"
                >
                    <template v-if="postType === 'bola'" class="relative h-full p-8" >
                       <img
                          v-if="post.cover"
                          class="carousel-img"
                          :src="post.cover"
                        >
                        <span class="carousel-span px-3 md:px-8 pb-3 pt-4" >
                            <h6 class="inline-block py-1 mr-1 bg-gold-600 text-white text-sm font-bold rounded-sm">{{ post.category }}</h6>
                            <h3 class="card-title text-yellow-500">{{ post.title }}</h3>
                            <p class="mt-2 text-white text-xs pl-1">{{ post.description }}</p>
                        </span>
                    </template>

                    <template v-else>
                        <span class="w-full">
                            <span class="flex justify-between align-baseline">
                            <h3 class="card-title text-lg">{{ post.title }}</h3>
                            <h6
                                v-if="post.createdAt"
                                class="self-start inline-block mt-0 py-1 px-2 bg-gray text-white font-medium rounded-sm whitespace-no-wrap text-xs"
                            >{{ formatDate(post.createdAt) }}</h6>
                            </span>
                            <p class="mt-2 text-base">{{ post.description }}</p>
                        </span>
                    </template>
                </nuxt-link>
            </li>
         </VueSlickCarousel>
    <p v-else class="max-w-5xl mx-auto">
        {{ amount > 1 ? 'Posts not found' : 'Post not found' }}
    </p>
  </div>
</template>

<style lang="css" scoped>
.carousel-span{
    position: absolute;
    display: block;
    width: 100%;
    bottom: 0.2em;
    background: linear-gradient(0deg, black, rgba(255, 255, 255, 0));
}
.carousel-img{
    width: 100%;
    height: 420px;
    object-fit: cover;
    opacity: 0.9;
}
.slick-slide{
     height: 370px; 
}
.slick-dots{
  bottom: 0;
}
.slick-prev, .slick-next, .slick-prev:before, .slick-next:before{
  color: #d69e2e;
  z-index: 99;
}
.slick-next {
    right: 8px;
}
.slick-prev{
  left: 8px;
}
</style>
 
<script>
  import VueSlickCarousel from 'vue-slick-carousel'
  import 'vue-slick-carousel/dist/vue-slick-carousel.css'
  // optional style for arrows & dots
  import 'vue-slick-carousel/dist/vue-slick-carousel-theme.css'
 
  export default {
    name: 'MyComponent',
    components: { VueSlickCarousel },
    props: {
      postType: {
        type: String,
        default: 'bola',
        validator: (val) => ['blog', 'projects', 'bola'].includes(val),
      },
      amount: { // ? https://content.nuxtjs.org/fetching#limitn
        type: Number,
        default: 10,
        validator: (val) => val >= 0 && val < 100,
      },
      sortBy: { // ? https://content.nuxtjs.org/fetching#sortbykey-direction
        type: Object,
        default: () => ({
          key: 'slug',
          direction: 'desc' // you probably want 'asc' here
        }),
        validator: (obj) => typeof obj.key === 'string' && typeof obj.direction === 'string',
      }
    },
    data() {
      return {
        posts: [],
        loading: true,
        settings: {
            "arrows": true,
            "dots": true,
            "fade": true,
            "speed": 500,
            "infinite": true,
            "slidesToShow": 1,
            "slidesToScroll": 1,
            "cssEase": "linear",
            "swipe": true,
        },
      }
    },
    computed: {
      placeholderClasses() {
        const classes = ['w-full','w-2/3','w-5/6'];
        return [...Array.from({ length: this.amount }, (v, i) => classes[i % classes.length])]; // repeats classes after one another
      }
    },
    async mounted() {
      this.loading = true;
      this.posts = await this.fetchPosts();
      this.loading = false;
    },
    methods: {
      formatDate(dateString) {
        const date = new Date(dateString)
        return date.toLocaleDateString(process.env.lang) || ''
      },
      async fetchPosts(
          postType = this.postType,
          amount = this.amount,
          sortBy = this.sortBy,
        ) {
        return this.$content(postType)
          .sortBy(sortBy.key, sortBy.direction)
          .limit(amount)
          .fetch()
          .catch((err) => {
            error({ statusCode: 404, message: amount > 1 ? 'Posts not found' : 'Post not found' })
          });
      }
    },
  }
</script> 

