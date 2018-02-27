<template>
	<div class="activity">
		<h3>{{ activity.name }}</h3>
		<div class="days-since">{{ daysSince }}</div>
		<button v-on:click="update" class="btn">I Did It</button>
		<button v-on:click="removeMe" class="icon-btn">
			<span>Delete</span>
			<svg version="1.1" xmlns="http://www.w3.org/2000/svg" width="512" height="512" viewBox="0 0 512 512">
  			<title></title>
  			<path d="M64 160v320c0 17.6 14.4 32 32 32h288c17.6 0 32-14.4 32-32v-320h-352zM160 448h-32v-224h32v224zM224 448h-32v-224h32v224zM288 448h-32v-224h32v224zM352 448h-32v-224h32v224z"></path>
  			<path d="M424 64h-104v-40c0-13.2-10.8-24-24-24h-112c-13.2 0-24 10.8-24 24v40h-104c-13.2 0-24 10.8-24 24v40h416v-40c0-13.2-10.8-24-24-24zM288 64h-96v-31.599h96v31.599z"></path>
  			</svg>
		</button>
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

<style lang="sass">
.activity {
	position: relative;
	float: left;
	margin: 1em;
	padding: 1em;
	width: 100%;
	max-width: 12em;
	min-height: 13em;
	background-image: linear-gradient( 135deg, #F97794 0%, #623AA2 100%);
	text-align: center;
	color: #ffffff;
}

@media (max-width: 500px) {
	.activity {
		float: none;
		display: block;
		margin-left: auto;
		margin-right: auto;
	}
}

.activity h3 {
	margin: 0;
	font-size: 1.5em;
	font-weight: 400;
	letter-spacing: 1px;
}

.days-since {
	font-size: 4em;
}

.icon-btn {
	position: absolute;
	top: 5px;
	right: 5px;
	background: transparent;
	border: none;
	color: #ffffff;

	span { 
	  position: absolute; 
	  overflow: hidden; 
	  clip: rect(0 0 0 0); 
	  height: 1px; width: 1px; 
	  margin: -1px; padding: 0; border: 0; 
	}

	svg {
		display: inline-block;
		width: 1em;
		height: 1em;
		fill: currentColor;
		vertical-align: middle;
	}
}
</style>