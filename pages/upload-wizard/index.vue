<template>
  <div class="upload-wizard-main">
    <Wizard @nextStep="handleNextStep" @complete="handleComplete">
      <WizardStep name="Services" :selected="true">
        <h1>What we do</h1>
        <input name="test" type="text" value="Step 1" />
      </WizardStep>
      <WizardStep name="Pricing">
        <h1>How much we do it for</h1>
        <input name="test" type="text" value="Step 2" />
      </WizardStep>
      <WizardStep name="About Us">
        <h1>Why we do it</h1>
        <input name="test" type="text" value="Step 3" />
      </WizardStep>
      <WizardStep name="Submit">
        <h1>Show the results</h1>
        <input name="test" type="text" value="Step 4" />
      </WizardStep>
    </Wizard>
  </div>
</template>

<script>

import { defineComponent } from '@vue/composition-api'

export default defineComponent({
  methods: {
    handleNextStep(prevData, nextData) {
      console.log(prevData.get('test'), nextData.get('test'));
    },
    handleComplete() {
      alert('Done!');
    },
  },
});
</script>

<style>
* {
  margin: 0;
  padding: 0;
  border: 0 solid black;
}

.upload-wizard-main {
  max-width: 700px;
  margin: 0 auto 0 auto;
}
</style>
