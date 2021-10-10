<template>
  <form v-show="isActive" ref="form">
    <slot></slot>
  </form>
</template>
<script>
import { defineComponent } from '@vue/composition-api'

export default defineComponent({
  name: 'WizardStep',
  props: {
    name: { required: true },
    selected: { default: false },
  },

  data() {
    return {
      isActive: false,
    };
  },

  computed: {
    href() {
      return '#' + this.name.toLowerCase().replace(/ /g, '-');
    },
    formData() {
      return new FormData(this.$refs.form);
    },
  },

  mounted() {
    this.isActive = this.selected;
  }
})
</script>

<style>
</style>
