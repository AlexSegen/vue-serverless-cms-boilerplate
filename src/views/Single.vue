<template>
  <div id="blog-post">

    <article class="post-body">
    <div class="post-meta">
        <h1 class="post-title">{{ post.data.title }}</h1>
        <p class="post-details">Category: <a href="#!">Ninguna</a> | Published on {{post.data.created}}, by <span>{{ post.data.author.first_name }} {{ post.data.author.last_name }}</span></p>       
    </div>
    <div class="post-content" v-html="post.data.body"></div>
    </article>

    <template v-if="post.meta.previous_post">
        <router-link :to="/blog/ + post.meta.previous_post.slug" class="button">
        {{ post.meta.previous_post.title }}
        </router-link>
    </template>
    <template v-if="post.meta.next_post">
        <router-link  :to="/blog/ + post.meta.next_post.slug" class="button">
        {{ post.meta.next_post.title }}
        </router-link>
    </template>

  </div>


<!--     <div id="blog-post">
    <h1>{{ post.data.title }}</h1>
    <h4>{{ post.data.author.first_name }} {{ post.data.author.last_name }}</h4>
    <div v-html="post.data.body"></div>

    <router-link v-if="post.meta.previous_post" :to="/blog/ + post.meta.previous_post.slug" class="button">
      {{ post.meta.previous_post.title }}
    </router-link>
    <router-link v-if="post.meta.next_post" :to="/blog/ + post.meta.next_post.slug" class="button">
      {{ post.meta.next_post.title }}
    </router-link>
    </div>
 -->
</template>
<script>
  import { butter } from '@/buttercms'
  export default {
    name: 'blog-post',
    data() {
      return {
        post: {}
      }
    },
    methods: {
      getPost() {
        butter.post.retrieve(this.$route.params.slug)
          .then((res) => {
            // console.log(res.data)
            this.post = res.data
          }).catch((res) => {
            console.log(res)
          })
      }
    },
    watch: {
      $route(to, from) {
        this.getPost()
      }
    },
    created() {
      this.getPost()
    }
  }
</script>
<style lang="scss">
.post-body {
  margin: 10px auto;
  max-width: 600px;
  height: auto;
  padding: 10px;

  .post-content{
      img{
          max-width: 100%;
          height: auto;
      }
  }
  .post-meta {
    .post-title {
      margin-bottom: 3px;
    }
    .post-details {
      span {
        font-weight: 600;
      }
      a {
        color: teal;
        font-weight: 600;
      }
    }
  }
}
</style>
