<template>

  <p v-if="!comments.length">
    <button class="btn primary" @click="openHandler">Загрузить комментарии</button>
  </p>
    
  <div class="card" v-else>
    <h2>Комментарии</h2>
    <comments-list :comments="comments"></comments-list>
  </div>

</template>

<script>
  import CommentsList from '@/components/CommentsList'

  export default {
    name: 'CommentsBlock',
    components: { CommentsList },
    props: {
      comments: Array
    },
    methods: {
      openHandler() {
        this.$emit('load-comments')
      }
    }
  }
</script>