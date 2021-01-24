<template>
  <div class="container column">
    
    <resume-form @create-content="createContentHandler"></resume-form>

    <resume-content 
      v-if="!loadingView"
      :items="contentItems"
    ></resume-content>
    <app-loader v-else></app-loader>

  </div>
  <div class="container">
    
    <comments-block 
      v-if="!loadingComments"
      :comments="comments"
      @load-comments="loadCommentsHandler"  
    ></comments-block>
    <app-loader v-else></app-loader>
    
  </div>
</template>

<script>
  import ResumeForm from '@/components/ResumeForm'
  import ResumeContent from '@/components/ResumeContent/ResumeContent'
  import CommentsBlock from '@/components/CommentsBlock'
  import AppLoader from '@/components/AppLoader'

  export default {
    name: 'App',
    components: { ResumeForm, ResumeContent, CommentsBlock, AppLoader },
    data() {
      return {
        contentItems: [],
        comments: [],
        loadingView: true,
        loadingComments: false
      }
    },
    async mounted() {
      try {
        const response = await fetch(process.env.VUE_APP_DATABASE_URL + '/content.json')
        const data = await response.json()
        this.contentItems = data ? Object.values(data) : []
      } catch (e) {
        console.error(e)
      } finally {
        this.loadingView = false
      }
    },
    methods: {
      async createContentHandler(item) {
        try {
          await fetch(process.env.VUE_APP_DATABASE_URL + '/content.json', {
            method: 'POST',
            headers: {
              'Content-Type': 'application/json'
            },
            body: JSON.stringify(item)
          })
          this.contentItems.push(item)
        } catch (e) {
          console.error(e)
        }
      },
      async loadCommentsHandler() {
        try {
          this.loadingComments = true
          const response = await fetch(process.env.VUE_APP_COMMENTS_URL)
          this.comments = await response.json()
        } catch (e) {
          console.error(e)
        } finally {
          this.loadingComments = false
        }
      }
    }
  }
</script>

