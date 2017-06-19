<template>
  <div id="app">
  	<h1>Days Since...</h1>
    <activity-list></activity-list>
  </div>
</template>

<script>
import ActivityList from './components/ActivityList.vue'

export default {
  name: 'app',
  components: {
    ActivityList
  }
}
</script>
