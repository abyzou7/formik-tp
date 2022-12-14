<template>
  <form class="Formik" @submit.prevent="handleSubmit">
    <h1>Formik TP</h1>
    <!-- Get every field -->
    <div v-for="field in fields">
      <label :for="field">{{ field }} : </label>
      <input type="text" v-model="form[field]" :placeholder="field">
      <!-- Show error if there is one -->
      <p v-if="errors[field]">
        <span style="color: red">
        {{ errors[field] }}
        </span>
      </p>
    </div>
    <!-- Submit button display -->
    <br/>
    <button type="submit" :disabled="isSubmitting">Submit</button>
    <!-- -->
  </form>
</template>

<script lang="ts">
const isEmpty = (obj: Object) => Object.keys(obj).length === 0

export default {
  name: 'Formik',
  props: {
    initialValues: {
      type: Object,
      required: true
    },
    validate: {
      type: Function,
      required: true,
    },
  },
  emits: ['submit'],
  data() {
    return {
      form: {},
      errors: {},
      isSubmitting: false,
    }
  },
  computed: {
    fields() {
      const fields = Object.keys(this.initialValues)

      return fields
    },
  },
  methods: {
    setIsSubmitting(isSubmitting) {
      this.isSubmitting = isSubmitting
    },
    handleSubmit() {
      const values = { ...this.form }
      this.errors = this.validate(values)

      if (isEmpty(this.errors)) {
        this.$emit('submit', values, this.setIsSubmitting)

        this.isSubmitting = true;
      }
    },
  },
  created() {
    this.form = { ...this.initialValues };
  }
}
</script>