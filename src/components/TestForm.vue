<template>
  <div id="app" class="container mt-2">
      <PageTitle :titleText="pageTitle" />
    <form @submit.prevent="calculateResult">
      <div class="row mb-3">
        <label for="field1" class="form-label col-sm-2">Field 1 (Number)</label>
        <div class="col-sm-10">
          <input v-model="field1" type="number" class="form-control" id="field1" required>
        </div>
      </div>
      <div class="row mb-3">
        <label for="field2" class="form-label col-sm-2">Field 2 (Number)</label>
        <div class="col-sm-10">
          <input v-model="field2" type="number" class="form-control" id="field2" required>
        </div>
      </div>
    <div class="row mb-3">
          <label class="form-label col-sm-2">Field 3 (Options)</label>
          <div class="col-sm-10">
            <div class="form-check">
              <input v-model="field3" class="form-check-input" type="radio" value="divide" id="operationDivide" @change="resetResult" required>
              <label class="form-check-label" for="operationDivide">Divide</label>
            </div>
            <div class="form-check">
              <input v-model="field3" class="form-check-input" type="radio" value="complex" id="operationComplex" @change="resetResult" required>
              <label class="form-check-label" for="operationComplex">Complex</label>
            </div>
          </div>
        </div>
      <div v-if="field3 === 'complex'" class="row mb-3">
        <label for="field4" class="form-label col-sm-2">Field 4 (Dropdown)</label>
        <div class="col-sm-10">
          <select v-model="field4" class="form-select" id="field4" required>
            <option value="two">Two</option>
            <option value="three">Three</option>
          </select>
        </div>
      </div>
            <!-- Display Complex Result -->
      <div v-if="result !== null && field3 === 'complex'" class="mt-3">
          <h4>Result:</h4>
          <p>{{ result }}</p>
      </div>
      <div class="row">
        <div class="col-sm-2">

        </div>
        <div class="col-sm-10">
          <button type="submit" class="btn btn-primary">Submit</button>
        </div>
      </div>

      <!-- Display Divide Result -->
      <div v-if="result !== null && field3 === 'divide'" class="mt-3">
        <h4>Result:</h4>
        <p>{{ result }}</p>
      </div>
    </form>
  </div>
</template>

<script>
import PageTitle from './PageTitle.vue';

export default {
  components:{
    PageTitle,
  },
  data() {
    return {
      pageTitle: 'Test Page',
      field1: null,
      field2: null,
      field3: null,
      field4: null,
      result: null,
    };
  },
  methods: {
    calculateResult() {
      if (this.field3 === 'divide') {
        // RB1 option selected: Divide Field 1 by Field 2
        this.result = this.field1 / this.field2;
      } else if (this.field3 === 'complex') {
        // RB2 option selected: Multiply Field 1 by Field 2
        const multiplicationResult = this.field1 * this.field2;

        // Elevate the previous result to the number indicated in Field 4
        if (this.field4 === 'two') {
          this.result = multiplicationResult * 2;
        } else if (this.field4 === 'three') {
          this.result = multiplicationResult * 3;
        }
      }
    },
    resetResult() {
      // Reset result to null when options change
      this.result = null;
    },
  },
};
</script>

<style>

</style>
