<template>
  <div class="card card-w70">

    <template v-if="contentItems.length">
      <component 
        v-for="item in contentItems" 
        :key="item.id"
        :is="getComponentName(item.type)" 
        :content="item.data" 
      ></component>
    </template>
    <h3 v-else>Добавьте первый блок, чтобы увидеть результат</h3>

  </div>
</template>

<script>
import ResumeContentHeading from '@/components/ResumeContent/ResumeContentHeading'
import ResumeContentSubheading from '@/components/ResumeContent/ResumeContentSubheading'
import ResumeContentImage from '@/components/ResumeContent/ResumeContentImage'
import ResumeContentText from '@/components/ResumeContent/ResumeContentText'

export default {
  name: 'ResumeContent',
  props: {
    contentItems: Array
  },
  components: { 
    ResumeContentHeading,
    ResumeContentSubheading,
    ResumeContentImage,
    ResumeContentText 
  },
  methods: {
    getComponentName(type) {
      return 'resume-content-' + type
    }
  }
}
</script>
