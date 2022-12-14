<template>
    <div>
      <label :for="name">{{ name }}</label>
      <input :id="name" :name="name" :type="type" :value="value" @input="handleChange" />
      <div v-if="error">{{ error }}</div>
    </div>
  </template>
  
  <script lang="ts">
  export default {
    name: 'Field',
    props: {
      name: {
        type: String,
        required: true,
      },
      type: {
        type: String,
        default: 'text',
      },
      value: {
        type: String,
        default: '',
      },
      error: {
        type: String,
        default: '',
      },
    },
    emits: ['change'],
    methods: {
      handleChange(event: Event) {
          const target = event.target as HTMLInputElement
          this.$emit('change', target.value)
      },
    },
  }
  
  </script>
  