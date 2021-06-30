<template>
  <div id="app">
    <b-container fluid class='px-lg-5'>
      <b-row class='d-flex justify-content-center'> 
        <b-col xs='12' xl="3">
            <MyEvents @selected="onSelectedEvent" class='px-5 px-xl-0'/>
        </b-col> 
        <b-col xs='12' md='6' xl="5">
            <div v-if="selectedEvent!==null">
              <Details :selected="selectedEvent" class='px-xl-5 py-xl-0 py-5' />
            </div>
        </b-col> 
        <b-col xs='12' md='6' xl="4">
            <div v-if="selectedEvent!==null">
             <Commentaires :selected="selectedEvent" class='py-xl-0 py-5'/>
            </div>
        </b-col>  
      </b-row>
    </b-container>
  </div>
</template>

<script>
import MyEvents from './components/MyEvents.vue'
import Details from './components/Details.vue'
import Commentaires from './components/Commentaires.vue'

export default {
  name: 'App',
  components: {
    MyEvents,Details,Commentaires
  },
  data () {
      return {
        selectedEvent: null
      }
    },
  methods: {
    onSelectedEvent (value) {
      this.selectedEvent=value;
    }
  }

}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
