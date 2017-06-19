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
      <button v-on:click="addActivity" class="btn">Add Activity</button>
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

    if (typeof storedActivities !== 'undefined' && storedActivities.length > 0) {
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

<style lang="sass">
  .activity-list {
    *zoom: 1;

    &:before,
    &:after {
      content: " ";
      display: table;
    }

    &:after {
      clear: both;
    }
  }

  ul {
    padding: 0;
    list-style-type: none;
  }

  .add-activity {
    float: left;
    margin: 1em;
    padding: 1em;
    width: 100%;
    max-width: 12em;
    min-height: 13em;
    background-image: linear-gradient( 135deg, #5EFCE8 0%, #736EFE 100%);
    text-align: center;
    color: #ffffff;

    input {
      display: block;
      margin: 0 auto 1em;
      padding: 8px;
      width: 100%;
      background: transparent;
      border: none;
      border-bottom: 1px solid #ffffff;
      font-size: 1.2em;
      color: #ffffff;
      outline: none;

      &:active,
      &:focus {
        outline: none;
      }

      &.placeholder,
      &:-moz-placeholder,
      &::-moz-placeholder,
      &::-webkit-input-placeholder {
        color: rgba(#fff, 0.6);
      }
    }
  }

  @media (max-width: 500px) {
    .add-activity {
      float: none;
      display: block;
      margin-left: auto;
      margin-right: auto;
    }
  }

  .vdp-datepicker__calendar {
    top: calc(100% - 1px);
    left: -1em;
    color: #3c3c3c;
    max-width: 12em;
    border: 1px solid #3c3c3c;
  }
  
</style>