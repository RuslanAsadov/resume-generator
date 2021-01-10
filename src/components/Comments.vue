<template>

  <p v-if="!isOpen">
    <button class="btn primary" @click="openHandler">Загрузить комментарии</button>
  </p>

  <template v-else>
    
    <div class="card" v-if="comments.length">
      <h2>Комментарии</h2>
      <comments-list :comments="comments"></comments-list>
    </div>
    <app-loader v-else></app-loader>

  </template>

</template>

<script>
  import AppLoader from '@/components/AppLoader'
  import CommentsList from '@/components/CommentsList'

  export default {
    name: 'Comments',
    components: { AppLoader, CommentsList },
    data() {
      return {
        isOpen: false,
        comments: []
      }
    },
    methods: {
      async openHandler() {
        this.isOpen = true
        try {
          const response = await fetch(process.env.VUE_APP_COMMENTS_URL)
          this.comments = await response.json()
        } catch (e) {
          console.error(e)
          this.isOpen = false
        }
      }
    }
  }
</script>