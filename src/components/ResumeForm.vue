<template>
  <form class="card card-w30" @submit.prevent="submitHandler">
    <div class="form-control">
      <label for="type">Тип блока</label>
      <select id="type" v-model="type">
        <option value="heading">Заголовок</option>
        <option value="subheading">Подзаголовок</option>
        <option value="image">Аватар</option>
        <option value="text">Текст</option>
      </select>
    </div>

    <div class="form-control">
      <label for="value">Значение</label>
      <textarea id="value" rows="3" v-model="value"></textarea>
    </div>

    <button class="btn primary" type="submit" :disabled="!validValue">Добавить</button>
  </form>
</template>
<script>
export default {
  name: 'ResumeForm',
  emits: ['createContent'],
  data() {
    return {
      type: 'heading',  
      value: ''
    }
  },
  methods: {
    submitHandler() {
      if (this.validValue) {
        const data = {
          id: Date.now(),
          type: this.type,
          data: this.value,
        }
        this.$emit('createContent', data)

        this.value = ''
        this.type = 'heading'
      }
    }
  },
  computed: {
    validValue() {
      return this.value.length > 3
    }
  }
}
</script>