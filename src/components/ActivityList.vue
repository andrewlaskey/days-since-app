<template>
	<div class="activity-list">
    <ul>
        <li v-for="(activity, index) in activities">
          <activity :activity="activity" :onUpdate="saveData" v-on:remove="removeItem(index)"></activity>
        </li>
    </ul>
    <div class="add-activity">
      <input v-model="activityName" placeholder="Activity...">
      <datepicker v-model="activityLastDate"></datepicker>
      <button v-on:click="addActivity">Add Activity</button>
    </div>
	</div>
</template>

<script>
import moment from 'moment'
import store from 'store'
import Datepicker from 'vuejs-datepicker'
import Activity from './Activity.vue'

export default {
  name: 'activity-list',
  data () {
    return {
      activities: [],
      activityName: '',
      activityLastDate: new Date()
    }
  },
  components: {
    Activity,
    Datepicker
  },
  created () {
    let storedActivities = store.get('activities')

    console.log(storedActivities)

    if (storedActivities.length > 0) {
      this.activities = storedActivities
    } else {
      this.activities = [
        {
          name: 'Read',
          lastDate: moment().subtract(1, 'days')
        },
        {
          name: 'Gym',
          lastDate: moment().subtract(3, 'days')
        }
      ]
    }
  },
  updated () {
    this.saveData()
  },
  methods: {
    addActivity () {
      this.activities.push({
        name: this.activityName,
        lastDate: moment(this.activityLastDate)
      })

      this.activityName = ''
      this.activityLastDate = new Date()
    },
    removeItem (index) {
      this.activities.splice(index, 1)
    },
    saveData () {
      store.set('activities', this.activities)
    }
  }
}
</script>