<template lang="html">
  <div class="details">
    <section>
      <h1 class='title'>{{selected.title}}</h1>
    </section>
    <p class="eventSubTitle">Crée le {{format_date(selected.creationDate)}} à {{format_hour(selected.creationDate)}} par {{selected.createdBy}}</p>
    <form class='form'>
      <span><b>Titre</b></span><br>
       <div>
        <b-form-input v-model="selected.title"></b-form-input>
      </div>
      <br>
      <span><b>Description</b></span><br>
       <div>
          <b-form-textarea
            id="textarea"
            v-model="selected.description"
            rows="3"
          ></b-form-textarea>
        </div>
      <br>
      <b-row> 
        <b-col xl="6">
            <span><b>Date</b></span><br>
             <div>
              <b-form-datepicker  :date-format-options="{ year: 'numeric', month: 'numeric', day: 'numeric' }"
              :value="format_date(selected.creationDate)"  disabled locale="fr"></b-form-datepicker>
            </div>
        </b-col> 
        <b-col xl="6">
            <span><b>Heure</b></span><br>
            <div>
              <b-form-timepicker :value="format_hour(selected.creationDate)" locale="fr" disabled></b-form-timepicker>
            </div>
        </b-col> 
      </b-row>
      <br>
      <span><b>Nom du statut</b></span><br>
       <div>
        <b-form-select v-model="selected.statusName" >
          <b-form-select-option value="Open">Open</b-form-select-option>
          <b-form-select-option value="Closed">Closed</b-form-select-option>
          <b-form-select-option value="InProgress">InProgress</b-form-select-option>
        </b-form-select>
      </div>
      <br>
      <span><b>Employé impliqué</b></span><br>
        <b-form-select v-model="selected.involvedEmployeeId">
          <b-form-select-option v-for="(employee, i) in employees" :key="i" :value="employee.id" > 
          {{employee.firstname+" "+employee.lastname+ " (" + employee.id + ")"}}
          </b-form-select-option>
        </b-form-select>
    
      <br><br>
      <span><b>Témoins</b></span><br>
      <b-form-tags v-model="selected.Témoins" size='lg' tag-pills placeholder tag-variant="success"/>
    </form>
  </div>
</template>

<script lang="js">
  import moment from 'moment'
  import {getAllEmployees} from '../data';

  export default  {
    name: 'details',
    props: ['selected'],
    mounted () {

    },
    data () {
      return {
        employees: getAllEmployees(),
      }
    },
    methods: {
      format_date(value){
        let date = moment(value);
         if (date) {
           return moment(date).format('YYYY-MM-DD')
          }
      },
      format_hour(value){
          let date = moment(value);
         if (date) {
           return moment.utc(date).format("HH:mm")
         }
      },
    },
    computed: {

    },
   
}


</script>

<style scoped>
  .title {
    font-weight: bold
  }

  .details{
    text-align: left;
    padding: 0px 20px 0px 20px
  }
  textarea
{
  width:100%;
}
</style>
