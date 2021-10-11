<template>
  <div>
    <div class="steps">
      <ul>
        <li
          v-for="step in steps"
          v-bind:key="step.name"
          :class="{ 'is-active': step.isActive }"
        >
          <div>
            <a :href="step.href" @click="selectStep(step)">{{ step.name }}</a>
          </div>
        </li>
      </ul>
    </div>
    <div class="steps-details">
      <slot></slot>
    </div>
    <div class="footer">
      <button @click="goToNext()">{{ isLast ? 'Finish' : 'Next' }}</button>
    </div>
  </div>
</template>
<script>
import { defineComponent } from '@vue/composition-api'

export default defineComponent({
  name: 'Wizard',

  data() {
    return { steps: [], selectedStep: undefined };
  },

  created() {
    this.steps = this.$children;
  },

  mounted() {
    this.selectedStep = this.steps[0];
  },

  methods: {
    selectStep(selectedStep) {
      this.steps.forEach(step => {
        step.isActive = (step.name == selectedStep.name);
      });
      this.$emit('nextStep', this.selectedStep.formData, selectedStep.formData);
      this.selectedStep = selectedStep;
    },
    goToNext() {
      if (this.isLast) {
        this.$emit('complete');
        return;
      }
      const activeIdx = this.steps.findIndex(x => x.isActive);
      this.selectStep(this.steps[activeIdx + 1]);
    },
  },

  computed: {
    isLast() {
      return (this.steps.length - 1) === this.steps.findIndex(x => x.isActive);
    },
  }
})
</script>

<style>
.steps > ul {
  height: 40px;
  line-height: 40px;
  list-style: none;
  display: flex;
  align-content: stretch;
  justify-content: space-evenly;
  align-items: stretch;
}

.steps > ul > li {
  text-align: center;
  width: 100%;
  background-color: rgb(240, 240, 240);
}

.steps > ul > li.is-active {
  background-color: rgb(140, 140, 140);
}

.footer {
  display: flex;
  flex-direction: row-reverse;
  padding-top: 20px;
}
</style>
