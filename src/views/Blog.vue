<template>
  <div id="blog-home">
      <h1>{{ page_title }}</h1>
      <div class="container">
        <div class="card" v-for="(post,index) in posts" :key="post.slug + '_' + index">
            <router-link :to="'/blog/' + post.slug">
            <article class="media">
                <figure>             
                <img v-if="post.featured_image" :src="post.featured_image" alt="">
                <img v-else src="http://via.placeholder.com/250x250" alt="">
                </figure>
                <h2>{{ post.title }}</h2>
                <p>{{ post.summary }}</p>
            </article>
            </router-link>
        </div>
      </div>
  </div>
</template>
<script>
import { butter } from "@/buttercms";
export default {
  name: "blog-home",
  data() {
    return {
      page_title: "Blog",
      posts: [],
      post: ""
    };
  },
  methods: {
    getPosts() {
      butter.post
        .list({
          page: 1,
          page_size: 10
        })
        .then(res => {
          // console.log(res.data)
          this.posts = res.data.data;
        });
    }
  },
  created() {
    this.getPosts();
  }
};
</script>

<style lang="scss">
.container{
    max-width: 800px;
    height: auto;
    margin: 0 auto;
    position: relative;
}
.card {
  max-width: 50%;
  min-height: 350px;
  float: left;
  margin-bottom: 10px;
  border-bottom: 1px solid rgba(#ddd, 0.5);

  img {
    max-width: 100%;
    height: autoM;
    margin: 0 auto;
    display: block;
  }
}
</style>
