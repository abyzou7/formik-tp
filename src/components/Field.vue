<template>
    <!-- Field -->
    <Component :is="as" v-bind="{
      value,
      onInput,
    }">
      <slot></slot>
    </Component>
  </template>
  
  <script lang="ts">
  // Formik imports
  import type { FormikValue, FormikValueGetter, FormikValueSetter } from '../../types/formik';
  export default {
    name: 'Field',
    props: {
      name: {
        type: String,
        required: true,
      },
      as: {
        type: String,
        default: 'input',
      },
    },
    inject: ['getValueByName', 'setValueByName'],
    data() {
      return {
        modelValue: null,
      }
    },
    computed: {
      value() {
        return (this.getValueByName as FormikValueGetter)(this.name)
      },
    },
    methods: {
      onInput(event: InputEvent) {
        const value: FormikValue = (event.target as HTMLInputElement).value
        return (this.setValueByName as FormikValueSetter)(this.name, value)
      },
    }
  }
  </script>
