<template>
  <Formik :initial-values="initialValues" :validate="validate" @submit="handleSubmit" />
</template>

<script lang="ts">
import Formik from "./components/Formik.vue"

export default {
  name: 'App',
  components: {
    Formik,
  },
  data() {
    return {
      initialValues: {
        email: '',
        password: '',
      }
    }
  },
  methods: {
    validate(values) {
      console.log(values)
      const errors = {};

      if (!values.email) {
        errors.email = 'Email is required';
      } else if (
        !/^[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,}$/i.test(values.email)
      ) {
        errors.email = 'Incorrect email format';
      }

      if (!values.password) {
        errors.password = 'Password is required';
      }
      return errors;
    },
    handleSubmit(values, setIsSubmitting) {
      console.log('Form submitted', values)
      setTimeout(() => {
        setIsSubmitting(false);
      }, 2000)
    }
  }
}
</script>


<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
