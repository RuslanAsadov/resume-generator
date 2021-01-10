<template>
  <div class="avatar">
    <img :src="content">
  </div>
</template>

<script>
export default {
  props: {
    content: {
      default: 'https://sbis.perm.ru/wp-content/uploads/2019/09/placeholder.png',
      required: true,
      type: String
    }
  }
}
</script>

<style>
  .avatar {
    display: flex;
    justify-content: center;
  }

  .avatar img {
    width: 150px;
    height: auto;
    border-radius: 50%;
  }
</style>
