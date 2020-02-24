<template>
  <div id="app">
    <issue-form></issue-form>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'
import IssueForm from './components/IssueForm.vue'

@Component({
  components: {
    IssueForm
  }
})
export default class App extends Vue {}
</script>

<style lang="scss">
#app {
  margin: 0 auto;
  max-width: 750px;
}
</style>
