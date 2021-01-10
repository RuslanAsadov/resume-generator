<template>
  <h1>{{ content }}</h1>
</template>

<script>
export default {
  props: {
    content: {
      default: '',
      required: true,
      type: String
    }
  }
}
</script>
