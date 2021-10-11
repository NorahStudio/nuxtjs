<template>
  <div class="upload-wizard-main">
    <Wizard @nextStep="handleNextStep" @complete="handleComplete">
      <WizardStep name="Step 1" :selected="true">
        <h1>In Step 1</h1>
        <label for="step1_demo">Test Textbox1</label>
        <input id="step1_demo" name="test" type="text" value="Step 1" />
        <br>
        <br>
        <input type="radio" id="html" name="fav_language" value="HTML">
        <label for="html">HTML</label><br>
        <input type="radio" id="css" name="fav_language" value="CSS">
        <label for="css">CSS</label><br>
        <input type="radio" id="javascript" name="fav_language" value="JavaScript">
        <label for="javascript">JavaScript</label><br><br>
      </WizardStep>
      <WizardStep name="Step 2 / Upload">
        <h1>In Step 2</h1>
        <label for="step2_demo">Test Textbox2</label>
        <input id="step2_demo" name="test" type="text" value="Step 2" />
        <br>
        <br>
        <input type="file" @change="handleFileUpload"/>
        <p>{{ uploadStatus }}</p>
      </WizardStep>
      <WizardStep name="Step 3">
        <h1>In Step 3</h1>
        <label for="step3_demo">Test Textbox3</label>
        <input id="step3_demo" name="test" type="text" value="Step 3" />
        <br>
        <br>
      </WizardStep>
      <WizardStep name="Submit">
        <h1>Last Step~~</h1>
        <label for="step4_demo">Test Textbox4</label>
        <input id="step4_demo" name="test" type="text" value="Step 4" />
        <br>
        <br>
      </WizardStep>
    </Wizard>
  </div>
</template>

<script>

import { defineComponent } from '@vue/composition-api'
import Papa from 'papaparse'

export default defineComponent({
  methods: {
    handleNextStep(prevData, nextData) {
      console.log(prevData.get('test'), nextData.get('test'));
    },
    handleComplete() {
      alert('Done!');
    },
    handleFileUpload(event) {
      if (event.target.files == null || event.target.files[0] == null) {
        return;
      }
      const reader = new FileReader();
      const handleFileLoad = (e) => {
        reader.removeEventListener('load', handleFileLoad);
        const parsedData = Papa.parse(e.target.result);
        console.log(parsedData.data);
        this.uploadStatus = `${parsedData.data.length} rows have been uploaded. The parsed result is shown in console.`;
      };
      reader.addEventListener('load', handleFileLoad);
      reader.readAsText(event.target.files[0], 'UTF-8');
    },
  },
  data() {
    return { uploadStatus: 'Please upload a CSV file:' };
  },
});
</script>

<style>
* {
  margin: 0;
  padding: 0;
  border: 0 solid black;
}

button, input {
  padding: 5px 10px 5px 10px;
  border-radius: 3px;
  border: 1px solid black;
}

.upload-wizard-main {
  max-width: 700px;
  margin: 0 auto 0 auto;
}
</style>
