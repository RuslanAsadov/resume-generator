<template>
  <div class="card card-w70" v-if="!loading">

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
  <app-loader v-else></app-loader>
</template>

<script>
import ResumeContentHeading from '@/components/ResumeContent/ResumeContentHeading'
import ResumeContentSubheading from '@/components/ResumeContent/ResumeContentSubheading'
import ResumeContentImage from '@/components/ResumeContent/ResumeContentImage'
import ResumeContentText from '@/components/ResumeContent/ResumeContentText'
import AppLoader from '@/components/AppLoader'

export default {
  name: 'ResumeContent',
  props: {
    contentItems: Array,
    loading: Boolean
  },
  components: { 
    ResumeContentHeading,
    ResumeContentSubheading,
    ResumeContentImage,
    ResumeContentText,
    AppLoader
  },
  methods: {
    getComponentName(type) {
      return 'resume-content-' + type
    }
  }
}
</script>
