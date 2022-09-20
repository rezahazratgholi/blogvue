<script>
  import axios from 'axios'
  import { Swiper, SwiperSlide } from "swiper/vue";
  import "swiper/css";
  import "swiper/css/pagination";
  import { Pagination } from "swiper";
  import BlogItem from "./components/BlogItem.vue";
export default {
  emits : ['show-blog'],
  components: {
    Swiper,
    SwiperSlide,
    BlogItem,
  },
  created() {
    axios.get('https://631b4332fae3df4dcff9acc9.mockapi.io/blogs')
            .then(res => {
              this.posts = res.data;
              console.log(this.posts)
            })
  },
  setup() {
    return {
      modules: [Pagination],
    };
  },
  data(){
    return {
      posts : [],
      post : {},
      listMode : true,
      createMode : false,
      showMode : false,
    }
  },
  paginationSettings : {
    dynamicBullets: true,
    slidesPerView : 3
  },
  methods : {
    showBlogHandler(id){
      const blog = this.posts.filter(post => post.id == id)[0];
      this.post = blog;
      this.listMode = false;
      this.showMode = true;
    }
  }

};
</script>

<template>
  <section v-show="listMode" v-if="posts.length > 0" class="row">
    <h2>Last News</h2>
    <swiper :pagination="paginationSettings" :slides-per-view="3" :modules="modules" class="mySwiper" >
      <swiper-slide v-for="post in posts">
        <BlogItem @show-blog="showBlogHandler" :blog="post" />
      </swiper-slide>
    </swiper>
  </section>
  <section v-if="showMode" ref="blogShow">
    <h2>{{post.title}}</h2>
  </section>

</template>

<style>
</style>
