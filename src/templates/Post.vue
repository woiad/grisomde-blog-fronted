<template>
  <Layout>
    <!-- Page Header -->
    <header
      class="masthead"
      :style="{backgroundImage: `url(${ GRIDSOME_API_URL + $page.post.cover.url})`}"
    >
      <div class="overlay"></div>
      <div class="container">
        <div class="row">
          <div class="col-lg-8 col-md-10 mx-auto">
            <div class="post-heading">
              <h1>{{ $page.post.title }}</h1>
<!--              <h2 class="subheading">Problems look mighty small from 150 miles up</h2>-->
              <span class="meta">Posted by
              <a href="#">Start Bootstrap</a>
              on {{ $page.post.created_at | date('MMM DD, YYYY') }}</span>
            </div>
          </div>
        </div>
      </div>
    </header>

    <!-- Post Content -->
    <article>
      <div class="container">
        <div class="row">
          <div
            class="col-lg-8 col-md-10 mx-auto"
            v-html="markdownToHtml($page.post.content)"
          >
          </div>
        </div>
      </div>
    </article>

  </Layout>
</template>
<page-query>
query($id: ID!){
  post: strapiPost(id: $id){
    id
    title
    created_at
    content
    cover{
      url
    }
    tags{
      title
    }
  }
}
</page-query>

<script>
import MarkdownIt from 'markdown-it'
const md = new MarkdownIt
export default {
  name: 'Post',
  metaInfo () {
    return {
      title: this.$page.post.title
    }
  },
  methods: {
    markdownToHtml (markdown) {
      if (!markdown) return ''
      return md.render(markdown)
    }
  }
}
</script>

<style>

</style>
