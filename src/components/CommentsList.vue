<template>
  <ul class="list">

    <li 
      class="list-item"
      v-for="item in comments"
      :key="item.id"
    >
      <div>
        <p><strong>{{ item.email }}</strong></p>
        <small>{{ item.body }}</small>
      </div>
    </li>

  </ul>
</template>

<script>
export default {
  name: 'CommentsList',
  props: {
    comments: Array
  }
}
</script>
