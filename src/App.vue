<template>
  <div class="container column">
    
    <resume-form @createContent="createContentHandler"></resume-form>
    <resume-content :contentItems="contentItems"></resume-content>

  </div>
  <div class="container">
    
    <comments></comments>
    
  </div>
</template>

<script>
  import ResumeForm from '@/components/ResumeForm'
  import ResumeContent from '@/components/ResumeContent/ResumeContent'
  import Comments from '@/components/Comments'

  export default {
    name: 'App',
    components: { ResumeForm, ResumeContent, Comments },
    data() {
      return {
        contentItems: []
      }
    },
    async created() {
      try {
        const response = await fetch(process.env.VUE_APP_DATABASE_URL + '/content.json')
        const data = await response.json()
        this.contentItems = data ? Object.values(data) : []
      } catch (e) {
        console.error(e)
      }
    },
    methods: {
      async createContentHandler(item) {
        try {
          this.contentItems.push(item)
          await fetch(process.env.VUE_APP_DATABASE_URL + '/content.json', {
            method: 'POST',
            headers: {
              'Content-Type': 'application/json'
            },
            body: JSON.stringify(item)
          })
        } catch (e) {
          console.error(e)
        }
      }
    }
  }
</script>

