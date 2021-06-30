<template lang="html">

  <section class="my-events">
    <h1>Mes évènements</h1>
    <b-container fluid class='bg-light eventCont'>
      <b-row> 
        <b-col xl="12"  v-for="(event, i) in events" :key="i" >
          <b-button :class="selectedEvent===event ? 'eventButton eventButtonSelected' : 'eventButton'"  block  :variant="selectedEvent===event ? 'success' : 'outline-secondary' " v-on:click="onClickButton(event)">
            {{event.title}}
          </b-button>
        </b-col>  
      </b-row>
    </b-container>
  </section>
</template>

<script lang="js">

import {getAllEvents} from '../data';

  export default  {
    name: 'my-events',
    props: [],
    mounted () {

    },
    data () {
      return {
        events: getAllEvents(),
        selectedEvent: null
      }
    },
    methods: {
      onClickButton (event) {
            this.selectedEvent=event;
            this.$emit('selected', this.selectedEvent)
          }
    },
    computed: {

    }
}


</script>

<style scoped lang="scss">
  .eventButton {
    margin-top: 15px;
    padding-top: 20px;
    padding-bottom: 20px;
  }
  .eventButtonSelected {
    transform: scale(1.1);
  }
  
</style>
