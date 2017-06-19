<template>
  <div id="app">
  	<h1>DAYS SINCE...</h1>
    <activity-list></activity-list>
    <p>How long ago did you do that hobby? Or stick to that goal you're working towards? Don't let the days drift away.</p>
    <p>Data is stored locally, so no need for a login and it will be saved even if you close the tab.</p>
    <p>A <a href="https://vuejs.org/" target="_blank">Vue.js</a> one-night build by <a href="http://www.andrewlaskey.com" target="_blank">Andrew Laskey</a>. View on <a href="https://github.com/andrewlaskey/days-since-app" target="_blank">Github</a>.</p>
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

<style lang="sass">
@import url('https://fonts.googleapis.com/css?family=Oswald:400,600');

* {
	box-sizing: border-box;
}

body {
	margin: 0;
	font-family: 'Oswald', sans-serif;
	color: #3c3c3c;
}

#app {
	margin: 0 auto;
	width: 100%;
	max-width: 1024px;
}

h1 {
	margin: 0;
	text-align: center;
	font-size: 4em;
}

button {
	cursor: pointer;
}

.btn {
	display: block;
	margin: 0 auto;
	padding: 6px 18px;
	border: 2px solid #fff;
	border-radius: 4px;
	font-size: 1.2em;
	color: #ffffff;
	background: transparent;

	&:hover {
		color: #3c3c3c;
		background: #ffffff;
	}
}

p {
	text-align: center;

	a {
		color: #623AA2;
		text-decoration: none;
		cursor: pointer;

		&:visited {
			color: #623AA2;
		}
	}
}
</style>