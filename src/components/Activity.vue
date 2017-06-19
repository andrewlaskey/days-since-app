<template>
	<div class="activity">
		<h3>{{ activity.name }}</h3>
		<div class="days-since">{{ daysSince }}</div>
		<button v-on:click="update">I Did It</button>
		<button v-on:click="removeMe">Delete</button>
	</div>
</template>

<script>
import moment from 'moment'

export default {
  name: 'activity',
  props: ['activity', 'onUpdate'],
  data () {
    return {}
  },
  computed: {
  	daysSince () {
  		this.activity.lastDate = moment(this.activity.lastDate)
  		return Math.abs(this.activity.lastDate.diff(moment(), 'days'))
  	}
  },
  methods: {
  	update (event) {
  		event.preventDefault()

  		this.activity.lastDate = moment()

  		this.onUpdate()
  	},
  	removeMe () {
  		this.$emit('remove')
  	}
  }
}
</script>