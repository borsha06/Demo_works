<template>
  <v-ons-page>
   <div class="tabbar tabbar--top tabbar--top-border">
  <label class="tabbar__item tabbar--top-border__item">
    <input type="radio" name="top-tabbar-b" checked="checked">

    <button class="tabbar__button tabbar--top-border__button">
      TableCartel.com
    </button>
     </label>
</div>

  <ons-col width="100%">
                                  
    <div class="location_button" v-for="r in rest">
      <button  @click="restaurant(r.term_id)">
      {{ r.name }}
    </button>
          
            
              </div>
</ons-col>

  </v-ons-page>
</template>

<script>
  import customToolbar from './CustomToolbar';
  import rest_list from './Rest_list';
  import axios from 'axios'
  export default {
    name :'location',
  data () {
      return {
        rest : {}
      }
    },
    created () {
          this.fetchData()
      },
     watch: {
          '$route': 'fetchData'
     },
     methods: {
       fetchData () {
       this.loading= true
       axios.get('http://clients.itsd.com.bd/table-cartel/wp-json/wp/v2/all-terms?term=location')
         .then((resp) => {
           this.rest= resp.data
            //console.log('--------------------------------')
            //console.log(resp.data)
           this.loading = false
         })
         .catch((err) => {
//           console.log(err)
         })
     },
       restaurant(id) {
           this.pageStack.push({
               extends: rest_list,
               data() {
                   return {
                       data: {'id': id}
                   }
               }
           });
       },
       pop(){
         this.pageStack.pop();
       },
       push() {
         this.pageStack.push(rest_list);
       }
     },
     props: ['pageStack'],
     components: { customToolbar }
  }
</script>
<style>

.location_button{}
.location_button button{
    background: #fff;
    width: 100%;
    text-align: left;
    padding: 4px 3px;
    font-size: 15px;
    border-right: 1px solid #fff;
    border-bottom: bisque;

}

.location_button button:hover{
  background:#ddd;

}



</style>

