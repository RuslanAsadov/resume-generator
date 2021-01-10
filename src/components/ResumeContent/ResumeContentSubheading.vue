<template>
  <h2>{{ content }}</h2>
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
