<template>
  <p>{{ content }}</p>
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
