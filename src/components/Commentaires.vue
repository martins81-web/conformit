import { GetEventComments } from '../data';
<template lang="html">

  <section class="commentaires">
    <span><b>Commentaires</b></span>
    <div class='commentBox bg-light'>
      <!-- New Comment -->
      <div>
        <b-button block variant="success" v-on:click="addComment=true" >Nouveau commentaire</b-button>
      </div>
      <div v-if="addComment">
          <b-card no-body class='px-3 py-1 my-2 '>

          <span class='headerIcons'>
              <button class="btn p-0" v-on:click="addComm(newComment)">
                <b-icon icon="check-square-fill" scale="1" variant="success"></b-icon>
              </button>
              <button class="btn p-0" v-on:click="addComment=false">
                <b-icon icon="x-square-fill" scale="1" variant="danger"></b-icon>
              </button>
          </span>

          <div class='avatar my-3'>
            <b-avatar></b-avatar>
            <div class='item'>
              <div>
                <b-form-input v-model="newComment.author" placeholder='Auteur'></b-form-input>
              </div>
              <div class='mt-1'>
                <b-form-textarea
                  placeholder='Commentaire'
                  v-model="newComment.content"
                  rows="3"
                ></b-form-textarea>
              </div>
            </div>
          </div>
          
        </b-card>
      </div>
      
      <div v-for="(comment, i) in eventComments" :key="i" >
        <!-- Delete/Edit Comment -->
        <div v-if="editComment!==comment">
          <b-card no-body class='px-3 py-2 my-2'>
            <span class='headerIcons'>
              <button class="btn p-0" v-on:click="deleteComment(comment)">
                <b-icon icon="trash-fill" scale="1" variant="danger"></b-icon>
              </button>
              <button class="btn p-0" v-on:click="editComment=comment" >
                <b-icon icon="pencil" scale="1" variant="success"></b-icon>
              </button>
            </span>

            <div class='avatar my-2'>
              <b-avatar></b-avatar>
              <div class='item'>
                <span class="text-muted font-weight-bold">{{comment.author}}</span>
                <br>
                {{comment.content}}
              </div>
            </div>
            <span class='footerDate'>{{format_date(comment.creationDate)}}</span>
          </b-card>
        </div>
        <!-- Edit Comment -->
        <div v-else>
          <b-card no-body class='px-3 py-1 my-2 '>
            <span class='headerIcons'>
              <button class="btn p-0" v-on:click="saveComment()">
                <b-icon icon="check-square-fill" scale="1" variant="success"></b-icon>
              </button>
              <button class="btn p-0" v-on:click="editComment=false">
                <b-icon icon="x-square-fill" scale="1" variant="danger"></b-icon>
              </button>
            </span>

            <div class='avatar my-3'>
              <b-avatar></b-avatar>
              <div class='item'>
                <div>
                  <b-form-input v-model="comment.author" placeholder='Auteur'></b-form-input>
                </div>
                <div class='mt-1'>
                  <b-form-textarea
                    placeholder='Commentaire'
                    v-model="comment.content"
                    rows="3"
                  ></b-form-textarea>
                </div>
              </div>
            </div>
            <span class='footerDate'>{{format_date(comment.creationDate)}}</span>

          </b-card>
        </div>
      </div>
    </div>
  </section>
</template>

<script lang="js">
  import {GetEventComments} from '../data';
  import moment from 'moment'

  export default  {
    name: 'commentaires',
    props: ['selected'],
    data () {
      return {
        eventComments: null,
        addComment: false,
        editComment: false,
        newComment: {
          creationDate: new Date(),
          author: "",
          content: ""
        }
      }
    },
    methods: {
        format_date(value){
          moment.locale('fr');
        let date = moment(value);
         if (date) {
           return moment(date).format('Do MMMM YYYY')
          }
      },
      deleteComment(comment){
        let index=this.eventComments.indexOf(comment);
        this.eventComments.splice(index,1);
      },
      addComm(comment){
        this.eventComments.push(comment);
        this.addComment=false;
        this.newComment= {
          creationDate: new Date(),
          author: "",
          content: ""
        }
      },
        saveComment(){
          this.editComment=false;
        }
    },
    computed: {

    }, 
    watch: { 
      selected: function(newVal, oldVal) { // watch it
        console.log('Prop changed: ', newVal, ' | was: ', oldVal);
        this.eventComments=GetEventComments(newVal.id);
      }
    },
    mounted() {
      this.$nextTick(function () {
        this.eventComments=GetEventComments(this.selected.id);
      })
  }
}


</script>

<style scoped lang="scss">
  .commentaires {
    text-align: left;
    
 }
  .avatar{
    display: flex;
    align-items: center;
  }
  .item{
    margin-left: 15px;
    flex-grow: 1
  }
  .footerDate{
    display: flex;
    flex-direction: row-reverse
  }
  .headerIcons{
    display: flex;
    flex-direction: row-reverse
  }
  .commentBox{
    padding: 25px;
    overflow-y: scroll;

  }

   
</style>
